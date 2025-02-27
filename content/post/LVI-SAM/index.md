---
title: LVI-SAM
summary: Tightly-coupled Lidar-Visual-Inertial Odometry via Smoothing and Mapping
date: 2021-06-12 15:08:08
tags: 
    - SLAM
    - RGB
    - PointCloud
    - IMU
---
# LVI-SAM:基于SAM的紧耦合激光雷达-视觉-惯导里程计

## 论文信息
**论文标题：** LVI-SAM: Tightly-coupled Lidar-Visual-Inertial Odometry via Smoothing and Mapping
**论文来源：** ICRA 2021
**论文链接：** https://arxiv.org/abs/2104.10831
**代码：** https://github.com/TixiaoShan/LVI-SAM

## 简介
作者提出了一个基于SAM的激光雷达-视觉-惯性测距框架 LVI-SAM，它实现了高精度和鲁棒的实时状态估计和地图构建。 LVI-SAM 建立在因子图(factor graph)之上，由两个子系统组成：视觉惯性系统 (VIS) 和激光雷达惯性系统 (LIS)。这两个子系统以紧耦合的方式设计，其中 VIS 利用 LIS 的估计来进行初始化。通过使用激光雷达的扫描数据提取视觉特征的深度信息，提高了 VIS 的精度。反过来，LIS 利用 VIS 估计进行初始猜测以支持扫描点的匹配。闭环检测首先由 VIS 识别，然后由 LIS 进一步细化。 LVI-SAM 也可以在两个子系统之一出现问题时正常使用，从而提高其在无纹理和无特征环境中的稳健性。 LVI-SAM 对从多个平台在各种规模和环境中收集的数据集进行了广泛评估。

## 特点
1、实现了一个紧耦合的激光-视觉-惯导系统，通过因子图同时完成了多传感器融合和全局优化（包含回环检测）两项任务。
2、通过故障检测机制，绕过出现问题的子系统(LIS或VIS)，提高了整个系统的鲁棒性。

## 算法框架
![](https://notes.sjtu.edu.cn/uploads/upload_4ef6432c2459e6c1594e60d8b5efe625.png)
如算法流程框图所示，LVI-SAM系统主要分为基于视觉+惯导和点云+惯导两个系统。其中，VIS系统作者使用经典的VINS-Mono作为baseline。
### VIS
![](https://notes.sjtu.edu.cn/uploads/upload_93ea99968713aa2931a9c157933e245a.png)
该视觉系统的特征点通过角点来进行提取，跟踪算法使用Lucas-Tomasi算法。与VINS-Mono不同之处在于，该VIS系统初始化时，会将激光雷达帧与视觉数据配准后获得一个稀疏的深度图，该深度图可用于辅助获得视觉特征点的深度信息。之后再通过优化视觉和IMU的测量联合残差得到视觉里程计。
#### 初始化
由于在初始化时解决高度非线性问题，基于优化的 VIO 通常会出现发散。初始化的质量在很大程度上取决于两个因素：初始传感器运动和 IMU 参数的准确程度。在实践中，作者发现当传感器以小速度或恒定速度行进时，VINS-Mono经常无法初始化。这是因为当加速度激励不够大时观察变得十分困难。IMU 数据中噪声和偏差的比重过高，它们会影响原始加速度和角速度测量。在初始化时对这些参数的正确猜测有助于优化更快地收敛。
为了提高LVI-SAM中的 VIS 初始化的鲁棒性，作者利用了来自 LIS 的估计系统状态 $x$ 和 IMU 偏差$b$。因为深度可以从激光雷达直接观察到，作者首先初始化 LIS 并获得 $x$ 和 $b$。然后根据图像时间戳对它们进行插值并将它们关联到每个图像关键帧。这里作者假设了IMU偏差在两个图像关键帧之间是恒定的。最后，来自 LIS 的估计$x$和$b$被用作VIS初始化的初始猜测，这显着提高了初始化速度和鲁棒性。可以在[补充视频](https://youtu.be/8CTl07D6Ibc)中找到使用和不使用LIS帮助的VIS初始化的比较。
#### 特征深度关系
![](https://notes.sjtu.edu.cn/uploads/upload_365b60d63d25865da338c8f27cad0643.png)
VIS完成初始化后，目标是使用VIS视觉里程计配准激光雷达的扫描结果。我们都知道激光雷达扫描的点云结果是稀疏的。为解决这个问题，作者将若干激光雷达帧聚合在一起，试图获得一个稠密的深度图像。作者将特征点与激光雷达获得的点云转换至同一个以相机为球心的单位球上。在该球内使用K-D tree来寻找球坐标系下距离图像特征点最近的三个激光雷达深度点，并将特征点的深度表示为特征点与球心的连线与之前找到的三个激光雷达深度点形成的平面的交点的深度。
#### 失败检测
由于剧烈运动、光照变化和无纹理环境，VIS 会出现失败情况。 当机器人进行剧烈运动或进入无纹理环境时，跟踪特征的数量会大大减少。 不足的特征可能会导致优化问题无法收敛。当 VIS 出现故障时，估计会产生很大的IMU偏差。因此，当跟踪特征的数量低于阈值或估计的 IMU 偏差超过阈值时，LVI-SAM报告VIS失败。 该系统需要主动故障检测，以便其故障不会破坏LIS的功能。 一旦检测到故障，VIS会重新初始化并通知LIS。
#### 回环检测
LVI-SAM使用DBoW2算法进行闭环检测。对每个新的关键帧，提取BRIEF描述子，并与之前的进行比较。通过DBoW2获得的候选者，将会发给LIS进行进一步验证。
### LIS
![](https://notes.sjtu.edu.cn/uploads/upload_bdc1290ed4c5cb588d1c55a86964a328.png)
激光模块作者基于自己此前的工作LIO-SAM，使用因子图进行全局位姿优化。通过IMU预积分、视觉里程计、激光雷达里程计、闭环检测四种约束来优化结果。作者对激光雷达使用了一个关键帧滑动窗来保证计算复杂度。当机器人产生较大位移时，即丢弃关键帧之间的帧。选择了新关键帧后，如图所示，则在因子图中增加一个新的机器人状态$x$节点。
#### 初始估计
在 LIS 初始化之前，作者假设机器人从零速度的静态位置开始。然后整合原始IMU测量，假设偏置和噪声为零值。两个激光雷达关键帧之间的综合平移和旋转变化产生了扫描匹配的初始猜测。作者发现当初始线速度小于 $10 m/s$ 且角速度小于 $180^{\circ}/s$ 时，这种方法可以成功初始化系统。 LIS 初始化后，我们在因子图中估计 IMU 偏差、机器人位姿和速度。然后我们将它们发送到 VIS 以帮助其初始化。
LIS 初始化后，便可以从两个来源获得初始猜测：具有校正偏差的集成 IMU 测量值和 VIS。当可用时，作者使用视觉惯性里程计作为初始猜测。如果 VIS 报告失败，系统将切换到 IMU 测量以进行初始猜测。这些程序在纹理丰富和纹理少的环境中提高了初始猜测的准确性和鲁棒性。
#### 失败检测
尽管激光雷达可以在远距离捕获环境的精细细节，但它仍然会遇到扫描匹配受到不良约束的场景。作者们采用 *“On Degeneracy of Optimization-based State Estimation Problems”* 中的方法进行 LIS失败检测。 
## 实验
作者使用自己采集的数据集进行了消融实验，其中A1：不包含LIS；A2：不包含VIS；A3：LIS与VIS都用，测试VIS中深度优化的作用；A4：包含闭环检测
![](https://notes.sjtu.edu.cn/uploads/upload_8888e04fe7c632609bd4607fa137d06f.png)
作者在Jackal dataset和Handheld dataset中对比了LVI-SAM和目前的一些SOTA方法，LVI-SAM在两个数据集上都完成得很好。
![](https://notes.sjtu.edu.cn/uploads/upload_7f9969790df1b82cd2536c338ee4488f.png)
![](https://notes.sjtu.edu.cn/uploads/upload_42d02822055f7c8ab0697b4d0b7e0b95.png)

## 参考文献
[1]: Shan T, Englot B, Ratti C, Rus D. LVI-SAM: Tightly-coupled Lidar-Visual-Inertial Odometry via Smoothing and Mapping. arXiv preprint arXiv:2104.10831. 2021 Apr 22.

[2]: Qin, Tong, Peiliang Li, and Shaojie Shen. "Vins-mono: A robust and versatile monocular visual-inertial state estimator." IEEE Transactions on Robotics 34, no. 4 (2018): 1004-1020.

[3]: Shan T, Englot B, Meyers D, Wang W, Ratti C, Rus D. Lio-sam: Tightly-coupled lidar inertial odometry via smoothing and mapping. arXiv preprint arXiv:2007.00258. 2020 Jul 1. 





---
title: "[ECCV2022] Latency-Aware Collaborative Perception"
authors:
- zixing
- Shunli Ren
- Yue Hu
- Wenjun Zhang
- Siheng Chen
date: "2022-8-10T00:00:00Z"
doi: ""

# Schedule page publish date (NOT publication's date).
publishDate: "2022-8-10T00:00:00Z"

# Publication type.
# Accepts a single type but formatted as a YAML list (for Hugo requirements).
# Enter a publication type from the CSL standard.
publication_types: ["paper-conference"]

# Publication name and optional abbreviated publication name.
publication: "ECCV 2022"
publication_short: ""

abstract:  Collaborative perception has recently shown great potential to improve perception capabilities over single-agent perception. Existing collaborative perception methods usually consider an ideal communication environment. However, in practice, the communication system inevitably suffers from latency issues, causing potential performance degra- dation and high risks in safety-critical applications, such as autonomous driving. To mitigate the effect caused by the inevitable latency, from a machine learning perspective, we present the first latency-aware collaborative perception system, which actively adapts asynchronous perceptual features from multiple agents to the same time stamp, promoting the robustness and effectiveness of collaboration. To achieve such a feature-level synchronization, we propose a novel latency compensation module, called SyncNet, which leverages feature-attention symbiotic estimation and time modulation techniques. Experiments results show that the proposed latency aware collaborative perception system with SyncNet can outperforms the state-of-the-art collaborative perception method by 15.6% in the communication latency scenario and keep collaborative per- ception being superior to single agent perception under severe latency.


# Summary. An optional shortened abstract.
summary: We present the first latency-aware collaborative perception system, which actively adapts asynchronous perceptual features from multiple agents to the same time stamp

tags: []

featured: false

# links:
# - name: ""
#   url: ""
url_pdf: 'https://www.ecva.net/papers/eccv_2022/papers_ECCV/papers/136920315.pdf'
url_code: 'https://github.com/MediaBrain-SJTU/SyncNet'
# url_dataset: ''
url_poster: 'uploads/3474.pdf'
# url_project: ''
# url_slides: ''
# url_source: ''
# url_video: ''

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
image:
  caption: 'SyncNet'
  focal_point: ""
  preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
projects: []

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
# slides: uploads/3474.pdf
---
<!-- 
{{% callout note %}}
Click the *Cite* button above to demo the feature to enable visitors to import publication metadata into their reference management software.
{{% /callout %}}

{{% callout note %}}
Create your slides in Markdown - click the *Slides* button to check out the example.
{{% /callout %}}

Add the publication's **full text** or **supplementary notes** here. You can use rich formatting such as including [code, math, and images](https://wowchemy.com/docs/content/writing-markdown-latex/). -->

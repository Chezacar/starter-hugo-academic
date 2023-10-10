---
title: "Interruption-Aware Cooperative Perception for V2X Communication-Aided Autonomous Driving"
authors:
- Runli Ren
- zixing
- Zi Wang
- Dianati Mehrdad
- Yafei Wang
- Siheng Chen
- Wenjun Zhang
date: "2023-07-07T00:00:00Z"
doi: ""

# Schedule page publish date (NOT publication's date).
publishDate: "2017-01-01T00:00:00Z"

# Publication type.
# Accepts a single type but formatted as a YAML list (for Hugo requirements).
# Enter a publication type from the CSL standard.
publication_types: ["article"]

# Publication name and optional abbreviated publication name.
publication: ""
publication_short: ""

abstract: Cooperative perception enabled by V2X Communication technologies can significantly improve the perception performance of autonomous vehicles beyond the limited perception ability of the individual vehicles, therefore, improving the safety and efficiency of autonomous driving in intelligent transportation systems. However, in order to fully reap the benefits of cooperative perception in practice, the impacts of imperfect V2X communication, i.e., communication errors and disruptions, need to be understood and effective remedies need to be developed to alleviate their adverse impacts. Motivated by this need, we propose a novel INterruption-aware robust COoperative Perception (V2X-INCOP) solution for V2X communication-aided autonomous driving, which leverages historical information to recover missing information due to interruption. To achieve comprehensive recovery, we design a communication adaptive multi-scale spatial-temporal prediction model to extract multi-scale spatial-temporal features based on V2X communication conditions and capture the most significant information for the prediction of the missing information. To further improve recovery performance, we adopt a knowledge distillation framework to give direct supervision to the prediction model and a curriculum learning strategy to stabilize the training of the model. Our experiments on three public cooperative perception datasets demonstrate that our proposed method is effective in alleviating the impacts of communication interruption on cooperative perception.

# Summary. An optional shortened abstract.
summary: We propose a novel INterruption-aware robust COoperative Perception (V2X-INCOP) solution for V2X communication-aided autonomous driving, which leverages historical information to recover missing information due to interruption.

tags:
- Source Themes
featured: false

links:
# - name: Custom Link
#   url: https://arxiv.org/pdf/2304.11821
url_pdf: https://arxiv.org/pdf/2304.11821
# url_code: '#'
# url_dataset: '#'
# url_poster: '#'
# url_project: ''
# url_slides: ''
# url_source: '#'
# url_video: '#'

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
image:
  caption: 'Overview of the interruption-aware cooperative perception (V2X-INCOP) system. '
  focal_point: ""
  preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
projects:
- internal-project

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
slides: example
---

<!-- {{% callout note %}}
Create your slides in Markdown - click the *Slides* button to check out the example.
{{% /callout %}}

Add the publication's **full text** or **supplementary notes** here. You can use rich formatting such as including [code, math, and images](https://wowchemy.com/docs/content/writing-markdown-latex/). -->

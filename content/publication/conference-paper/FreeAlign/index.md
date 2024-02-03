---
title: "[ICRA 2024] Robust Collaborative Perception without External Localization and Clock Devices"
authors:
- zixing
- Zhenyang Ni
- Ruize Han
- Shuo Tang
- Chen Feng 
- Siheng Chen
- Yanfeng Wang
date: "2024-01-29T00:00:00Z"
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

abstract: A consistent spatial-temporal coordination across multiple agents is fundamental for collaborative perception, which seeks to improve perception abilities through informa-tion exchange among agents. To achieve this spatial-temporal alignment, traditional methods depend on external devices to provide localization and clock signals. However, hardware-generated signals could be vulnerable to noise and potentially malicious attack, jeopardizing the precision of spatial-temporal alignment. Rather than relying on external hardwares, this work proposes a novel approach aligning by recognizing the inherent geometric patterns within the perceptual data of various agents. Following this spirit, we propose a robust collaborative perception system that operates independently of external localization and clock devices. The key module of our system, FreeAlign, constructs a salient object graph for each agent based on its detected boxes and uses a graph neural network to identify common subgraphs between agents, leading to accurate relative pose and time. We validate FreeAlign on both real-world and simulated datasets. The results show that, the FreeAlign empowered robust collaborative perception system perform comparably to systems relying on precise localization and clock devices. We will release code related to this work.

# Summary. An optional shortened abstract.
summary: We propose a novel INterruption-aware robust COoperative Perception (V2X-INCOP) solution for V2X communication-aided autonomous driving, which leverages historical information to recover missing information due to interruption.

tags:
- Source Themes
featured: false

links:
# - name: Custom Link
#   url: https://arxiv.org/pdf/2304.11821
url_pdf: '#'
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
  caption: 'Overview of FreeAlign'
  focal_point: ""
  preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
# projects:
# - internal-project

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
# slides: example
---


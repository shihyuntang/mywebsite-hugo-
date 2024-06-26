---
title: "IGRINS RV: A Precision RV Pipeline for IGRINS Using Modified Forward-Modeling in the Near-Infrared"
authors:
- "Asa G. Stahl"
- admin
- "Christopher M. Johns-Krull"
- "L. Prato"
- "Joe Llama"
- "Gregory N. Mace"
- "Jae Joon Lee"
- "Heeyoung Oh"
- "Jessica Luna"
- "Daniel T. Jaffe"

date: "2021-05-26T00:00:00Z"
doi: "10.3847/1538-3881/abf5e7"

# Schedule page publish date (NOT publication's date).
publishDate: "2021-02-02T00:00:00Z"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["2"]

# Publication name and optional abbreviated publication name.
publication: "The Astronomical Journal 161:283 (26pp)"
publication_short: ""

abstract: Applications of the radial velocity (RV) technique to the near infrared (NIR) are valuable for their diminished susceptibility to the impact of stellar activity and their suitability for studying late-type stars. In this paper, we present the IGRINS RV open source python pipeline for computing infrared RV measurements from reduced spectra taken with IGRINS, a R$\equiv \lambda/\Delta \lambda \sim$45,000 spectrograph with simultaneous coverage of the H band (1.49--1.80 µm) and K band (1.96--2.46 µm). Using a modified forward modeling technique, we construct high resolution telluric templates from A0 standard observations on a nightly basis to provide a source of common-path wavelength calibration while mitigating the need to mask or correct for telluric absorption. A0 standard observations are also used to model the variations in instrumental resolution across the detector, including a yearlong period when the K band was defocused. Without any additional instrument hardware, such as a gas cell or laser frequency comb, we are able to achieve precisions of 26.8 m/s in the K band and 31.1 m/s in the H band for narrow-line hosts. These precisions are validated by a monitoring campaign of two RV standard stars as well as the successful retrieval of planet-induced RV signals for both HD 189733 and $\tau$ Boo A; furthermore, our results affirm the presence of the Rossiter-McLaughlin effect for HD189733. The IGRINS RV pipeline extends another important science capability to IGRINS, with publicly available software designed for widespread use.

# Summary. An optional shortened abstract.
summary: "The Astronomical Journal 161:283 (26pp)"

tags:
- radial velocities
- IGRINS
- planets and satellites detection
featured: false

links:
- name: ADS
  url: https://ui.adsabs.harvard.edu/abs/2021AJ....161..283S/abstract
- name: AJ 161:283
  url: https://iopscience.iop.org/article/10.3847/1538-3881/abf5e7
- name: arXiv:2104.02082
  url: https://arxiv.org/abs/2104.02082

#url_pdf: http://arxiv.org/pdf/1512.04133v1
#url_code: ''
#url_dataset: ''
#url_poster: ''
#url_project: ''
#url_slides: ''
#url_source: ''
#url_video: ''

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
image:
 caption: 'Image credit: Figure 5 in Stahl et al. 2021. Final RVs for RV standard stars'
 focal_point: ""
 preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
#projects: []

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
#slides: example

#{{% alert note %}}
#Click the *Cite* button above to demo the feature to enable visitors to import publication metadata into their reference #management software.
#{{% /alert %}}

#{{% alert note %}}
#Click the *Slides* button above to demo Academic's Markdown slides feature.
#{{% /alert %}}

#Supplementary notes can be added here, including [code and math](https://sourcethemes.com/academic/docs/writing-markdown-#latex/).

---
![rv](202104_igrinsrv_aj.png)
*Image credit: Figure 5 in Stahl et al. 2021.*: Final RVs for RV standard stars
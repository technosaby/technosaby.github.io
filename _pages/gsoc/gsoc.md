---
layout : single
permalink: /gsoc/gsoc
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/images/gsoc_banner.png
title: Google Summer of Code 2022 - RedHen Labs 
author: Sabyasachi Ghosal

toc_label: "GSoc Blogs"
sidebar:
  nav: gsoc_nav
---


I am thrilled to be a part of the awesome Red Hen Lab community! Thank you for selecting me and giving me a chance to contribute to the Red Hen codebase.

This post describes my journey after being selected as a Google Summer of Code (GSoC) student associated with Red Hen Lab. I plan to summarize my progress at the end of every week until the end of the summer.

Here’s the abstract of my project:

*"The objective is to develop a machine learning model to tag sound effects in streams (like police sirens
in a news-stream) of Red Hen’s data. A single stream of data can contain multiple sound effects, so the
model should be able to label them from a group of known sound effects like a Multi-label classification
problem. The first step would be to develop a baseline model using existing pre-trained deep learning
models and add to the Red Hen’s pipeline. Then the performance can be improved using transfer learning
and fine tuning the existing model to achieve better accuracy. In this process, the models can be trained on
sound effects from noisy or human labeled data sets after they are pre-processed to avoid acoustic domain
mismatch problems."*

My mentors are Austin Bennett, Ahmed Ismail Zahran & Mark Turner.
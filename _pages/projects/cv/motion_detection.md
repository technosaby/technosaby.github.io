---
layout : single 
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/images/others_assets/cv_banner_image.jpg
title: "Motion Detection"
tagline: "Optic flow as the problem of computing a dense flow field"
description: "This project introduces optic flow as the problem of computing a dense flow field where a flow field is a vector field <u(x,y), v(x,y)>. The standard Hierarchical Lucas and Kanade will be used for computing these vectors. This assignment focusses on implementing simpler operations in order to understand more about array manipulation and the math behind them.
The learning objectives are as follows:
* Implement the Lucas-Kanade algorithm based on the concepts learned from the lectures.
* Learn how pixel movement can be seen as flow vectors.
* Create image resizing functions with interpolation.
* Implement the Hierarchical Lucas-Kanade algorithm.
* Understand the benefits of using a Pyramidal approach.
* Understand the theory of action recognition."
permalink: /projects/cv/motion_detection
classes: wide
author: Sabyasachi Ghosal
sidebar:
  nav: others_nav
---
# Project Goal
This project introduces optic flow as the problem of computing a dense flow field where a flow field is a vector field <u(x,y), v(x,y)>. The standard Hierarchical Lucas and Kanade will be used for computing these vectors. This assignment focusses on implementing simpler operations in order to understand more about array manipulation and the math behind them.

The learning objectives are as follows:
* Implement the Lucas-Kanade algorithm based on the concepts learned from the lectures.
* Learn how pixel movement can be seen as flow vectors.
* Create image resizing functions with interpolation.
* Implement the Hierarchical Lucas-Kanade algorithm.
* Understand the benefits of using a Pyramidal approach.
* Understand the theory of action recognition.

Optic flow can be used in Frame Interpolation (Szelinski 2010 Section 8.5.1). With Optic Flow principles, we are able to (or at least attempt to) create missing frames. Here, the input is given by a set of 3 images which has some missing frames.
<p float="left">
  <img src="/assets/images/others_assets/cv_fi_input_mc01.png" width="300" />
  <img src="/assets/images/others_assets/cv_fi_input_mc02.png" width="300" />
  <img src="/assets/images/others_assets/cv_fi_input_mc03.png" width="300" />  
</p>

# Solution
[Github Link](https://github.com/technosaby/portfolio-projects/tree/master/cv/ps04) 

[Please note that the link may not be accessible, please drop me a message if you want to know more]

# Output
The output with the missing frames.
<img src="/assets/images/others_assets/cv_fi_output.png" width="900" />
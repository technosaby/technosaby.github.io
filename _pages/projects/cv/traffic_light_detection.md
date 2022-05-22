---
layout : single 
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/images/others_assets/cv_banner_image.jpg
title: "Traffic Light Detection"
tagline: "Traffic Light Detection using Hogh tools and Hough algorithms"
description: "This project relates to understand the basic building blocks of image processing. Key areas that where focussed on in this project are: loading and manipulating images, producing some valued output of images, and comprehension of the structural and semantic aspects of what makes an image. In this project, Hough Transform and line finding are used to understand how traffic lights
can be identified. There are many advanced libraries now to do this task, but the main aim of the project was to understnd the working principles behind them and also to understand how each image is composed and what patterns can be used to identify objects in a scene. 

* Understand the image representation (along with color channels) in 2D,3D arrays.  
* Use Hough tools to search and find lines and circles in an image
* Use the results from the Hough algorithms to identify basic shapes.
* Understand how objects can be selected based on their pixel locations and properties.
* Address the presence of distortion / noise in an image.
* Identify what challenges real-world images present over simulated scenes."
permalink: /projects/cv/traffic_light_detection
classes: wide
author: Sabyasachi Ghosal
sidebar:
  nav: others_nav
---
# Project Goal
This project relates to understand the basic building blocks of image processing. Key areas that where focussed on in this project are: loading and manipulating images, producing some valued output of images, and comprehension of the structural and semantic aspects of what makes an image. In this project, Hough Transform and line finding are used to understand how traffic lights
can be identified. There are many advanced libraries now to do this task, but the main aim of the project was to understnd the working principles behind them and also to understand how each image is composed and what patterns can be used to identify objects in a scene. 

* Understand the image representation (along with color channels) in 2D,3D arrays.  
* Use Hough tools to search and find lines and circles in an image
* Use the results from the Hough algorithms to identify basic shapes.
* Understand how objects can be selected based on their pixel locations and properties.
* Address the presence of distortion / noise in an image.
* Identify what challenges real-world images present over simulated scenes.


# Solution
[Github Link](https://github.com/technosaby/portfolio-projects/tree/master/cv/ps02) 

[Please note that the link may not be accessible, please drop me a message if you want to know more]

# Output
To test the different traffic signals, the following images are used, where the cordinates are identified to the center of the signals. This is also tested on noisy images.
<p float="left">
  <img src="/assets/images/others_assets/cv_traffic_simple1.png" width="400" />
  <img src="/assets/images/others_assets/cv_traffic_simple2.png" width="400" /> 
  <img src="/assets/images/others_assets/cv_traffic_simple3.png" width="400" /> 
  <img src="/assets/images/others_assets/cv_traffic_simple4.png" width="400" /> 
</p>

To test in real images, following images were used. 
<p float="left">
  <img src="/assets/images/others_assets/cv_traffic_real_world1.png" width="400" />
  <img src="/assets/images/others_assets/cv_traffic_real_world2.png" width="400" /> 
</p>
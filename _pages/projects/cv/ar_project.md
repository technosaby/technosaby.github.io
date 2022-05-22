---
layout : single 
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/images/others_assets/cv_banner_image.jpg
title: "Enhanced Augmented Reality"
tagline: "To explore different techniques to insert images and video into a scene without markers"
description: "For this topic different techniques are explored to insert images and video into a scene without markers. The final algorithm must identify a clear surface in a video and project an advertisement onto that surface. The advertisement must remain in a fixed position in real-world coordinates as the camera is moved. The algorithm must also handle the case where the advertisement location temporarily moves out of the camera’s field of view.
The main task is to detect a flat surface in a scene and project an image on it without the use of predefined markers. A flat surface can be found in common large items such as walls, tables, doors, etc. As part of the process, your method must use existing features in a scene as anchor points for the projected image. Placing markers in a scene will not be accepted. Determining which these can be is part of your research and project requirements. To find interest points, you could use any of the distance transform methods.  
The projected image must behave similar to an object present in the scene. This means that your approach must be able to handle cases where part of the projected image is outside the frame boundaries while keeping the remaining part in the scene. If the camera view leaves the area where the projected image is, the projected image will not show in the current scene. However, the object must show again if the camera moves back to a view where the object should be visible. One way to address this is to track the image / camera motion using features to track and use this information to “guess” where these are outside the image frame. This approach must be tested using these cases as part of the project requirements."
permalink: /projects/cv/ar_project
classes: wide
author: Sabyasachi Ghosal
sidebar:
  nav: others_nav
---

# Project Goal
For this topic different techniques are explored to insert images and video into a scene without markers. The final algorithm must identify a clear surface in a video and project an advertisement onto that surface. The advertisement must remain in a fixed position in real-world coordinates as the camera is moved. The algorithm must also handle the case where the advertisement location temporarily moves out of the camera’s field of view.

The main task is to detect a flat surface in a scene and project an image on it without the use of predefined markers. A flat surface can be found in common large items such as walls, tables, doors, etc. As part of the process, your method must use existing features in a scene as anchor points for the projected image. Placing markers in a scene will not be accepted. Determining which these can be is part of your research and project requirements. To find interest points, you could use any of the distance transform methods.  
The projected image must behave similar to an object present in the scene. This means that your approach must be able to handle cases where part of the projected image is outside the frame boundaries while keeping the remaining part in the scene. If the camera view leaves the area where the projected image is, the projected image will not show in the current scene. However, the object must show again if the camera moves back to a view where the object should be visible. One way to address this is to track the image / camera motion using features to track and use this information to “guess” where these are outside the image frame. This approach must be tested using these cases as part of the project requirements. 

# Solution 
[Github Link](https://github.com/technosaby/portfolio-projects/tree/master/cv/er_project) 

[Please note that the link may not be accessible, please drop me a message if you want to know more]

# Output
[Output video](https://www.youtube.com/watch?v=EuCC8uv8jbM)
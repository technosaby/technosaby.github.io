---
layout : single 
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/images/code.jpg
title: "Navigating through asteroids"
tagline: "Track a collection of asteroids and estimate their future locations and pilot a craft around them to a goal location"
description: "This projects ask to track a collection of asteroids and estimate their future locations and pilot a craft around them to a goal location. On each time step, the pilot will be asked to estimate the locations of all asteroids on the next time step. The pilot’s estimates from the prior step will be compared with the asteroids’
current locations. The estimation is successful if 90% of the asteroids currently active match the prior step’s estimates. The navigation task is intended to be tackled after completing the estimation task as the navigation task will  make use of the estimation. This task initializes a craft below the asteroid field and asks you to pilot it
through the field and into a goal area above it."
permalink: /projects/air/asteroids
classes: wide
author: Sabyasachi Ghosal
sidebar:
  nav: others_nav
---

# Project Goal
This projects ask to track a collection of asteroids and estimate their future locations and pilot a craft around them to a goal location. On each time step, the pilot will be asked to estimate the locations of all asteroids on the next time step. The pilot’s estimates from the prior step will be compared with the asteroids’
current locations. The estimation is successful if 90% of the asteroids currently active match the prior step’s estimates. The navigation task is intended to be tackled after completing the estimation task as the navigation task will  make use of the estimation. This task initializes a craft below the asteroid field and asks you to pilot it
through the field and into a goal area above it. 
Each move by the craft is specified by:
* angle change: the craft may turn left, right, or go straight. Turns adjust the craft’s heading by angle_increment.
* speed change: the craft may accelerate, decelerate, or continue at its current velocity. 

# Solution 

[Github Link](https://github.com/technosaby/portfolio-projects/tree/master/ai4r/asteroids) 

[Please note that the link may not be accessible, please drop me a message if you want to know more]

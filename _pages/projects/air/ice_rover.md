---
layout : single 
permalink: /projects/air/ice_rover
title: "Ice Rover"
tagline: "Practice implementing a SLAM module and a robot control system that uses it to navigate through a world"
description: "The goal of this project is to practice implementing a SLAM module and a robot control system that uses it to navigate through a world. 
The SLAM system should be able to keep track of where the robot is located after a series of movements (using measurements to landmark beacons).
The movements and measurements will have noise. The robot will be dropped via parachute onto the ice sheet. To help it navigate, a set of solar powered beacons have also been dropped onto the ice (they are flat, and the rover can roll over them). These beacons are scattered randomly, but will melt themselves into the ice upon placement. The robot should make it’s own map of the environment, using it’s starting location as the origin, and taking advantage of the signals from the beacons to maintain a good estimate of its own position relative to the origin as it slips around on the ice. (The ice may introduce movement noise, in that the robot may not turn or move the exact distances based on the command given.) The science team has manually planted a set of special beacons (called “sites”) in specific locations which the robot must navigate to and sample. 
There is a time penalty for attempting to sample an invalid site. The robot has a maximum turning angle and distance that it can move each turn. Movement commands that exceed these values will be cause the robot to not move."
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/images/code.jpg
classes: wide  
author: Sabyasachi Ghosal
sidebar:
  nav: others_nav
---

# Project Goal
The goal of this project is to practice implementing a SLAM module and a robot control system that uses it to navigate through a world. 
The SLAM system should be able to keep track of where the robot is located after a series of movements (using measurements to landmark beacons).
The movements and measurements will have noise. The robot will be dropped via parachute onto the ice sheet. To help it navigate, a set of solar powered beacons have also been dropped onto the ice (they are flat, and the rover can roll over them). These beacons are scattered randomly, but will melt themselves into the ice upon placement. The robot should make it’s own map of the environment, using it’s starting location as the origin, and taking advantage of the signals from the beacons to maintain a good estimate of its own position relative to the origin as it slips around on the ice. (The ice may introduce movement noise, in that the robot may not turn or move the exact distances based on the command given.) The science team has manually planted a set of special beacons (called “sites”) in specific locations which the robot must navigate to and sample. 
There is a time penalty for attempting to sample an invalid site. The robot has a maximum turning angle and distance that it can move each turn. Movement commands that exceed these values will be cause the robot to not move.

# Solution
[Github Link](https://github.com/technosaby/portfolio-projects/tree/master/ai4r/ice_rover) 

[Please note that the link may not be accessible, please drop me a message if you want to know more]

---
layout : single 
title: "Mars Glider"
tagline: "Implement a particle filter which is used to localize a robotic glider that does not have access to terrestrial based GPS satellites"
description: "The goal of this project is to implement a particle filter which is used to localize a robotic glider that does not have access to terrestrial based GPS satellites. The glider is released from a spacecraft over the surface of mars, and receives a distance to ground measurement from a downward facing radar, as well as an altitude estimate from a barometric pressure sensor. The glider has an on-board map of the area it is being dropped into. The map
covers an area 10 km on a side (100 sq km), and the robot is supposed to be dropped somewhere near (0,0). The map was generated by radar from the mars surveyor satellite mission, and has a 1x1 meter resolution. Dimensions in the map range from -5,000m to 5,000m. The glider will be dropped somewhere within the mapped area hopefully near (0,0), but possibly as far off as +/- 500m in both X and Y. It will pop out of the reentry craft approximately 5,000 meters (+/- 50m) above “sea level”.
As mars has a thin atmosphere, the glide ratio is 5:1, which means that the glider moves forward 5 meters for every meter it falls. It moves 5m/sec, and falls 1m/s. This means that there is at least 900 seconds to localize the glider before it potentially goes “off-map”. There is upto 4,500 seconds of “glide time” before the glider risks hitting the surface, but this would need to steer the glider to keep it within the boundaries of the known map.
Note that the radar sensor [sense function] gives you a (noisy) distance to “ground”, and not “sea level” (on mars, “sea level” is defined as the mean ground height). The barometric sensor [get_height function] gives the gliders distance above “sea level”, modulo the (unknown to you) atmospheric offset due
to the naturally changing barometric pressure. The atmospheric offset will be static (unchanging) over the course of a single “drop”, but an estimation is necessary to localize the glider successfully."
permalink: /projects/air/mars_glider
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
The goal of this project is to implement a particle filter which is used to localize a robotic glider that does not have access to terrestrial based GPS satellites. The glider is released from a spacecraft over the surface of mars, and receives a distance to ground measurement from a downward facing radar, as well as an altitude estimate from a barometric pressure sensor. The glider has an on-board map of the area it is being dropped into. The map
covers an area 10 km on a side (100 sq km), and the robot is supposed to be dropped somewhere near (0,0). The map was generated by radar from the mars surveyor satellite mission, and has a 1x1 meter resolution. Dimensions in the map range from -5,000m to 5,000m. The glider will be dropped somewhere within the mapped area hopefully near (0,0), but possibly as far off as +/- 500m in both X and Y. It will pop out of the reentry craft approximately 5,000 meters (+/- 50m) above “sea level”.
As mars has a thin atmosphere, the glide ratio is 5:1, which means that the glider moves forward 5 meters for every meter it falls. It moves 5m/sec, and falls 1m/s. This means that there is at least 900 seconds to localize the glider before it potentially goes “off-map”. There is upto 4,500 seconds of “glide time” before the glider risks hitting the surface, but this would need to steer the glider to keep it within the boundaries of the known map.
Note that the radar sensor [sense function] gives you a (noisy) distance to “ground”, and not “sea level” (on mars, “sea level” is defined as the mean ground height). The barometric sensor [get_height function] gives the gliders distance above “sea level”, modulo the (unknown to you) atmospheric offset due
to the naturally changing barometric pressure. The atmospheric offset will be static (unchanging) over the course of a single “drop”, but an estimation is necessary to localize the glider successfully. 

# Solution
[Github Link](https://github.com/technosaby/portfolio-projects/tree/master/ai4r/marsglider) 

[Please note that the link may not be accessible, please drop me a message if you want to know more]
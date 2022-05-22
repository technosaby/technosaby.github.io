---
layout : single 
title: "Lunar Lander"
permalink: /projects/rl_projects/lunar_lander
excerpt: ""
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
For this project, an RL agent is implemented to successfully land the [Lunar Lander](!https://gym.openai.com/envs/LunarLander-v2) in OpenAI gym. The problem is an 8-dimensional state space, with six continuous state variables and two discrete ones. The action space is discrete. The four discrete actions available are: do nothing, fire the left orientation engine, re the main engine, re the right orientation engine. The landing pad is always at coordinates (0,0). Coordinates consist of the rst two numbers in the state vector. The base reward for moving from the top of the screen to the landing pad depends on a number of factors. If the lander moves away from the landing pad it is penalized the amount of reward that would be gained by moving towards the pad. An episode nishes if the lander crashes or comes to rest, receiving an additional -100 or +100 points, respectively, on top of the base reward. Each leg-ground contact is worth +10 points. Firing the main engine incurs a -0.3 point penalty and firing the orientation engines incur a -0.03 point penalty, for each occurrence. Landing outside of the landing pad is possible. Fuel is infinite, so, an agent could learn to fly and land on its rst attempt. The problem is considered solved when achieving a score of 200 points or higher on average over 100 consecutive
runs. 

# Solution
[Github](https://github.com/technosaby/portfolio-projects/rl/lunar-lander)

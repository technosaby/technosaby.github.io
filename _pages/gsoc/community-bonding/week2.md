---
layout : single 
title: Week 2 (May 29 - June 4) 
permalink: /gsoc/community-bonding/week2
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/images/code.jpg
author: Sabyasachi Ghosal
sidebar:
  nav: gsoc_nav
---

This is the second week of the program and we are in the community bonding phase.

## Redhen Infrastructure Set Up
Prof. Mark Turner from RedHen team reached out to us to have the necessary infrastructure set up. I am summarizing them below.

1. Accounts were created in case.edu domain.
2. An orientation for using CWRU HPC were [shared](https://sites.google.com/case.edu/techne-public-site/cwru-hpc-orientation) with us. 
3. VPN was [set up](https://sites.google.com/case.edu/techne-public-site/cwru-hpc-orientation/access-cwru-hpc-via-vpn) to login to the case servers remotely. 
4. Once VPN is set up, we can ssh to your HPC using the command, where abc123 represents a dummy user id.
  - ssh abc123@rider.case.edu 
5. “gallina” is a Red Hen Lab file server mounted on CWRU HPC. In the HPC, the gallina home has been set up to /mnt/rds/redhen/gallina/home/abc123. This should serve as a home directory and all work related files (with significant size) should be kept here, not in the home directory.
6. Once the account is created, we had set up the permissions and symbolic link for work. 
7. There is a chance of of losing your work when a connection to CWRU HPC drops, so RedHen recommended us to work in Linux screen to solve this problem. A [tutorial](https://linuxize.com/post/how-to-use-linux-screen/) has been shared with the commands required for day to day use. 
Some of the standard screen control-a commands are:
	- Ctrl+a c Create a new window (with shell)
	- Ctrl+a " List all windows
	- Ctrl+a 0 Switch to window 0 (by number )
	- Ctrl+a A Rename the current window
	- Ctrl+a S Split current region horizontally into two regions
	- Ctrl+a | Split current region vertically into two regions
	- Ctl+a tab Switch the input focus to the next region
	- Ctrl+a Ctrl+a Toggle between the current and previous region
	- Ctrl+a Q Close all regions but the current one
	- Ctrl+a X Close the current region
8. Also we have set up the RSA key to access the servers. 

## Contributor Summit
Google Summer of Code has also set up a [Contributor Summit](https://www.youtube.com/watch?v=HnQBMwR-RuY%C2%A0). It was great to hear from lot of experienced Googlers as well as previous GSoc members and contributors. 

But the 3 common advice given by every one are
- Do your research
- Reach outside of your comfort zone
- Communicate with mentors

Other good advices were
- Stay connected even after the program is over
- Get associated with the organization more deeply
- Try to contribute in the organization more (by writhing documentation, improve process)

I also came to know about [Google Developer Groups](https://gdg.community.dev/) which connects local developers working with new skills and technologies. They conduct seminar throughout the year which can be attended virtually as well as in-person.

In the upcoming week, I plan to do the following
- Establish a communication with my mentor
- Review the existing proposal with my mentor
- Complete existing [set up](https://sites.google.com/case.edu/techne-public-site/home) in RedHen infrastructure.

---
layout : single 
title: Week 4 (June 13 - June 18) 
permalink: /gsoc/phase1/week4
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/images/code.jpg
author: Sabyasachi Ghosal
sidebar:
  nav: gsoc_nav
---

## Ambitions
- Creation of Audio Files from Redhen Video files
- Run Yamnet on one RedHen video to extract the classes labelled for the audio effects
- Execute the baseline code in CWR HPC servers 

## Challenges
- Redhen does not have an existing pipeline to extract the audio. So for now, I am writting a script to do that myself. (This has been done locally). A generic pipeline to reuse for all RedHen projects can be done (but out of scope for my work). This can be taken after the work is completed.
- Deciding output format is one challenge. Currently I am dumping the data (scores & labels) in the CSV format. 

## Strategies
- Handling the tasks & milestones through Github project is going on good for now. All issues and discussions are being handled there.
- All the discussions with the mentors are also handled in the Github project. 
- Prof Urhig also suggested to write the output in the format of ELAN EAF files. Prof Turner suggested to create a file with .sgx extension and generate data in Red Hen format. These options should to be weighed in the M2 milestone after the integration with the Redhen infrastructure. 

## Setbacks
- All this work has been done locally. I need to set up the docker and singularity container to make this happen. This will be taken in the next week.
- All the work for generation of output files is also not completed. It is important to decide how to parse the output. 

## Details/Successes 
- Set up the Github Project (as suggested by mentor Austin)
- Was able to write a script to extract the audio files from the videos
- Dumped the audio tags in a csv format
- Discussion was done with mentors in slack/github project

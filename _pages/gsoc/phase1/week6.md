---
layout : single 
title: Week 6 (June 26 - July 2) 
permalink: /gsoc/phase1/week6
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/images/code.jpg
author: Sabyasachi Ghosal
sidebar:
  nav: gsoc_nav
---

## Ambitions
1. Do a baslining with YaMNet
2. Generate a RedHen output metadata file

## Challenges
Finalising the metatdata format is a critical part because these metadata is the only way how the future RedHen's will use the output  

## Details & Successes
In this week, I worked on the following
1. Created a pipeline with the YaMNet model and run some RedHen Videos.  
2. Created a metatdata file (.sfx) format based on the output of the model. 
  The generated template contains the following
  - Header: Red Block, Copied from seg files of the video
  - Legend: Blue Block, Describing about the owner of this file
  - Body: Green Block showing one frame, where all the audio tags are mapped corresponding to time frame 
 ![metadata_structure](/assets/images/gsoc/metadata_structure.png "Metatdata Structure")

 Also we had a discussion and review about the progress. Prof Turner suggested the next set of events
 - Create a bash script to filter the tags based on timeframes
 - Use the generated Metadata in ELAN
 - Prepare a codebook explanation about the structure of the generated output


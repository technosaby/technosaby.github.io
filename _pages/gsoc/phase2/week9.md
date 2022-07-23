---
layout : single 
title: Week 9
permalink: /gsoc/phase2/week9
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/images/code.jpg
author: Sabyasachi Ghosal
sidebar:
  nav: gsoc_nav
---

## Ambitions
1. Finalise the query using JQ
2. Fixing review comments of mentors (like generating TOP for files not having .seg, etc)

## Details
1. Worked on the codebook. Wrote a script which will take the file with the YaMNet class mapping and generate 
 a codebook file. In the process, it also does some formatting ( like removing the ',' between tags and replacing them with '|', 
 string formatting, etc)
2. Modify the ssfx script to generate TOP part when .seg files are not present. 

3. Generate a script to filter tags based on JQ query.  
  ```python ssfx.py "../samples/" 2022-01-01 2022-11-01 "(.Music // .Song), (.Television // .Radio)" 1```
  
This will take the sfx file(s) from the "samples" folder (which are generated from the tagging script) and filters 
between the dates "2022-01-01" and "2022-11-01" and then filters the scores based on the query for each frame of data.
The output will contain the timestamp where the tag is found and the scores for all the tags at that timestamp.
The tags which are present in the SFX file and should be used for filtering are given in the code book

[JQ](https://stedolan.github.io/jq/) has been used to generate the query for the tags. Some examples to make the queries 
are given below. These are standard JQ query formats.
- ```"(.Music // .Song)"```
  Filter the frames which contain tag with (Music or Radio) 
- ```".Song, .Radio"```
  Filter the frames which contain tags with Song and Radio
- ```"(.Music // .Song), (.Television // .Radio)"```
  Filter the frames which contain tag with (Music or Radio) and (Television or Radio)


I am planning to have a review of the work with the mentors and go to the next step.
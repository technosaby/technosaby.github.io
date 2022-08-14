---
layout : single 
title: Week 12 
permalink: /gsoc/phase2/week12
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/images/code.jpg
author: Sabyasachi Ghosal
sidebar:
  nav: gsoc_nav
---

## Ambitions
- Update the tag annotation in the ELAN TOOL.
- Review with mentors and decide the next course of actions

## Ideas
I found an option in the ELAN tool which can import a CSV file. So I decided to use this approach to export the tags in a CSV file and import the annotations in ELAN tool.

## Details
ELAN is a tool used by the research community to make and view annotations. So if we can add the audio tag annotations in the ELAN tool, then it will benefir the research community more as all the annotations will be on one place.
1. I generated the tags in a [CSV](https://github.com/technosaby/gsoc2022/blob/main/tagging_audio_effects/samples/2022-07-10_PresidentXiJinping-Why_I_proposed_the_Belt_and_Road-hNKTbMx8PFk.csv) file (similar to SFX file). 
2. Then I imported the EAF file, MP4 file and the generated CSV file in the ELAN tool, the tag annotations can be seen in the [ELAN](../../../assets/images/gsoc/elan_tag_mp4_sample.png). 
3. After discussion with Mark and Austin, I did a little modification, such that the Audio tags are set as tiers and the tagged frames are plotted as annotations in the ELAN tool. So the CSV is generated like this.
![csv_file](/assets/images/gsoc/csv_settings.png "CSV Settings")
Then the CSV file with the plotted data is imported in ELAN with the following settings. 
![elan_file](/assets/images/gsoc/elan_settings_import.png "ELAN Settings")

After ELAN processes the data, the Audio Tags are show like this. 
![elan_output_initial](/assets/images/gsoc/elan_output_initial.png "ELAN Output")

4. We can also format the ELAN output such that continuous tags can be plotted together. This will be taken in the next week. 


## Setbacks
When I imported an MKV file in the ELAN, the annotations appear but the video does not get loaded with the following [error](../../../assets/images/gsoc/error_elan_mkv.png) 

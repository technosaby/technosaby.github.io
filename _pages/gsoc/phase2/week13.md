---
layout : single 
title: Week 13 
permalink: /gsoc/phase2/week13
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/images/code.jpg
author: Sabyasachi Ghosal
sidebar:
  nav: gsoc_nav
---

## Ambitions
1. Finalize the project deliverables 
2. Review with mentors
3. Finalize the singularity pipleine


## Details
I have added a feature to filter the  tagging before updating the CSVs files with scores specified by the user. If the user only wants to see the tags above .30 score, he/she can specify the score while calling the tagging script with the -c argument. 

```python tag_audio_effects.py -i <audio input path> -o <output data path (default: .)> -f <output file type (CSV) -c <csv_filter_score>  -l <logs enabled (default 0) >```

If this value is passed while generating the SFX file, then this parameter has no action.

Once that is done the generated CSV file will only contain scores above 0.30. When the CSV file is imported in ELAN, it will be something like this, 

![elan_csv_filter_file](/assets/images/gsoc/csv_score_filter.png "ELAN CSV Filter")

## Final Week Ambitions
1. Finalize the Singularity Container. 
2. Final review with mentors for GSoc.
3. Run the tagger on files specified by the mentors. 
3. Start working for a paper to be submitted on our work in GSoc.
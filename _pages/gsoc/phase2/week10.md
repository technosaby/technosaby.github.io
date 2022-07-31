---
layout : single 
title: Week 10 
permalink: /gsoc/phase2/week10
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/images/code.jpg
author: Sabyasachi Ghosal
sidebar:
  nav: gsoc_nav
---

## Ambitions
1. Make some small changes in the ReadMe and scripts as suggested in review
2. Package the code in singularity container and run in HPC


## Details
To prepare the singularity container I followed those steps

1. Create /scratch/users/$USER folder and clone the repo from here. 
2. Load the singularity 
```module load singularity/3.8.1```
3. Create Singularity sif file from docker container. To do this, go to /scratch/users/$USER folder and then run 
  ```singularity pull image.sif docker://ghcr.io/technosaby/gsoc2022-redhen-audio-tagging-stages:1```

4. Now execute the following command using the singularity exec command
```singularity exec --bind /scratch/users/sxg1263/ image.sif python3 /scratch/users/sxg1263/gsoc2022/tagging_audio_effects/tools/audio_file_convertor.py -i /mnt/rds/redhen/gallina/tv/2022/2022-01/2022-01-01/ - /scratch/users/sxg1263/Output/AudioFiles/ -l 1" ```

As a start I wanted to convert all the video files for 2022-01-01 to audio files. Ideally the script should generate all audio files for the video files present in the date folder(2022-01-01) and put it inside the AudioFiles folder in Output of the scratch. But the output looks like this below and no files got generated. I only get this warning and no error.

"WARNING: While bind mounting '/scratch/users/sxg1263:/scratch/users/sxg1263/': destination is already in the mount point list
Starting generation of audio files from  /mnt/rds/redhen/gallina/tv/2022/2022-01/2022-01-01/  to  wav with format."

5. When the same command is run in my local LINUX PC using singularity sif file (created in the same way as above), it works fine and the audio files get generated correctly.

## Setbacks
This week's progress was very slow. Though I managed to prepare the container, I still struggled to run it correctly in the HPC. I am facing a wierd problem. When I run the command to access the video files from /mnt/rds/redhen/tv/ it does not work, but if I copy the video files to my scratch folder and run the singularity exec command, it runs fine. 

As suggested by my mentor Ahmad, I tried running this on GPU using srun, but I faced the same problem.

## Next Steps
1. Fix the singularity problem. For now I am planning to copy the video files (for one month) in the scratch folder and run the scripts to finish the workflow
2. FInd if there are other pre-trained models like YaMNet and how they perform
3. Prepare about transfer learning -> (Discuss with Austin about strategies?)
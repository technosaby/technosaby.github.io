---
layout : single 
title: Week 14 
permalink: /gsoc/phase2/week14
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/images/code.jpg
author: Sabyasachi Ghosal
sidebar:
  nav: gsoc_nav
---

## Ambitions
1. Do more testing with more videos
2. Fix existing bugs
3. Check and finalize script on Singularity 

## Details
As we are entering into the last phase of the project, all the deliverables are ready. I have the scripts ready which can be run on a local as well as in HPC.

The following steps summarizes the execution of the Audio Tagger in HPC. 

1. Create a folder name with videos required for tagging or use an existing folder from RedHen's mount point. Store it in a variable VIDEO_FILES. 
```VIDEO_FILES=/mnt/rds/redhen/gallina/tv/2022/2022-01/2022-01-01/``` 
If you are planning to create in the tags in SFX file, please ensure that you have the .seg files for your videos.

2. Please clone the repo in RedHen's HPC as a scratch user in the home of the scratch user (e.g: /scratch/users/sxg1263/). After cloning you will have 
a gsoc2022 folder.

3. Set all the variables as below
   ```
    SCRATCH_USER=/scratch/users/$USER
    TOOLS_FOLDER=$SCRATCH_USER/gsoc2022/tagging_audio_effects/tools
    ROOT_FOLDER=$SCRATCH_USER/gsoc2022/tagging_audio_effects
    HOME_FOLDER=$SCRATCH_USER/gsoc2022
   ```
4. Load the singularity container.  
  ```module load singularity/3.8.1```

5. In the scratch workspace, (e.g: /scratch/users/sxg1263/) create the singularity image from Github workspace.
   ```singularity pull image.sif docker://ghcr.io/technosaby/gsoc2022-redhen-audio-tagging-stages:1```

6. Create temporary folders for Outputs. The AudioFiles folder will contain the converted audio files while the TaggedAudioFiles contain the tagged files.
   ```
   mkdir Output/
   cd Output || exit
   mkdir AudioFiles
   mkdir TaggedAudioFiles
   ```

7. Execute the following command to convert the video (from $VIDEO_FILES) to audio file im the wav format (in Output/AudioFiles).   
```singularity exec --bind $SCRATCH_USER $SCRATCH_USER/image.sif python3 $TOOLS_FOLDER/audio_file_convertor.py -i $VIDEO_FILES -a "wav" -o $SCRATCH_USER/Output/AudioFiles/ ```

8. Execute the following command to use the Audio Files generated from the last step to generate the Audio Tags in CSV (with confidence >= 0.2) and SFX format. The tags will be generated in TaggedAudioFiles folder.
```singularity exec --bind $SCRATCH_USER $SCRATCH_USER/image.sif python3 $ROOT_FOLDER/tag_audio_effects.py -i $SCRATCH_USER/Output/AudioFiles/ -o $SCRATCH_USER/Output/TaggedAudioFiles/ -s 0.2```

9. After the script is run, an TaggedAudioFiles folders will be generated with the tagged audio files.

10.  You can now choose to copy the tagged files to your HPC home/PC for analysis using ELAN or JQ.

Some of the result samples for the videos in the RedHen video database are present [here](https://github.com/technosaby/gsoc2022/tree/main/tagging_audio_effects/samples)

When a CSV file (e.g 2022-07-10_PresidentXiJinping-Why_I_proposed_the_Belt_and_Road-hNKTbMx8PFk.mkv) is imported in ELAN tool, some of the sample results are given below.
- Start of speech in video at 00:00:22 which is detected by YamNet at a confidence of 0.82

![elan_csv_filter_sample](/assets/images/gsoc/sample_elan_xingping_1.png "ELAN Sample 1")

- Detection of silence when there is no audio in the video from 00:00:03 - 00:00:06 

![elan_csv_filter_sample](/assets/images/gsoc/sample_elan_xingping_2.png "ELAN Sample 2")
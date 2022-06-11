---
layout : single 
title: Week 3 (June 5 - June 12) 
permalink: /gsoc/community-bonding/week3
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/images/code.jpg
author: Sabyasachi Ghosal
sidebar:
  nav: gsoc_nav
---

This week I am setting up the singularity container by following this [link](https://sites.google.com/case.edu/techne-public-site/singularity). A great reference about singularity is also found from Yunfei's [blog](https://blog.yunfeizhao.com/2021/05/30/GSOC1-singularity/) who was also a RedHen contributer in GSoc 2021. 

## Ambitions
- Discuss the use cases and goals
- Discuss scope of project with mentors
- Set up a communication channel (async)
- Discuss timelines and expectations 

## Ideas
- Use slack (or something ?) for communication with students/past students/mentors ?

## Challenges
- Faced small issues in setting up the docker with Github actions. Fixed it with setting the submodules as recursive 
- Singularity container does not direct me to the gallina home, rather diverts me to /tmp. Need to check this issue.

## Achievements
- Successful in running the docker through github actions.
- Also able to access singularity file in the case hpc.
- Also updated the Techne Public Site with the fixes which I did for the Github workflow.
- In this week we had a Meet and Greet session with all the RedHens where we got introduced to all contributors and mentors. 
- Have set up a slack channel where all the RedHens can discuss about issues like setting up infrastructure etc.
- Prof Urgig discussed about differents tips to handle Gallina (discussed in the Tips sections) 
- Prof Turner discussed that the end product of project should be a working pipeline delivered in a singularity container.

## Tips
### Working with Singularity
1. Singularity containers should not be kept inside the 'safe' directory, rather it should be inside the gallina home but not inside the safe folder. This is because we dont want to back up the singularity container. 
2. All the repository code should be committed in Github and what ever is in Github does not need to be in the "safe" directory.
3. The mount points are not available in the nodes. So you should always get a node with GPU using the "srun" command (as mentioned in the Techne Public Site). This command will give me a v100 GPU for 1 day with 5Gb of RAM.
```srun -p gpu -C gpu2v100 --gres=gpu:1 -n 1 -c 2 --time=1:00:00 --mem=5gb --pty /bin/bash```
  ![singularity](/assets/images/gsoc/gsoc_singularity_setup.png "Singularity")
4. When a GPU is allocated, you can see the GPU node details using 'nvidia-smi' command
5. Also, it will navigate to /tmp and there we will not have access to gallina-home. So, at the start of the script, the data needs to be copied to the scratch folder (using scp). The scratch is a temporary folder which gets deleted automatically later on. You can refer to the [Techne Public Site reference](https://sites.google.com/case.edu/techne-public-site/storing-files-on-cwru-hpc-and-gallina?authuser=0).
```scp hpc4:/mnt/rds/redhen/gallina/home/sxg1263/somefile.txt /scratch/sxg1263```
6. After your code is run, copy the results in your home directory. You can also clean up the copied file from the "scratch" at the end of the script.
7. Use a standard docker container for the singularity and then install the packages in the docker. We should not install packages in the hpc or request installation for new packages to CSU.


## Setbacks
- Could not start with the project yet as me and mentors could not find a suitable time to meet
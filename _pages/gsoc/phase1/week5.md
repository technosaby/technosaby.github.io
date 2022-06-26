---
layout : single 
title: Week 5 (June 19 - June 25) 
permalink: /gsoc/phase1/week5
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/images/code.jpg
author: Sabyasachi Ghosal
sidebar:
  nav: gsoc_nav
---

## Ambitions
1. Study about Singularity and Docker environment 
2. Create Github workflows and modify docker file to download the docker hub in local environment  
3. Prepare singularity containers in local environment. 
4. Generate audio files from video files using the singularity

## Challenges
In the first step, I was trying to set up the docker image in the CWR HPC cluster itself. But there was a problem in submitting the SLURM jobs from gallinahome. So Prof Uhrig suggested to create the Singularity containers on our personal Linux machines (physical or virtual).  

So to create the singularity container, we first have to create a docker image. The idea is to set up a docker image locally and push it in docker

## Details
In this week I tried to set up the docker container for setting up the project infrastructure.

### Installation & Account Creation
I installed singularity to use it later. I will try to create the singularity container in local and import it in the HPC itself. 

#### Singularity 
I followed the installation process as mentioned in the [Singularity Website](https://docs.sylabs.io/guides/3.6/admin-guide/admin_quickstart.html#installation-from-source). 
    
I first installed the dependencies. 
```sudo apt-get update && sudo apt-get install -y \
  build-essential \
  uuid-dev \
  libgpgme-dev \
  squashfs-tools \
  libseccomp-dev \
  wget \
  pkg-config \
  git \
  cryptsetup-bin```

Then I installed Go version 1.16.6.
```
export VERSION=1.16.6 OS=linux ARCH=amd64  
wget -O /tmp/go${VERSION}.${OS}-${ARCH}.tar.gz https://dl.google.com/go/go${VERSION}.${OS}-${ARCH}.tar.gz && \
sudo tar -C /usr/local -xzf /tmp/go${VERSION}.${OS}-${ARCH}.tar.gz
echo 'export GOPATH=${HOME}/go' >> ~/.bashrc && \
echo 'export PATH=/usr/local/go/bin:${PATH}:${GOPATH}/bin' >> ~/.bashrc && \
source ~/.bashrc
```
Then I downloaded and installed Singularity from a Github release

```
export VERSION=3.8.1 && wget https://github.com/sylabs/singularity/releases/download/v${VERSION}/singularity-ce-${VERSION}.tar.gz && \
tar -xzf singularity-ce-${VERSION}.tar.gz && \
cd singularity

./mconfig && \
make -C ./builddir && \
sudo make -C ./builddir install
```

To test that the singularity is working fine. I built a container in the Sylabs Container Library.

```sudo /usr/local/singularity/3.8.1/bin/singularity build --sandbox niftynet niftynet.img```

#### Docker & Docker Compose
I installed the docker version 20.10.12. 
I faced some issues while installing the latest version of docker-compose. This [stack overflow link](https://stackoverflow.com/questions/58747879/docker-compose-usr-local-bin-docker-compose-line-1-not-command-not-found) helped me out. I used the following command
```
sudo curl -L "https://github.com/docker/compose/releases/download/$(curl https://github.com/docker/compose/releases | grep -m1 '<a href="/docker/compose/releases/download/' | grep -o 'v[0-9:].[0-9].[0-9]')/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose
```
### Setting up github workflow and docker
I fixed the [Github workflow](https://github.com/technosaby/gsoc2022/blob/0bc7d1af6f5769fc6c063cf24f34c6d4719ceb53/.github/workflows/docker-publish.yml) and [Dockerfile](https://github.com/technosaby/gsoc2022/blob/0bc7d1af6f5769fc6c063cf24f34c6d4719ceb53/Dockerfile) in my repo such that I can create the docker using the workflow. I also wrote a [docker-compose](https://github.com/technosaby/gsoc2022/blob/0bc7d1af6f5769fc6c063cf24f34c6d4719ceb53/docker-compose.yml) file.

### Setting up Local Docker Image
Once the workflows are set up, I cloned the repo and try to build the docker using the command
```docker-compose up  ```
Now the docker image will be build locally.

Once this is done, we can check the docker image using command 
``` sudo docker images ```
![docker_images](/assets/images/gsoc/docker_images.png "Docker Images")

Here the "technosaby/gsoc2022-redhen-audio-tagging" image is tagged as "latest" which will be used.

### Testing the docker image
To test the created docker image, we can give the following command
```sudo docker run -it --rm -p 8888:8888 -v $PWD:/TaggingAudioEffects technosaby/gsoc2022-redhen-audio-tagging ```

![docker_launch](/assets/images/gsoc/docker_launch.png "Docker Launch")
As I did not have GPU in my local system, so I did not use (--gpus all) flags
 

### Build a local singularity sandbox from docker container

```sudo /usr/local/bin/singularity build --sandbox singularity_container technosaby/gsoc2022-redhen-audio-tagging```

### Copy the sandbox to the HPC
We can do this by SCP
```scp -r singularity_container/ sxg1263@rider.case.edu:/home/sxg1263/sxg1263gallinahome```

### Running the container in HPC

After loading the singularity using the command,
```module load singularity/3.8.1```
we can run the container using,

``` singularity shell -w /home/sxg1263/sxg1263gallinahome/singularity_container```

## Setbacks
1. I have done the set up of docker but I could not finish the work for running my script for conversion of the audio files
2. I also spent a lot of time learning about docker and singularity which impacted my ambitions. 
3. I also need to convert the docker image in SIF in HPC which will be taken care in the next week.

## Strategies

I created a free docker hub and created repository with name "gsoc2022-redhen-audio-tagging" on my username "technosaby".
After creating the local docker container, we could also push it to docker hub
The command for that is
```docker push technosaby/gsoc2022-redhen-audio-tagging```
This will push all the local docker changes in the docker hub.

![docker_hub](/assets/images/gsoc/docker_hub_snap.png "Docker Hub Update ")

After that we can clone the docker hub image in the HPC
As the docker image is ready in the dockerhub, we can pull the image in the HPC using the following command. 

```docker pull technosaby/gsoc2022-redhen-audio-tagging```

Then we can convert Docker image to SIFs and also run in HPC. 

But this has some challenges. Docker hub has restrictions on free license of size of the docker. So, I will be following the approach of creating the container locally and copying to HPC

## Tips
SLURM will by default write logs to the directory from which the job was submitted. This is the current working directory from where I am running "srun" or "sbatch". 
So we have to make sure that we always run "srun" or "sbatch" while in home directory or a subdirectory thereof. Something like ~/logs (in the home directory) can be good place to run it from.
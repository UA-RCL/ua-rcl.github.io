---
title: FPGA'23 Tutorial
---

# **Work in Progress**

# CEDR: A Holistic Software and Hardware Design Environment for FPGA-Integrated Heterogeneous Systems

## Linux, Windows, and Mac

Install Docker based on the host machine platform using the link below: 
[https://docs.docker.com/engine/install/#desktop](https://docs.docker.com/engine/install/#desktop) 

Pull the existing latest Docker container with all dependencies installed: 
[https://hub.docker.com/r/mackncheesiest/cedr_dev/tags](https://hub.docker.com/r/mackncheesiest/cedr_dev/tags)

## Windows-based example: 

Open a terminal and run the docker image using the following command: 

`docker run -it --rm -v <working-directory>:/root/repository mackncheesiest/cedr_dev:latest /bin/bash`

Set <working-directory> as any folder in the host machine, all files will be stored here. 

You can use this method to re-connect to the docker container after you exit. 

Clone CEDR from GitHub using one of the following methods: 

Clone with ssh: 

`git clone git@github.com:UA-RCL/CEDR.git`

Clone with https: 

`git clone https://github.com/UA-RCL/CEDR.git`

## Linux Specific (Requires root access) 

Install git using the following command: 

`sudo apt-get install git-all`

Clone CEDR from GitHub using one of the following methods: 

Clone with ssh: 

`git clone git@github.com:UA-RCL/CEDR.git`

Clone with https: 

`git clone https://github.com/UA-RCL/CEDR.git`

Change your working directory to the cloned CEDR folder 

`cd CEDR`

## Docker Image Path: 

Install Docker using the following command: 

`sudo apt install docker.io`

Build the Docker image: 

`docker build --tag cedr_dev:latest .`

Run the Docker image: 

`docker run -it --rm -v $(pwd):/root/repository cedr_dev:latest /bin/bash`

## Without Using Docker Image: 

Install all the required dependencies using the following command (this will take some time): 

`sudo bash install_dependencies.sh`
## FROM Command ###
From Command is the one of the most fundamental command in docker which is used to specify the baseimage for image creation.
FROM is going to be the first instruction in your Dockerfile
When you run a Docker container,  you start with the base image that contain minimal operating system and some essential tools.
FROM command allow you to specify which base image to use for your image.
Base image is a starting point of an image then you can build by adding more layers.
*EX: FROM baseimage:tag*
Here tag is optional whcih specify the version of operating system.
*LKE: FROM ubuntu:20.04*

#### RUN Command ##########

RUN command is a Docker instruction which is used to execcute the commands inside the docker container during the image build process,
When you run the docker build command Docker execute all the run instruction in the Dockerfile , creating a new layer in the image.
such as installing packages updating software and running Script etc.
EX: Following RUN command install the curl packages inside the container
*"RUN apt-get update && apt-get install -y curl"*
This command uses the apt-get package manager to update the container's package index and install the curl package.


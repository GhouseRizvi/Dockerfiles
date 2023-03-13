#### Interview Questioins and answers ####
1. What is the difference between Virtualization and Containerization? 
Resource optimization is the main difference, Guest OS can block all the resources allocated it but containers dont block the resources. Apart from this provisioning/boot up time is very less in containers as they are very less size compared to VM. Scalability, high availability are achieved easily. Containers are immutable in nature they work same across all environment. basically build once and run anywhere. Performance is improved as containers can communicate with physical hardware directly where as in virtualization there is a hypervisor layer.

2. How to do the port mapping to the container?
We will docker -p [host-port]:[container-port] option

3. How can you get the shell access of running container?
We need to issue docker exec -it [container-ID] bash command to get inside of the container.
EX: docker exec -it nginx bash

4. What is the difference between RUN and CMD?
RUN is the instruction executes at the time of image creation, 
CMD is the instruction executes at the time of Container creation. 
CMD commands keeps the container running.
RUN is used to install packages, configure something at the time of image creation.

5. What is Dockerfile?
Dockerfile is the declarative way of creating our own images. We need to use Dockerfile instructions to create the image.

6. How do you build Docker image?
We need to use docker build -t [REPO-URL]/[USERNAME]/[IMAGE-NAME]:version . 
We should have Dockerfile available in the directory where we run docker build command

7. What is the difference between ADD vs COPY?
ADD and COPY does the same, copying the files from local to container. But ADD has some extra capabilities.
1. ADD can download the resources from internet to Container.
2. ADD can directly direct unzip the file into container if it is recognized format
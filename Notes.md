## FROM Command ###
From Command is the one of the most fundamental command in docker which is used to specify the baseimage for image creation.
FROM is going to be the first instruction in your Dockerfile
When you run a Docker container,  you start with the base image that contain minimal operating system and some essential tools.
FROM command allow you to specify which base image to use for your image.
Base image is a starting point of an image then you can build by adding more layers.
*EX: FROM baseimage:tag*
Here tag is optional whcih specify the version of operating system.
*LKE: FROM ubuntu:20.04*

Below are the few examples for FROM instruction in Docker.
1. FROM python:3.9-slim: This command specifies that the base image for the Dockerfile should be the official Python 3.9 slim image from Docker Hub. This image contains a minimal Python environment without any unnecessary dependencies.

2. FROM node:14-alpine: This command specifies that the base image for the Dockerfile should be the official Node.js 14 Alpine image from Docker Hub. This image is based on Alpine Linux and contains a minimal Node.js environment.

3. FROM nginx:latest: This command specifies that the base image for the Dockerfile should be the official Nginx image from Docker Hub. This image contains the Nginx web server and can be used as a base for serving static websites or as a reverse proxy for other web services.

4. FROM ubuntu:latest: This command specifies that the base image for the Dockerfile should be the official Ubuntu Linux image from Docker Hub. This image contains a full Ubuntu Linux environment and can be used as a base for a wide variety of applications.

5. FROM openjdk:11-jre-slim: This command specifies that the base image for the Dockerfile should be the official OpenJDK 11 JRE slim image from Docker Hub. This image contains a minimal Java environment without any unnecessary dependencies and can be used as a base for Java applications.

#### RUN Command ##########

RUN command is a Docker instruction which is used to execcute the commands inside the docker container during the image build process,
When you run the docker build command Docker execute all the run instruction in the Dockerfile , creating a new layer in the image.
such as installing packages updating software and running Script etc.
EX: Following RUN command install the curl packages inside the container
*"RUN apt-get update && apt-get install -y curl"*
This command uses the apt-get package manager to update the container's package index and install the curl package.

Below are the few exmples for RUN instruction in Docker:
1. RUN apt-get update && apt-get install -y package1 package2: This command updates the package index of the container's package manager and then installs the packages package1 and package2.
2. RUN mkdir /app: This command creates a new directory named app in the root of the container's file system.
3. RUN useradd -ms /bin/bash newuser: This command creates a new user named newuser with the home directory set to /home/newuser.
4. RUN curl -sSL https://get.rvm.io | bash -s stable: This command downloads and installs the Ruby Version Manager (RVM) using the curl command.
5. RUN pip install --upgrade pip && pip install -r requirements.txt: This command upgrades the pip package manager and then installs the dependencies listed in the requirements.txt file.


##### CMD ############
CMD instruction is used to set in Docker file to run the default instruction when the container is launched.
CMD instructions takes two forms CMD["Command","parameter1","parameter2"] OR CMD command parameter1 parameter2
For EX CMD["npm","start"] should start the npm start command at the time of container execution.
if a Dockerfilecontains more that one CMD commands only the last one get exxecuted at the time when the container is launched.
CMD instruction is not executed during the image creation but when the  container is launched.

Below are the few CMD Examples:
1. CMD ["npm", "start"]: This command runs the npm start command when the container starts, assuming that the image has the necessary dependencies to run a Node.js application.
2. CMD ["python", "app.py"]: This command runs the python app.py command when the container starts, assuming that the image has the necessary dependencies to run a Python application.
3. CMD ["sh", "-c", "echo Hello, World!"]: This command runs the shell command echo Hello, World! when the container starts.
4. CMD ["tail", "-f", "/var/log/app.log"]: This command runs the tail -f /var/log/app.log command when the container starts, which can be useful for monitoring log files in real-time.
5. CMD ["sleep", "infinity"]: This command runs the sleep infinity command when the container starts, which causes the container to stay running indefinitely until it is stopped or killed.


### LABEL ##############
LABEL is a Docker file instruction that add the metadata to the imaga, 
his metadata can include information such as the maintainer of the image, version numbers, descriptions, and other details that can help users understand what the image is for and how it should be used.
Labels can be used to add arbitrary key-value pairs to the image and can be accessed using the docker <b>inspect</b> command or by tools that support the Docker API.

1. LABEL maintainer="John Doe <johndoe@example.com>": This command sets the maintainer label for the Docker image to "John Doe johndoe@example.com".

2. LABEL version="1.0": This command sets the version label for the Docker image to "1.0".

3. LABEL description="This is a sample Docker image for a Python web application.": This command sets the description label for the Docker image to "This is a sample Docker image for a Python web application."

4. LABEL org.label-schema.schema-version="1.0" org.label-schema.build-date=$BUILD_DATE: This command sets the schema version label and build date label for the Docker image using the "org.label-schema" convention.

5. LABEL com.example.release-date="2023-03-13" com.example.version="1.0-beta" com.example.app="myapp": This command sets multiple labels for the Docker image including the release date, version, and name of the application.

### EXPOSE ########
EXPOSE is a Dockerfile instruction that informs Docker that the container will listen on the specified network ports at runtime. It does not actually publish the port or make it accessible to the host or other containers.

Here's an example of how to use EXPOSE in a Dockerfile:
FROM nginx:latest

# Expose port 80 for HTTP traffic
EXPOSE 80

# Copy the configuration file
COPY nginx.conf /etc/nginx/nginx.conf

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
In this example, the EXPOSE instruction is used to indicate that the container will listen on port 80 for HTTP traffic. This information is used by Docker when the container is started with the -P or -p options to map the container's port to the host.
Note that EXPOSE does not actually publish the port, so you'll need to use the -p or -P options when running the container to actually make the port accessible.
EXPOSE is a useful instruction for providing information to other developers or users about the intended use of a container image.

Here are the few Examples of Expose in docker.

Here are a few examples of EXPOSE in a Dockerfile:

1. Expose a single port:
FROM ubuntu:latest
EXPOSE 8080
CMD ["python", "app.py"]
In this example, the Dockerfile specifies that the container will listen on port 8080. The CMD directive specifies the command that will run when the container starts.

2. Expose multiple ports:
FROM ubuntu:latest
EXPOSE 80 443
CMD ["nginx", "-g", "daemon off;"]
This Dockerfile specifies that the container will listen on ports 80 and 443. The CMD directive specifies the command that will run when the container starts, which in this case is the NGINX web server.

3. Expose a range of ports:
FROM ubuntu:latest
EXPOSE 8000-9000
CMD ["node", "server.js"]
This Dockerfile specifies that the container will listen on ports 8000 to 9000. The CMD directive specifies the command that will run when the container starts, which in this case is a Node.js server.


### ENV #####
In Docker, ENV is used to set environment variables that can be accessed by processes running inside a container. An environment variable is a key-value pair that provides configuration or runtime information to an application.

Using ENV in Docker allows you to:

1. Set values that can be accessed from multiple layers within a Dockerfile
2. Set values that can be passed to a container when it is created using docker run
3. Provide runtime configuration for applications running inside a container

here are a few examples of using ENV in Docker:
1. Setting a database connection string:

ENV DB_HOST=localhost
ENV DB_PORT=5432
ENV DB_NAME=mydatabase
ENV DB_USER=myuser
ENV DB_PASSWORD=mypassword

2. Setting a timezone:
ENV TZ=Europe/London

3. Setting a default port for a web server:
ENV PORT=80

4. Setting a default value for a command-line argument:
ENV DEFAULT_MESSAGE="Hello, world!"

5. Setting a path to a configuration file:
ENV CONFIG_PATH=/app/config.json


### COPY ####
In Docker, COPY is a command that is used to copy files and directories from the host machine to a Docker container. The COPY instruction in a Dockerfile is used to copy files or directories from the host machine to the container's file system.

Here's the syntax for the COPY command:

 COPY <src> <dest>
<src> specifies the path of the file or directory on the host machine that you want to copy, and <dest> specifies the path in the container's file system where you want to copy the file or directory.

Here's an example of how to use COPY in a Dockerfile:

FROM ubuntu:latest
WORKDIR /app
COPY app.py .
COPY requirements.txt .
RUN pip install -r requirements.txt
CMD [ "python", "app.py" ]

In this example, we're creating a Docker image based on the latest version of the Ubuntu operating system. We're setting the working directory to /app in the container's file system. We're then using the COPY command to copy the app.py file and the requirements.txt file from the host machine to the /app directory in the container.

After that, we're running the pip install command to install the packages listed in requirements.txt. Finally, we're setting the command to run when the container is started to python app.py.

Using COPY in Docker makes it easy to include files and directories from the host machine in the Docker image, which can be useful for including configuration files, scripts, and other assets needed by the application running in the container.

# here are a few examples of using the COPY command in Docker:

1. Copying a single file:

COPY app.py /app/
In this example, we're copying the file app.py from the host machine to the /app/ directory in the container.

2. Copying a directory:

COPY src/ /app/src/
In this example, we're copying the entire src/ directory from the host machine to the /app/src/ directory in the container.

3. Copying multiple files:

COPY file1.txt file2.txt /app/
In this example, we're copying the files file1.txt and file2.txt from the host machine to the /app/ directory in the container.

4. Using wildcards:

COPY *.txt /app/
In this example, we're copying all files with the .txt extension from the host machine to the /app/ directory in the container.

5. Copying a file with a different name:

COPY app.py main.py
In this example, we're copying the file app.py from the host machine to the container and renaming it to main.py.

##### ADD ##################
ADD is a Dockerfile instruction that is used to copy files or directories from a source on the host into a destination in the Docker image.

The syntax for the ADD instruction is:

ADD <src> <dest>

Where <src> is the source of the file or directory to be copied, which can be a local file or directory on the host, a URL, or a file or directory inside the build context. <dest> is the path where the file or directory will be copied inside the Docker image.

It's important to note that ADD is intended to copy files or directories into the Docker image during the build process, rather than during runtime. If you need to copy files into a running container, you should use the docker cp command instead.

* Unlike the COPY instruction, the ADD instruction can also extract tar files automatically, which can be useful for adding compressed files to the Docker image. However, it's generally recommended to use COPY instead of ADD for copying individual files, as it has a simpler syntax and behavior.

* Furthermore, ADD has a few more features, such as being able to download a file from a URL, unpack compressed files, and automatically adjust file permissions. But, the use of COPY is still preferred for its simplicity and predictable behavior.

Here are a few examples of how the ADD instruction can be used in Docker:

## Copy a file from the host to a Docker image:

1. ADD myfile.txt /app/
This will copy the file myfile.txt from the host into the /app/ directory inside the Docker image.

2. Copy a directory from the host to a Docker image:

ADD mydir /app/
This will copy the entire mydir directory from the host into the /app/ directory inside the Docker image.

3. Download a file from a URL and add it to a Docker image:

ADD https://example.com/myfile.txt /app/
This will download the file myfile.txt from the URL https://example.com/myfile.txt and add it to the /app/ directory inside the Docker image.

4. Extract a compressed file and add it to a Docker image:

ADD myarchive.tar.gz /app/
This will extract the myarchive.tar.gz file and add its contents to the /app/ directory inside the Docker image.

Note that in each of these examples, the ADD instruction is followed by the source file or directory on the host, and then the destination directory inside the Docker image.


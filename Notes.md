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

### ENTRYPOINT #################
In Docker, ENTRYPOINT is a Dockerfile instruction that specifies the command to be run when a container based on the image is started.

The ENTRYPOINT instruction takes the following form:

ENTRYPOINT ["executable", "param1", "param2"]
where executable is the command to be executed when the container starts, and param1, param2, etc. are optional parameters to be passed to the command.

The ENTRYPOINT instruction is often used in conjunction with the CMD instruction, which provides default arguments to the command specified by ENTRYPOINT. If CMD is also specified, it will be passed as additional arguments to the command specified by ENTRYPOINT.

For example, consider the following Dockerfile:

FROM ubuntu
ENTRYPOINT ["echo", "Hello"]
CMD ["world"]
In this case, the ENTRYPOINT specifies the command echo Hello, and the CMD specifies the argument world. When a container is created from this image, the command that will be executed is echo Hello world.

It's important to note that any commands specified in the CMD instruction will override any arguments specified on the command line when the container is started. However, arguments specified on the command line can still be passed to the ENTRYPOINT command by using the --entrypoint option when running the docker run command.

Here are a few examples of how the ENTRYPOINT instruction can be used in Docker:

### A simple example using the echo command:

FROM alpine
ENTRYPOINT ["echo", "Hello, world!"]
In this example, the ENTRYPOINT specifies the echo command with the argument "Hello, world!". When a container is created from this image, the command that will be executed is echo Hello, world!.

1. A more complex example using a custom script:

FROM ubuntu
COPY myscript.sh /usr/local/bin/
ENTRYPOINT ["myscript.sh"]
CMD ["arg1", "arg2"]
In this example, the ENTRYPOINT specifies a custom script called myscript.sh that has been copied into the /usr/local/bin/ directory inside the container. The CMD specifies default arguments to be passed to the script. When a container is created from this image, the myscript.sh command will be executed with the arguments arg1 and arg2 (unless overridden by arguments passed on the command line).

2. An example that uses the exec command:

FROM alpine
ENTRYPOINT ["exec", "nginx", "-g", "daemon off;"]
In this example, the ENTRYPOINT specifies the exec command with the arguments nginx and -g daemon off;. This is a common pattern for running a long-running process in the container, such as a web server like nginx. The exec command replaces the shell process with the specified command (in this case nginx), which can help avoid issues with signal handling and process management.

Note that in all of these examples, the ENTRYPOINT instruction specifies the command to be executed when the container is started, and any arguments passed to the container are passed as additional arguments to that command.

### ONBUILD #############
The ONBUILD instruction is a Dockerfile instruction that adds a trigger to the build process. When a Docker image with an ONBUILD instruction is used as the base image for another build, the ONBUILD instructions are executed at the beginning of the new build process.

The ONBUILD instruction is used to create a "trigger" for a subsequent build. When the Dockerfile containing the ONBUILD instruction is built into an image, the instruction is not executed immediately. Instead, it adds a trigger to the image that will be executed in the future when another image is built on top of the current image.

For example, let's say you have a Dockerfile for an application that requires a specific file or configuration to be present before it can be built. You could use the ONBUILD instruction to ensure that the required file or configuration is present in any image that is built on top of your base image.

Here's an example Dockerfile that uses the ONBUILD instruction:

FROM ubuntu:latest
RUN apt-get update && apt-get install -y curl
ONBUILD ADD . /app
ONBUILD RUN /app/setup.sh

In this example, the ONBUILD ADD instruction adds the contents of the current directory to the /app directory in the image. The ONBUILD RUN instruction runs a setup script that is assumed to be present in the /app directory. When this Dockerfile is built into an image, the ONBUILD instructions are not executed immediately. Instead, they are added as triggers to the image. When another Dockerfile is built using this image as the base, the ONBUILD instructions will be executed before any other instructions in the new Dockerfile.

 ### Here are a few examples of how the ONBUILD instruction can be used in Dockerfiles:

1. Setting up a Python application
Let's say you have a Python application that requires certain dependencies to be installed. You can use the ONBUILD instruction to ensure that those dependencies are installed in any image that is built on top of your base image. Here's an example Dockerfile:

FROM python:3.8
WORKDIR /app
ONBUILD COPY requirements.txt .
ONBUILD RUN pip install --no-cache-dir -r requirements.txt
ONBUILD COPY . /app
CMD ["python", "app.py"]
In this example, the ONBUILD COPY instruction copies the requirements.txt file to the /app directory in the image. The ONBUILD RUN instruction installs the dependencies specified in requirements.txt. Finally, the ONBUILD COPY instruction copies the entire contents of the current directory to the /app directory in the image. When this Dockerfile is built into an image, the ONBUILD instructions are added as triggers to the image. When another Dockerfile is built using this image as the base, the ONBUILD instructions will be executed before any other instructions in the new Dockerfile.

2. Setting up a Node.js application
Similar to the previous example, let's say you have a Node.js application that requires certain dependencies to be installed. You can use the ONBUILD instruction to ensure that those dependencies are installed in any image that is built on top of your base image. Here's an example Dockerfile:

FROM node:14
WORKDIR /app
ONBUILD COPY package*.json ./
ONBUILD RUN npm install
ONBUILD COPY . .
CMD ["npm", "start"]
In this example, the ONBUILD COPY instruction copies the package*.json file to the /app directory in the image. The ONBUILD RUN instruction installs the dependencies specified in package.json. Finally, the ONBUILD COPY instruction copies the entire contents of the current directory to the /app directory in the image. When this Dockerfile is built into an image, the ONBUILD instructions are added as triggers to the image. When another Dockerfile is built using this image as the base, the ONBUILD instructions will be executed before any other instructions in the new Dockerfile.

### WORKDIR #########
WORKDIR is a Dockerfile instruction that sets the working directory for any RUN, CMD, ENTRYPOINT, COPY, and ADD instructions that follow it in the Dockerfile. It is used to set the default directory where the commands in the Dockerfile will be executed.

The syntax for the WORKDIR instruction is:


WORKDIR /path/to/directory
Here, /path/to/directory is the absolute path to the directory that you want to set as the working directory.

For example, consider the following Dockerfile:

FROM python:3.8
WORKDIR /app
COPY . /app
RUN pip install -r requirements.txt
CMD ["python", "app.py"]
In this Dockerfile, the WORKDIR instruction sets the working directory to /app. The COPY instruction copies the contents of the current directory to the /app directory in the image. The RUN instruction installs the dependencies specified in the requirements.txt file in the /app directory. Finally, the CMD instruction sets the command to run when a container is started from this image.

By using the WORKDIR instruction, we ensure that all subsequent commands are executed in the /app directory, which is where our application code is located. This makes the Dockerfile easier to read and helps avoid mistakes when specifying paths in the RUN, CMD, and other instructions.

#### Here is the few examples for WORKDIR  ########

1. Setting the working directory for a Node.js application
Let's say you have a Node.js application that requires certain dependencies to be installed. You can use the WORKDIR instruction to ensure that all subsequent commands are executed in the appropriate directory for the application. Here's an example Dockerfile:

FROM node:14
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
CMD ["npm", "start"]

In this example, the WORKDIR instruction sets the working directory to /app, which is where we want to install the application dependencies and run the application. The COPY instruction copies the package*.json file to the /app directory in the image. The RUN instruction installs the dependencies specified in package.json. Finally, the second COPY instruction copies the entire contents of the current directory to the /app directory in the image. When the container is started from this image, the CMD instruction runs the npm start command in the /app directory.

2. Setting the working directory for a Python application
Similar to the previous example, let's say you have a Python application that requires certain dependencies to be installed. You can use the WORKDIR instruction to ensure that all subsequent commands are executed in the appropriate directory for the application. Here's an example Dockerfile:

FROM python:3.8
WORKDIR /app
COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
CMD ["python", "app.py"]

In this example, the WORKDIR instruction sets the working directory to /app, which is where we want to install the application dependencies and run the application. The COPY instruction copies the requirements.txt file to the /app directory in the image. The RUN instruction installs the dependencies specified in requirements.txt. Finally, the second COPY instruction copies the entire contents of the current directory to the /app directory in the image. When the container is started from this image, the CMD instruction runs the python app.py command in the /app directory.

#### USER ###########

In a Dockerfile, the USER instruction is used to set the user and group that will run the subsequent RUN, CMD, ENTRYPOINT, COPY, and ADD instructions.

The syntax for the USER instruction is:

USER <user>[:<group>] or <UID>[:<GID>]
Here, <user> is the username or user ID, and <group> is the group name or group ID. If <group> is not specified, the user's primary group will be used. If <UID> and <GID> are specified, they will be used instead of the username and group name.

For example, consider the following Dockerfile:

FROM python:3.8
WORKDIR /app
COPY . /app
RUN pip install -r requirements.txt
USER appuser
CMD ["python", "app.py"]
In this Dockerfile, the USER instruction sets the user to appuser for the subsequent RUN, CMD, and other instructions. This is done to improve security by running the application as a non-root user. The CMD instruction sets the command to run when a container is started from this image.

By using the USER instruction, we ensure that the subsequent commands are executed with the permissions of the appuser user rather than the default root user. This helps to reduce the potential impact of security vulnerabilities in the application.

#### USERS EXAMPLES #########

Setting a non-root user for a Node.js application
Let's say you have a Node.js application that requires a non-root user to be used for security reasons. You can use the USER instruction to ensure that all subsequent commands are executed as this non-root user. Here's an example Dockerfile:
######
FROM node:14
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
USER node
CMD ["npm", "start"]
In this example, the USER instruction sets the user to node for the subsequent RUN, CMD, and other instructions. This is done to improve security by running the application as a non-root user. The CMD instruction sets the command to run when a container is started from this image.

Setting a specific user and group for a Python application
Similar to the previous example, let's say you have a Python application that requires a specific user and group to be used for security reasons. You can use the USER instruction to ensure that all subsequent commands are executed as this specific user and group. Here's an example Dockerfile:
###### ##########################################
FROM python:3.8
WORKDIR /app
COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
USER myuser:mygroup
CMD ["python", "app.py"]
In this example, the USER instruction sets the user to myuser and the group to mygroup for the subsequent RUN, CMD, and other instructions. This is done to improve security by running the application as a specific user and group. The CMD instruction sets the command to run when a container is started from this image.

######  VOLUME #########

In Docker, a volume is a mechanism for persisting data generated by and used by Docker containers. Volumes provide a way to share data between containers and between the host machine and containers.

Volumes are created using the docker volume create command or can be specified in a Dockerfile or docker-compose file. Once a volume is created, it can be mounted to a container using the docker run command or in a Dockerfile using the VOLUME instruction.

Volumes are stored in a part of the host filesystem that is managed by Docker. They can be created as named volumes or anonymous volumes. Named volumes are created with a specific name and can be used by multiple containers, while anonymous volumes are temporary and only used by a single container.

Here's an example of how to create and use a named volume in a Dockerfile:

######
FROM node:14
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
VOLUME /app/data
CMD ["npm", "start"]
In this example, the VOLUME instruction creates a named volume called /app/data. This volume will be created when a container is started from this image and can be used by multiple containers. Any data written to the /app/data directory in the container will be stored in the named volume and will persist even after the container is deleted.

You can mount the named volume to a container using the docker run command with the -v option:
######

docker run -v myvolume:/app/data myimage
This will create a container using the myimage image and mount the named volume myvolume to the /app/data directory in the container.

#### Volume Examples ########

1. Persisting data for a database container
Let's say you have a Docker container running a database server, and you want to persist the data stored in the database even if the container is deleted or recreated. You can use a volume to store the database data outside of the container. Here's an example docker run command:

docker run -v mydatabase:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=mysecretpassword mysql:8.0
This command creates a named volume called mydatabase and mounts it to the /var/lib/mysql directory in the container running the MySQL 8.0 image. The -e option sets the root password for the MySQL server.

2. Sharing files between containers
Let's say you have two Docker containers running, one for a web server and one for a database server, and you want to share files between them. You can use a volume to share a directory between the two containers. Here's an example docker run command:

docker run -d --name db -v db_data:/var/lib/mysql mysql:8.0
docker run -d --name web -p 80:80 --link db:mysql -v web_data:/var/www/html mywebapp:latest
This command creates two named volumes, db_data and web_data, and mounts them to the /var/lib/mysql directory in the db container and the /var/www/html directory in the web container. The --link option creates a network link between the two containers, allowing them to communicate with each other.

3. Developing applications using a bind mount
Let's say you're developing a Node.js application on your local machine, and you want to test it in a Docker container. You can use a bind mount to mount the local directory containing the application code into the container. Here's an example docker run command:

docker run -p 3000:3000 -v $(pwd):/app mynodeapp:latest
This command mounts the current directory (the one you're in when you run the command) to the /app directory in the container running the mynodeapp image. The -p option maps port 3000 in the container to port 3000 on your local machine, allowing you to access the application running in the container from your web browser.

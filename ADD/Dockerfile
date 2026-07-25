FROM almalinux
RUN yum install zip unzip -y
ADD https://raw.githubusercontent.com/GhouseRizvi/Dockerfiles/refs/heads/main/Readme.md /tmp/
ADD apache-tomcat-9.0.120.zip /tmp/
RUN unzip /tmp/apache-tomcat-9.0.120.zip -d /tmp/

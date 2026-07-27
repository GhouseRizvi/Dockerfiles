FROM almalinux
#When creator runs the docker build command, the ONBUILD instruction will be not executed.
RUN yum install -y httpd
ONBUILD ADD simple.txt/tmp/


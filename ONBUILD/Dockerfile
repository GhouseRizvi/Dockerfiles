FROM almalinux
#When creator runs the docker build command, the ONBUILD instruction will be not executed.
RUN yum install -y httpd
ONBUILD RUN echo "Welcom the the on build"


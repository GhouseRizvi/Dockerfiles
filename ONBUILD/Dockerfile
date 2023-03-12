FROM almalinux
RUN yum install nginx -y
#when image crator is running this below command will not work , when some one tries to use your image it'll run
ONBUILD ADD simple.txt /tmp/

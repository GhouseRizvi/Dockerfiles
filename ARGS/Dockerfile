#ARG is a variable that can be passed at build time to customize the image.  

ARG VERSION:latest
FROM almalinux:$VERSION
ARG GREETING
RUN echo "$GREETING"
RUN echo "The version of almalinux is $VERSION"
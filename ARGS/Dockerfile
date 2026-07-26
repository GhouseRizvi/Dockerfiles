#ARG is a variable that can be passed at build time to customize the image.  

ARG VERSION
FROM almalinux:${VERSION:-8}
ARG GREETING="Hello, World!"
RUN echo "$GREETING"
RUN echo "The version of almalinux is $VERSION"
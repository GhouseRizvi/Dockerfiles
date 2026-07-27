#ARG is a variable that can be passed at build time to customize the image.  

ARG VERSION
#setting a default value to 8
FROM almalinux:${VERSION:-8}
#Adding another argument to the image
ARG GREETING="Hello World"
ENV GREET=$GREETING
RUN echo "$GREET"
RUN echo "$VERSION"
ARG is used to supplu variables during the image creation.
In Docker, ARG is an instruction in a Dockerfile used to define build-time variables. These ARG variables can be passed to the Docker build process to parameterize the Dockerfile and control aspects of the image build dynamically. However, ARG values exist only during the build stage and are not persisted in the final image or accessible in the running container by default.

ARG VERSION=1.0
FROM alpine:${VERSION}
RUN echo "Building version ${VERSION}"

Build command to override ARG:
docker build --build-arg VERSION=2.0 -t myimage:2.0 .

NOTE: ARG DECLARED before from cannot be accessed after from.
 
 ### We can also use ENV and ARG for best results
 
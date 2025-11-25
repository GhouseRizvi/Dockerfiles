ENV
The ENV instruction in a Dockerfile is used to set environment variables that will be available both during the image build process and at runtime within the container.
we can override the env value at runtime
docker run -e MY_VAR=new_value image-name

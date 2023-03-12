### ARG 
arg is used to supply few svariables during image creation.
ARG is the only instruction we can use before from
ARG declared before from cannot be accesed after from

### using ARG and ENV for best results
Create one env variable and assign the value of ARG to that.
Then we can access ARG values through ENV both in image and container.
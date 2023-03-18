
Docker containers are ephemeral , when you remove the container it'll delete the data
to overcome this situation Docker volume is introduced.
Container will not have any default filesystem it'll use host file system when it is removed it also remove the the data.
using docker volume we create a volume where data remain safe in case container is deleted.

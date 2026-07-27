Docker containers are ephemeral, it has short life span, by default it'll delete the data.

to keep the data avaialbel even if the container is terminated.
we have a docker volume that can mount the data back to the container even in case of container failure data we'll be remain intact.

Docker save volume info 
/var/lib/docker

to create a volume t
docker volume create nginx
list a volume
docker volume ls
inspect a volume
docker volume inspect nginx

How can we attach the volume to container
 docker run -d -v nginx:/usr/share/nginx/html -p 80:80 nginx
 -p host-port:container-port
 -v host-path:container-path

Anonymous Volumes are not managed by dockers
docker run -d -v /home/ec2-user/test-data/:/usr/share/nginx/html/ -p 80:80 nginx

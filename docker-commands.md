How to remove multiple runnig containers at a time
docker rm -f `docker ps -a -q`
 docker inspect b32a526f3ca3 | grep -i author
 docker inspect b32a526f3ca3 | grep -i "label"
 [ec2-user@ip-172-31-19-190 ~]$ docker images --filter "label=author=Ghouse"
 
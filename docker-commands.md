How to remove multiple runnig containers at a time
docker rm -f `docker ps -a -q`
 docker inspect b32a526f3ca3 | grep -i author
 docker inspect b32a526f3ca3 | grep -i "label"
 [ec2-user@ip-172-31-19-190 ~]$ docker images --filter "label=author=Ghouse"
 overriding the runtime variables
[ec2-user@ip-172-31-19-190 ENV]$ docker run -e VERSION=2.0 env:v1 env
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
HOSTNAME=abc6342d8f95
VERSION=2.0
AUTHOR=GHOUSE
DESCRIPTION=This is my first dockerfile with ENV instruction
HOME=/root
 
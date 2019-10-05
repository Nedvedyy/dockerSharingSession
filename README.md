# dockerSharingSession

Goal: Demo the image creation and networking within Docker

Open three terminals: T1, T2, T3

1. start two containers in your terminals.
T1: 
docker pull amazonlinux
docker run --name dcInT1 -ti -p 8080:8080 amazonlinux

T2: 
docker run --name dcInT2 -ti amazonlinux

T3:
docker ps 

2. creat image
T1:
nc

T2:
yum install iputils to install ping
yum install nc
yum install net-tools
yum install procps
exit 2

T3: 
docker commit c3f279d17e0a  nedved/amazonimage:v2

T1: 
docker run --name dcInT1 -ti -p 8080:8080 amazonlinux


3. Networking
T1: 
nc -vlkp 8080

T2: 
nc terminal1_IP 8080
nc localIP 8080

T3: 
docker network ls
docker inspect networkID
docker port containerID

4. process mapping
T1:
ps

T3:
docker top containerIDT1





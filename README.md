# dockerSharingSession

**Goal: Demo the image creation and networking within Docker**

Open three terminals: T1, T2, T3

## 1. start two containers in your terminals.


| Terminal        | Steps           | Remarks  |
| ------------- |:-------------| :-----|
| T1      | docker pull amazonlinux | pull the image |
| | docker run --name dcInT1 -ti -p 8080:8080 amazonlinux      |  run the container and forward host 8080 to container 8080 port  |
| T2 | docker run --name dcInT2 -ti amazonlinux      |     |
| T3 | docker ps     |    show all the processes |


## 2. creat image

| Terminal        | Steps           | Remarks  |
| ------------- |:-------------| :-----|
| T1      | nc |  |
| T2 | yum install iputils to install ping      |    |
|  | yum install nc    |   |
|  | yum install net-tools    |   |
|  | yum install procps   |   |
|  | exit2  |   |
| T3 | docker commit c3f279d17e0a  nedved/amazonimage:v2     | create a new image from container 2|
| T1 | docker run --name dcInT1 -ti -p 8080:8080 amazonlinux     | run the newly created image in container 1|
|  | nc    | |

## 3. Networking

| Terminal        | Steps           | Remarks  |
| ------------- |:-------------| :-----|
| T1      | nc -vlkp 8080 | run the nc server on 8080|
| T2 | nc terminal1_IP 8080      |  nc connection to the container 1 directly  |
|  | nc localIP 8080    |  nc connection to the host, then the request will be forwarded to the container 1 |
| T3 | docker network ls    | to list down all the networks|
|  | docker inspect networkID    | to inspect the bridge |
|  | docker port containerID    | list all the port forwardining on container 1 |


## 4. Process mapping

| Terminal        | Steps           | Remarks  |
| ------------- |:-------------| :-----|
| T1      | ps | list the processes in container 1 |
| T3 | docker top containerIDT1   | list the process in container 1 from host |

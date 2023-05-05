# Networking in Docker

default networks:

1) bridge
2) none
3) host

#### bridge

`docker run ubuntu` 

private internal network created by docker on the host. All containers attached to this network and they get an internal ip address usually in the range 172.17 series. 

![image-20210911102646651](E:\AJUL\workspace\learning-docker\bridge-network.png) 



#### none

`docker run ubuntu --network=none`

isolated container

<img style="float: left;" src="./none-network.png"></img>





#### host

`docker run ubuntu --network=host` 

directly connected to host network. 

>  multiple containers running on same port is not possible.

<img style="float: left;" src="./host-network.png"></img>


Docker
=======

Docker for **windows (10)** bit different than other OS, **windows-10** has inbuild hyper-v management tool, we can create multiple VMs, we can setup primary virtual switchon Hyper-V to establish the connection with private network.On Hyper-V we can find docker NAT (Network Address Translation) to communicate with other network. 


[NAT] (https://www.cisco.com/c/en/us/support/docs/ip/network-address-translation-nat/26704-nat-faq-00.html)

![Image] (docker-architecture.png)


![Image] (Docker_vs_VM.png)


###Docker setup
[Reference](https://docs.docker.com/docker-for-windows/install/)


###Docker basic commands

* docker version (docker client version and server version has to be same)
* docker build -t <image-name> . (dot refers current working directory files as input docker build command)
* docker images (to list all images, if we build our own images, we can use publicly available images)
* docker login (to authenticate with docker hub account, same as like git-repo here we can store our own images, to pull public images we need not have any account)
* docker search <image-name*>
* docker pull image
* docker push image
* docker run -d -p 80:80 --name <container-name> <image-name>
* docker rmi <image-name/image#> (to remove particular image)
* docker rmi -f <image-name/image#> (to remove an image forcefully)
* docker rmi -f $(docker images -a -q) (to remove all available images)
* docker rm container-name/container# (to remove a specific container)
* docker exec -it container bash (to get inside docker container)
* docker ps (will display all docker processes)
* docker start <container-name/container#>
* docker stop <container-name/container#>


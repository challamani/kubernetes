Docker
=======

**Docker is an open source software platform to create, deploy and manage virtualized application containers on a common operating system (OS).**


Docker for **windows (10)** bit different than other OS, **windows-10** has in-built hyper-v management tool, we can create multiple VMs, we can setup primary virtual switch-on Hyper-V to establish the connection with private network.On Hyper-V we can find docker NAT (Network Address Translation) to communicate with other network. 
###Type - 1 Hypervisor
**Runs on top of Computer Physical Hardware**
![Image](https://github.com/java-manikanta/kubernetes/blob/master/docker/draft/hypervisor_type_1.jpg)

###Type - 2 Hypervisor
**Runs on top of Host-OS, it adds some delay in bring-up the VM and system resource accessing**
![Image](https://github.com/java-manikanta/kubernetes/blob/master/docker/draft/hypervisor_type_2.jpg)


[NAT](https://www.cisco.com/c/en/us/support/docs/ip/network-address-translation-nat/26704-nat-faq-00.html)

![Image](https://github.com/java-manikanta/kubernetes/blob/master/docker/draft/docker_architecture.png)


![Image](https://github.com/java-manikanta/kubernetes/blob/master/docker/draft/container_vs_vm_2.jpg)

![Image](https://github.com/java-manikanta/kubernetes/blob/master/docker/draft/container_vs_vm.png)


### Docker setup

[Reference](https://docs.docker.com/docker-for-windows/install/)


### Docker basic commands

* docker version (docker client version and server version has to be same)
* docker build -t <image-name> . (dot refers current working directory files as input docker build command)
* docker images (to list all images, if we build our own images, we can use publicly available images)
* docker login (to authenticate with docker hub account, same as like git-repo here we can store our own images, to pull public images we need not have any account)
* docker search <image-name*>
* docker pull image
* docker push image
* docker run -d -p <external-port>:<container-port> **--name** <container-name> <image-name>
* docker rmi <image-name/image#> (to remove particular image)
* docker rmi -f <image-name/image#> (to remove an image forcefully)
* docker rmi -f $(docker images -a -q) (to remove all available images)
* docker rm container-name/container# (to remove a specific container)
* docker exec -it container bash (to get inside docker container)
* docker ps (will display all docker processes)
* docker start <container-name/container#>
* docker stop <container-name/container#>


### Docker benefits 

* Effective resource management 
* Isolated application 
* No need to spend time in setting up QA,Staging and Production environment 
* Stack of custom images we can create (with specific features)
* Maintenance easy
* Build reusability 
* Can easily integrate with other devOp tools

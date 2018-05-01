# Minikube

## Steps to setup minikube in personal PC

* Install Kubectl in your PC (Windows either can download kubectl.exe or by using choco - util we can kubectl setup)
* Minikube setup by following Kubernetes documentation we can install minikube
* Minikube engine will come with one cluster with one worker node.
* In windows machine either we can achieve by using Hyper-V or VirtualBOX (VMWare)
* Minikube will use docker-daemon for containerization

1. Docker and Kubernetes will work on 64 bit platform only 
2. Once we start minikube then kubectl can get communicate with its master
3. 

#### When we run minikube with Hyper-V need to setup primary virtual switch (we need to be very careful other it will disturb existing Network interfaces). 
*** minikube start --vm-driver hyperv --hyperv-virtual-switch "PrimaryVSwitch" -v 9999 

### There is compatibility issue between minikube and kubectl versions, better to check compatibility before setting up minikube

[https://www.youtube.com/watch?v=BDrcUjOczsE]


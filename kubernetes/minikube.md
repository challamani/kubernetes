# Minikube

## Steps to setup minikube in personal PC

* Install Kubectl in your PC (Windows either can download kubectl.exe or by using choco - util we can kubectl setup)
* Minikube setup by following Kubernetes documentation we can install minikube
* Minikube engine will come with one cluster with one worker node.
* In windows machine either we can achieve by using Hyper-V or VirtualBOX (VMWare)
* Minikube will use docker-daemon for containerization
* Docker and Kubernetes will work on 64 bit platform only 
* Once we start minikube then kubectl can get communicate with its master

##### When we run minikube with Hyper-V need to setup primary virtual switch (we need to be very careful other it will disturb existing Network interfaces). 
....* minikube start --vm-driver hyperv --hyperv-virtual-switch "Primary Virtual Switch" -v 9999 

##### There is compatibility issue between minikube and kubectl versions, better to check compatibility before setting up minikube #####

* once the minikube is available, we start deploy pods and we can expose service

##### Example
1. kubectl run webserver --image=nginx:alpine
2. kubectl expose deployment webserver --type=LoadBalancer --port=80
3. minikube service webserver --url


*Minikube Reference [https://www.youtube.com/watch?v=BDrcUjOczsE&t=5s] [https://www.youtube.com/watch?v=BDrcUjOczsE]




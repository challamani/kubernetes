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



## Minikube in Mac

## Start Docker Desktop

## Start Minikube

- `brew install minikube`
- `minikube start --driver=docker --kubernetes-version=v1.29.10`

## Install Istio 

### Setup istioctl CLI

```shell
curl -L https://istio.io/downloadIstio | sh -
cd istio-1.*.*
export PATH=$PWD/bin:$PATH
echo 'export PATH=$PATH:'"$PWD"'/bin' >> ~/.zshrc
source ~/.zshrc
istioctl version
```

### Perform compatibility checks

```shell
istioctl x precheck
```

### Install istio

```shell
istioctl install --set profile=demo -y

#enable istio-injection for default namespace
kubectl label namespace default istio-injection=enabled
```

### Install httpbin service in default namespace

```shell
#yaml contains deployment,service,gateway and virtualservice resources.
kubectl apply -f kubernetes/resources/httpbin.yaml
```

### ExternalIP for Ingress Gateway

```shell
#run following command in new terminal
sudo minikube tunnel
kubectl get svc -n istio-system istio-ingressgateway

#add hostname mapping
echo "127.0.0.1 httpbin.local" | sudo tee -a /etc/hosts
```

### Perform curl calls to httpbin
```shell
curl -v http://httpbin.local/get
curl -v http://httpbin.local/status/200
```

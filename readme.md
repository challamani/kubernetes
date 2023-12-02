Kubernetes
=======

Kubernetes is an open-source system for automating deployment, scaling, and management of containerized applications that Google originally designed and is now maintained by the Cloud Native Computing Foundation**


[Architecture](https://x-team.com/blog/introduction-kubernetes-architecture/)


## Architecture
![Image](https://github.com/java-manikanta/kubernetes/blob/master/kubernetes/draft/k8s_architecture.jpg)

## Usecases & Architecture
<img src="https://github.com/java-manikanta/kubernetes/blob/master/kubernetes/draft/k8s_usecases.jpg" width="400" height="400"> 


## K8S Pod Networking

![Image](https://github.com/java-manikanta/kubernetes/blob/master/kubernetes/draft/k8s_pod_network.jpg)

[Pod Network](https://medium.com/google-cloud/understanding-kubernetes-networking-services-f0cb48e4cc82)

### Kubernetes Cluster setup

We have achieved the Kubernetes-cluster setup artifact with the below pre-requisites 

**One master node (Ubuntu - Desktop OS 64 bite), 2 worker nodes (Ubuntu Server OS - 64 bit)** 

Worker nodes are VM instances in the same machine (with externally available instances,; we have to use whatever master node uses network interface, eth0,eth1 and wifi)

**Worker node should be built with a minimum of 2 GB RAM, 2 cores, and 30 GB ROM**

Note: Need to check connectivity among all nodes, ssh or ping service

### Setup steps 

Below 4 steps we need to execute on each node (both master & slave nodes)
* sudo apt-get update && sudo apt-get install -qy docker.io
* sudo apt-get update && sudo apt-get install -y apt-transport-https && curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
* echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" sudo tee -a /etc/apt/sources.list.d/kubernetes.list && sudo apt-get update
* sudo apt-get update && sudo apt-get install -y kubelet kubeadm kubernetes-cni

**Configure cgroup driver used by kubelet on Master Node**

**Make sure that the cgroup driver used by kubelet is the same as the one used by Docker. Verify that your Docker cgroup driver matches the kubelet config**


### statements should execute only on master (14 commands should exec only on master)

### Double check docker cgroup driver & kubeadm cgroup driver should be equal

1. docker info | grep -i cgroup cat /etc/systemd/system/kubelet.service.d/10-kubeadm.conf
2. sed -i "s/cgroup-driver=systemd/cgroup-driver=cgroupfs/g" /etc/systemd/system/kubelet.service.d/10-kubeadm.conf

### Cluster Creation

3. kubeadm init sudo kubeadm init --pod-network-cidr=10.244.0.0/16 --apiserver-advertise-address=<master-node-ip> (secure cluster init, we have to store the init results)

### Master has to run with non-root user

4. sudo useradd <kubernete-master-user> -G sudo -m -s /bin/bash
5. sudo passwd <kubernete-master-user>
6. sudo su <kubernete-master-user>
7. cd $HOME
8. sudo cp /etc/kubernetes/admin.conf $HOME/
9. sudo chown $(id -u):$(id -g) $HOME/admin.conf
10. export KUBECONFIG=$HOME/admin.conf
11. echo "export KUBECONFIG=$HOME/admin.conf" | tee -a ~/.bashrc
12. source ~/.bashrc

**Apply your pod network (flannel)**

13. kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
14. kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/k8s-manifests/kube-flannel-rbac.yml


**Before execute join command in each worker node, we suppose to disable swapoff**

* <swapoff -a>
* <sudo sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab>

15. sudo kubeadm join --token token# master-node-ip:6443 --discovery-token-ca-cert-hash sha256:hash# 
16. kubectl get nodes (should display all nodes, which all are connected with kubeadm - join with token)


**If anything goes wrong like worker nodes not appearing in <kubectl get nodes> or problem with creating pods and container in worker-node can reset the process.**

**need to execute below statements in every node include master-node, after below statements we need to start from step-1 again**
* kubeadm reset
* service docker restart
* systemctl kubelet restart


* [Create cluster kubeadm](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/)

* [Kubernetes in 10 minutes](https://blog.alexellis.io/kubernetes-in-10-minutes/)


### Kubectl basic commands

* `kubectl get nodes`
* `kubectl cluster-info`
* `kubectl config view`

* `kubectl get pods -o wide`
* `kubectl get deployments`
* `kubectl describe pods`
* `kubectl logs pod`
* `kubectl run pod-name --image=image#:tag (pod creation)`

* `kubectl get services/svc`
* `kubectl describe service service-name`
* `kubectl scale deployment name --replicas=3`
* `kubectl delete service service-name`
* `kubectl expose deployment/pod-name --type=LoadBalancer/NodePort --port=service-port`

* `kubectl get ingress/ing`
* `kubectl describe ingress ingress-name#`


#### Examples:


. kubectl run webserver --image=nginx:alpine --replicas=2
. kubectl expose deployment webserver --type=LoadBalancer --port=80


. kubectl run camunda --image=camunda/camunda-bpm-platform:latest --replicas=2
. kubectl expose deployment/camunda --type=LoadBalancer --port=8080

. kubectl run wso2apim --image=isim/wso2apim
. kubectl expose deployment/wso2apim --type=LoadBalancer --port=9443

. kubectl run wso2esb --image=isim/wso2esb
. kubectl expose deployment/wso2esb --type=LoadBalancer --port=9443


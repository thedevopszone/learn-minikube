# How to Install Minikube on RHEL 9 Step-by-Step

1) Install Podman
2)  Install Kubectl 
3) Download and Install Minikube Binary
4) Start Minikube Cluster
5) Manage Minikube Addons
6) Test Kubernetes Cluster
7) Manage Minikube Cluster


## Prerequisites
- Minimal Installed RHEL 9 System
- Sudo User with Admin Rights
- Red Hat Subscriptions or locally Configured Repository
- Internet Connectivity
- Minimum 2 GB RAM or more
- 2 vCPUs or more
- 20 GB Free Disk Space

## 1) Install Podman

```
sudo dnf install -y podman
```

Allow your local user to run podman commands with passwordless sudo
```
echo "tmundt ALL=(ALL) NOPASSWD: /usr/bin/podman" | sudo tee /etc/sudoers.d/tmundt

# It should not prompt you to enter local user password
sudo -k -n podman version
```


## 2)  Install Kubectl

```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client
```


## 3) Download and Install Minikube Binary

```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
minikube version
```


## 4) Start Minikube Cluster

```
minikube start --driver=podman
```


Kubectl Commands
```
$ kubectl cluster-info
$ kubectl get nodes
$ kubectl get pods -A
```


## 5) Manage Minikube Addons

```
$ minikube addons list    // This will list available addons 
$ minikube addons enable dashboard   // It will enable k8s dashboard
$ minikube addons enable ingress     // It will enable ingress controller
$ minikube addons list | grep -i -E "dashboard|ingress"
```


To get Kubernetes dashboard url , run
```
$ minikube dashboard --url

minikube dashboard
```


## 6) Test Kubernetes Cluster

```
$ kubectl create deployment demo --image=nginx --replicas=2
$ kubectl expose deployment demo --type NodePort --port=80
$ kubectl get deployment demo
$ kubectl get pods
```

Get the url for your application, run
```
$ minikube service demo --url
http://192.168.49.2:31989$
```


Now, try to access application using following url
```
$ curl http://192.168.49.2:31989
```




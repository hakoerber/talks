### Kubernetes
An Orchestrator for Microservice Apps


* Big picture
  * Masters
  * Nodes
  * Pods
  * Services
* Installation
  * [Minikube](#minikube)
  * [Manual Cluster](#manual-cluster)
    * [Kubeadm](#kubeadm)
  * [GCE Goole Container Engine](#google-container-engine-gce)
  * [AWS](#aws)
    * [KOPS Kuberenetes OPS](#kops-kubernetes-ops)
* [Links](#links)
* [Questions](#questions)

## Minikube
Best way of spinning up a local k8s environment
![](img/0225.png)
![](img/0227.png)

#### installation of kubectl
##### macos
```sh
brew install kubectl
```
##### linux
```sh
apt-get install kubectl
```
#### installation of minikube
##### macos
```sh
brew cask install minikube
```
##### linux
```sh
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
 && chmod +x minikube && sudo mv minikube /usr/local/bin/
```
#### start minikube
```sh
minikube start
```
#### check current context
```sh
kubectl config current-context
```
#### get nodes
```sh
kubectl get nodes
```

#### show dashboard (opens browser)
```sh
minikube dashboard
```

#### stop minikube
```sh
minikube stop
```


## Manual Cluster

### Kubeadm

## Google Container Engine GCE

## AWS

### KOPS Kubernetes OPS

## Links
[Minikube](https://github.com/kubernetes/minikube)


## Questions
* kubectl switch context


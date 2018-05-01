## Preparations

#### install minikube

##### macos
```sh
brew cask install minikube
```
##### linux
```sh
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
 && chmod +x minikube \
 && sudo mv minikube /usr/local/bin/
```

#### install kubectl
##### macos
```sh
brew install kubectl
```
##### linux
```sh
apt-get install kubectl


### create minikube cluster
```sh
minikube start
```
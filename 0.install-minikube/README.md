## Install Minikube

### install minikube cli
```
$ curl -LO https://storage.googleapis.com/minikube/releases/v1.16.0/minikube-linux-amd64
$ chmod +x minikube-linux-amd64
$ sudo mv minikube-linux-amd64 /usr/local/bin/minikube
``

### install K8S minikube server
```
$ minikube version

$ minikube start --driver=none
```

### Test Kubectl cli
```
$ kubectl version

$ kubectl get ns
```

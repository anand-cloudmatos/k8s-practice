## Install Minikube

### install minikube cli
```bash
$ curl -LO https://storage.googleapis.com/minikube/releases/v1.16.0/minikube-linux-amd64
$ chmod +x minikube-linux-amd64
$ sudo mv minikube-linux-amd64 /usr/local/bin/minikube
```
### Prerequisite 
```bash
$ yum install conntrack
$ hostname minikube
$ systemctl enable docker.service
$ sudo echo '1' > /proc/sys/net/bridge/bridge-nf-call-iptables

```

### install K8S minikube server
```bash
$ minikube version

$ minikube start --driver=none
```
### Install Kubectl cli if kubectl command not found
```bash
$ cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
EOF

$ yum install -y kubectl
```

### Test Kubectl cli
```bash
$ kubectl version

$ kubectl get ns

$ kubectl get nodes
```

## Namespace in Openshift/k8s

### List all namespaces
```bash
$ kubectl get ns 
```
### List pod from kube-system
```bash
$ kubectl get pod -n kube-system

NAME                              READY   STATUS    RESTARTS   AGE
coredns-74ff55c5b-gl5gd           1/1     Running   0          24h
etcd-docker1                      1/1     Running   0          24h
kube-apiserver-docker1            1/1     Running   0          24h
kube-controller-manager-docker1   1/1     Running   0          24h
kube-proxy-dct6v                  1/1     Running   0          24h
kube-scheduler-docker1            1/1     Running   0          24h
storage-provisioner               1/1     Running   0          24h
```
### List POD from default namespace
```
$ kubectl get pod 
NAME    READY   STATUS    RESTARTS   AGE
hello   1/1     Running   0          7s

$ kubectl get pod -n default
NAME    READY   STATUS    RESTARTS   AGE
hello   1/1     Running   0 
```
### Create Namespace  my-ns 

```bash
$ kubectl create ns my-ns
$ kubectl get ns
```

### Create Pod in  my-ns  namespace
```bash
$ kubectl run hello --image=openshift/hello-openshift -n my-ns
$ kubectl get po -n my-ns
```

### Delete Pod
```bash
$ kubectl delete po hello -n my-ns
pod "hello" deleted
```

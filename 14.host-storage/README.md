## HOST Storage in Openshift/k8s


### create mount directory
```bash
# This assumes that your Node uses "sudo" to run commands
# as the superuser
$ sudo mkdir /tmp/data
```

### create index.html
```bash
# This again assumes that your Node uses "sudo" to run commands
# as the superuser
$ echo 'Hello from Kubernetes storage' > /mnt/data/index.html

$ cat /mnt/data/index.html
```

### Create a PersistentVolume 
```bash
$ kubectl apply -f pv.yaml
```


### GET a PersistentVolume 
```bash
$ kubectl get pv task-pv-volume
```

### Create a PersistentVolumeClaim
```bash
$ kubectl apply -f pvc.yaml
```


### GET a PersistentVolumeClaim
```bash
$ kubectl get pvc task-pv-claim
```

### Create POD
```bash
$ kubectl apply -f pod.yaml
```

### GET POD
```bash
$ kubectl get pod
```

### Access Application
```bash
$ curl http://<minikube-ip>:80
Hello from Kubernetes storage
```

### Delete All
```bash
$ kubectl delete -f .
$ kubectl delete all --all
```
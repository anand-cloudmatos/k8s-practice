## Init-Container Openshift/k8s

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
```

### Delete All
```bash
$ kubectl delete -f .
$ kubectl delete all --all
```
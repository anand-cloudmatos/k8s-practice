## SideCar Openshift/k8s

### Create POD
```bash
$ kubectl apply -f pod.yaml
```

### GET POD
```bash
$ kubectl get pod -o wide
```

### Access Application
```bash
$ curl http://<pod-ip>:80/app.txt
```

### Delete All
```bash
$ kubectl delete -f .
$ kubectl delete all --all
```
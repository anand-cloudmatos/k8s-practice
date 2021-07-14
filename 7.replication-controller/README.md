## Deploy replication-controller on Openshift/k8s


### Create and Get replication-controller Object
```bash
$ kubectl get -f rc.yml 
$ kubectl get rc 
NAME       DESIRED   CURRENT   READY   AGE
hello-rc   3         3         1       1m
```
### check 3 pods are running
```bash
$ kubectl get pods -o wide 
NAME             READY   STATUS    RESTARTS   AGE   IP            NODE     NOMINATED NODE
hello-rc-ds5gn   1/1     Running   0          1m    10.128.0.44   master   <none>
hello-rc-jbtjm   1/1     Running   0          18s   10.128.0.46   master   <none>
hello-rc-nfdxh   1/1     Running   0          18s   10.128.0.45   master   <none>
```
### delete one pod
```bash
$ kubectl delete pod hello-rc-ds5gn 
pod "hello-rc-ds5gn" deleted
```
### Get Pods - Observe that new pod created automatically
```bash
$ kubectl get pods -w 
NAME             READY   STATUS    RESTARTS   AGE
hello-rc-6rhb9   1/1     Running   0          9s
hello-rc-jbtjm   1/1     Running   0          47s
hello-rc-nfdxh   1/1     Running   0          47s
```
### Increase replica to 5
```bash
$ kubectl scale rc hello-rc --replicas=5 
replicationcontroller/hello-rc scaled
```

### Get Pods - Observer 2 new pods are created
```bash
$ kubectl get pods 
NAME             READY   STATUS              RESTARTS   AGE
hello-rc-6rhb9   1/1     Running             0          2m
hello-rc-9f4wh   0/1     ContainerCreating   0          5s
hello-rc-jbtjm   1/1     Running             0          2m
hello-rc-nfdxh   1/1     Running             0          2m
hello-rc-zw6wp   0/1     ContainerCreating   0          5s

$ kubectl get pods 
NAME             READY   STATUS    RESTARTS   AGE
hello-rc-6rhb9   1/1     Running   0          2m
hello-rc-9f4wh   1/1     Running   0          10s
hello-rc-jbtjm   1/1     Running   0          2m
hello-rc-nfdxh   1/1     Running   0          2m
hello-rc-zw6wp   1/1     Running   0          10s
```

### Scale donw application to 0
```bash
$ kubectl scale rc hello-rc --replicas=0 
replicationcontroller/hello-rc scaled

$ kubectl get pods 
NAME             READY   STATUS        RESTARTS   AGE
hello-rc-6rhb9   0/1     Terminating   0          2m
hello-rc-9f4wh   0/1     Terminating   0          23s
hello-rc-jbtjm   0/1     Terminating   0          3m
hello-rc-zw6wp   0/1     Terminating   0          23s

$ kubectl get pods 
No resources found in replication-control namespace.
```

### Start one replica
```bash
$ kubectl scale rc hello-rc --replicas=1 
replicationcontroller/hello-rc scaled

$ kubectl get pods 
NAME             READY   STATUS              RESTARTS   AGE
hello-rc-jghxq   0/1     ContainerCreating   0          5s


$ kubectl get pods 
NAME             READY   STATUS    RESTARTS   AGE
hello-rc-jghxq   1/1     Running   0          22s


$ kubectl delete rc hello-rc 
replicationcontroller "hello-rc" deleted

$ kubectl get all 
No resources found in replication-control namespace.
```

### Expose service for rc
```bash
$  kubectl expose rc hello-rc
$  kubectl get svc
$  kubectl get svc hello-rc -o yaml
$  curl <service-ip>:8080

```


### Delete All
```bash
$ kubectl delete all --all
```
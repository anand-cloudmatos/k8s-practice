## Deploy multicontainer single pod on Openshift/k8s


### Create pod using manifest file 
```bash
$ kubectl create -f multicontainer-single-pod.yml 
pod/multicontainer-single-app created
```
### Get Pod
```bash
$ kubectl get pods 
NAME                        READY   STATUS    RESTARTS   AGE
multicontainer-single-app   4/4     Running   0          1m
```
### Describe POD
```bash
$ kubectl describe pod hello-app 
```
### Check counter container logs 
  
```bash
$ kubectl logs multicontainer-single-app -c counter 
Incrementing counter by 5 ...
Incrementing counter by 2 ...
Incrementing counter by 10 ...
Incrementing counter by 9 ...
Incrementing counter by 9 ...
Incrementing counter by 5 ...
Incrementing counter by 10 ...
Incrementing counter by 10 ...
```

### Check counter container logs 
  
```bash
$ kubectl logs multicontainer-single-app -c poller 
Current counter: 35
Current counter: 50
Current counter: 65
Current counter: 82
Current counter: 97
Current counter: 108
Current counter: 115
```

### Delete Pod
```bash
$ kubectl delete -f multicontainer-single-pod.yml 
pod "hello-app" deleted
```

### Delete All
```bash
$ kubectl delete all --all
pod "hello-app" deleted
```
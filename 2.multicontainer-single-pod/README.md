## Deploy multicontainer single pod on Openshift/k8s

### 1. Create new project single-pod
```bash
$ kubectl create ns multicontainer-pod
```
### 2. Create pod using manifest file 
```bash
$ kubectl create -f multicontainer-single-pod.yml -n multicontainer-pod
pod/multicontainer-single-app created
```
### 3. Get Pod
```bash
$ kubectl get pods -n multicontainer-pod
NAME                        READY   STATUS    RESTARTS   AGE
multicontainer-single-app   4/4     Running   0          1m
```
### 4. Describe POD
```bash
$ kubectl describe pod hello-app -n multicontainer-pod
```
### 5. Check counter container logs 
  
```bash
$ kubectl logs multicontainer-single-app -c counter -n multicontainer-pod
Incrementing counter by 5 ...
Incrementing counter by 2 ...
Incrementing counter by 10 ...
Incrementing counter by 9 ...
Incrementing counter by 9 ...
Incrementing counter by 5 ...
Incrementing counter by 10 ...
Incrementing counter by 10 ...
```

### 6. Check counter container logs 
  
```bash
$ kubectl logs multicontainer-single-app -c poller -n multicontainer-pod
Current counter: 35
Current counter: 50
Current counter: 65
Current counter: 82
Current counter: 97
Current counter: 108
Current counter: 115
```

### 7. Delete Pod
```bash
$ kubectl delete -f multicontainer-single-pod.yml -n multicontainer-pod
pod "hello-app" deleted
```
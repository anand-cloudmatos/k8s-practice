## Deploy multi-pod-service  on Openshift/k8s


### 2. Create new app
```bash
$ kubectl create -f . 
pod/api-server created
service/api-server created
pod/app created
pod/redis created
service/redis created
```

### 3. Get POD
```bash
kubectl get pods 
NAME         READY   STATUS    RESTARTS   AGE
api-server   1/1     Running   2          1m
app          2/2     Running   0          1m
redis        1/1     Running   0          1m
```
### 4. Check Poller logs
```bash
$ kubectl logs app -c poller 
Current counter:
Current counter:
Current counter:
Current counter:
Current counter: 3
Current counter: 5
Current counter: 15
Current counter: 27
Current counter: 42
Current counter: 56
Current counter: 74
Current counter: 86
Current counter: 95
Current counter: 115
```

### 5. Get Counter logs
```bash
$ kubectl logs app -c counter 
Incrementing counter by 2 ...
Incrementing counter by 9 ...
Incrementing counter by 5 ...
Incrementing counter by 4 ...
Incrementing counter by 3 ...
Incrementing counter by 9 ...
Incrementing counter by 5 ...
Incrementing counter by 3 ...
Incrementing counter by 5 ...
Incrementing counter by 3 ...
Incrementing counter by 2 ...
Incrementing counter by 10 ...
```

### Delete All
```bash
$ kubectl delete all --all
pod "hello-app" deleted
```
## Deploy LoadBalancer Service on Openshift/k8s

### Create pod and service
```
$ kubectl create -f . 
pod/hello-pod created
service/hello-load-balance created
```
### Get all Object
```
$ kubectl get all 
NAME            READY   STATUS    RESTARTS   AGE
pod/hello-pod   1/1     Running   0          23s

NAME                         TYPE           CLUSTER-IP       EXTERNAL-IP                   PORT(S)          AGE
service/hello-load-balance   LoadBalancer   172.30.101.122   172.29.92.247,172.29.92.247   8080:31747/TCP   23s
```

### Delete All
```bash
$ kubectl delete all --all
```
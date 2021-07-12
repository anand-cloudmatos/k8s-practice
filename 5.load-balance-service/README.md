## Deploy LoadBalancer Service on Openshift/k8s

### Create new project load-balance
```bash
$ kubectl create ns load-balance 
```
### Create pod and service
```
$ kubectl create -f . -n load-balance
pod/hello-pod created
service/hello-load-balance created
```
### Get all Object
```
$ kubectl get all -n load-balance
NAME            READY   STATUS    RESTARTS   AGE
pod/hello-pod   1/1     Running   0          23s

NAME                         TYPE           CLUSTER-IP       EXTERNAL-IP                   PORT(S)          AGE
service/hello-load-balance   LoadBalancer   172.30.101.122   172.29.92.247,172.29.92.247   8080:31747/TCP   23s
```

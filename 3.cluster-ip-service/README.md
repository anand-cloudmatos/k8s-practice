## Deploy ClusterIP Service on Openshift/k8s

### Create new project cluster-ip-service
```bash
 $ kubectl create ns cluster-ip-service    
```

### Create pod
```bash
$ kubectl create -f .\pod.yml -n cluster-ip-service
  pod/hello-pod created
```

### GET pod
```bash  
$ kubectl get pods  -n cluster-ip-service         
NAME        READY   STATUS    RESTARTS   AGE
hello-pod   1/1     Running   0          11s
```

### Create Service
``` bash
$ kubectl create -f .\service.yml -n cluster-ip-service    
service/hello-svc created
```

### GET service
``` bash
$ kubectl get service   -n cluster-ip-service   
NAME        TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
hello-svc   ClusterIP   172.30.203.182   <none>        8080/TCP   19s
```

### Describe pod
```
$ kubectl describe service hello-svc  -n cluster-ip-service       
Name:              hello-svc
Namespace:         cluster-ip-service
Labels:            <none>
Annotations:       <none>
Selector:          app=hello
Type:              ClusterIP
IP:                172.30.203.182
Port:              <unset>  8080/TCP
TargetPort:        8080/TCP
Endpoints:         10.128.0.26:8080
Session Affinity:  None
Events:            <none>
```

### Curl from extenal network (home laptop)
```
$ curl http://172.30.203.182:8080                                                                                     
curl : Unable to connect to the remote server
```


### Curl from cluster (k8s master node)
```
$ curl http://172.30.203.182:8080                                                                                     
Hello OpenShift!!
```


### Create Service 2
```
$ kubectl create -f .\service.yml -n cluster-ip-service                                                                                   
service/hello-svc2 created
Error from server (AlreadyExists): error when creating ".\\service.yml": services "hello-svc" already exists
```


### Describe all service
```
$ kubectl describe service                                                                                                 Name:              hello-svc
Namespace:         cluster-ip-service
Labels:            <none>
Annotations:       <none>
Selector:          app=hello
Type:              ClusterIP
IP:                172.30.203.182
Port:              <unset>  8080/TCP
TargetPort:        8080/TCP
Endpoints:         10.128.0.26:8080
Session Affinity:  None
Events:            <none>


Name:              hello-svc2
Namespace:         cluster-ip-service
Labels:            <none>
Annotations:       <none>
Selector:          app=hello
Type:              ClusterIP
IP:                172.30.128.219
Port:              <unset>  9090/TCP
TargetPort:        8080/TCP
Endpoints:         10.128.0.26:8080
Session Affinity:  None
```


### Curl from cluster (k8s master node)
```
$  curl http://172.30.203.182:8080
Hello OpenShift!
$  curl http://172.30.203.182:9090
curl: (7) Failed connect to 172.30.203.182:9090; No route to host
$  curl http://172.30.128.219:9090
Hello OpenShift!
```

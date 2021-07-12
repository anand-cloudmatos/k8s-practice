## Deploy LoadBalancer Service on Openshift/k8s

### Create new project node-prot
```bash
$ kubectl create ns node-port  
```
### Create pod and service
```
$ kubectl create -f .\app.yml -n node-port 
pod/hello-pod created
service/hello-nodeport created
```
### Get all object
```
$ kubectl get all  -n node-port 
NAME            READY   STATUS    RESTARTS   AGE
pod/hello-pod   1/1     Running   0          42s

NAME                     TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
service/hello-nodeport   NodePort   172.30.92.114   <none>        9090:32402/TCP   42s
```

### Access application using nodeIP and port (32402 port create by cluster in previous command)
```
$ curl <minikube-ip>:<nodepod>
Hello OpenShift!
```
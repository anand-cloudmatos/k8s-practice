## Deploy single pod on Openshift/k8s using kubectl run

### Create hello pod using kubectl run command
```bash
$ kubectl run hello --image=openshift/hello-openshift --restart=Never 
```
### Check hello POD created
```bash
$ kubectl get pod 
NAME    READY   STATUS              RESTARTS   AGE
hello   0/1     ContainerCreating   0          4s

$ kubectl get pod 
NAME    READY   STATUS    RESTARTS   AGE
hello   1/1     Running   0          7s
```
### Describe POD
```bash
$ kubectl describe pod hello 
```
### To access application 

- Connect to k8s master node
- Obtain Pod IP from describe command   
```bash
$ curl http://<pod-ip>:8080
hello Html page
```

### 7. Delete Pod
```bash
$ kubectl delete pod hello 
pod "hello" deleted
```

## Deploy single pod on Openshift/k8s using Manifest

### Create pod using manifest file 
```bash
# generate pod manifest 
$ kubectl run hello-app --image=openshift/hello-openshift --restart=Never --dry-run -o yaml > single-pod.yaml

# create pod
$ kubectl create -f single-pod.yml 
pod/hello-app created
```
### Get Pod
```bash
$ kubectl get pods 
NAME        READY   STATUS    RESTARTS   AGE
hello-app   1/1     Running   0          32s
```
### Describe POD
```bash
$ kubectl describe pod hello-app 
```
### To access application 

- Connect to k8s master node
- Obtain Pod IP from describe command   
```bash
$ curl http://<pod-ip>:8080
Hello Openshift
```

### Delete Pod
```bash
$ kubectl delete -f single-pod.yml 
pod "hello-app" deleted
```


### Delete All
```bash
$ kubectl delete all --all
pod "hello-app" deleted
```

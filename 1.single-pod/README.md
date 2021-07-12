## Deploy single pod on Openshift/k8s using kubectl run

### Create new project single-pod
```bash
$ kubectl create ns single-pod
```

### Create nginx pod using kubectl run command
```bash
$ kubectl run hello --image=nginx --restart=Never -n single-pod
```
### 4. Check nginx POD created
```bash
$ kubectl get pod -n single-pod
NAME    READY   STATUS              RESTARTS   AGE
nginx   0/1     ContainerCreating   0          4s

$ kubectl get pod -n single-pod
NAME    READY   STATUS    RESTARTS   AGE
nginx   1/1     Running   0          7s
```
### 5. Describe POD
```bash
$ kubectl describe pod hello-app -n single-pod
```
### 6. To access application 

- Connect to k8s master node
- Obtain Pod IP from describe command   
```bash
$ curl http://<pod-ip>:8080
Nginx Html page
```

### 7. Delete Pod
```bash
$ kubectl delete pod nginx -n single-pod
pod "nginx" deleted
```

## Deploy single pod on Openshift/k8s using Manifest

### 1. Create new project single-pod
```bash
$ kubectl create ns single-pod
```
### 2. Create pod using manifest file 
```bash
# generate pod menifest 
$ kubectl run hello-app --image=openshift/hello-openshift --restart=Never --dry-run -o yaml > single-pod.yaml

# create pod
$ kubectl create -f single-pod.yml -n single-pod
pod/hello-app created
```
### 3. Get Pod
```bash
$ kubectl get pods -n single-pod
NAME        READY   STATUS    RESTARTS   AGE
hello-app   1/1     Running   0          32s
```
### 4. Describe POD
```bash
$ kubectl describe pod hello-app -n single-pod
```
### 5. To access application 

- Connect to k8s master node
- Obtain Pod IP from describe command   
```bash
$ curl http://<pod-ip>:8080
Hello Openshift
```

### 6. Delete Pod
```bash
$ kubectl delete -f single-pod.yml -n single-pod
pod "hello-app" deleted
```
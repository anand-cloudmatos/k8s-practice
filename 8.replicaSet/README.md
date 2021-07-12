## Deploy ReplicaSet on Openshift/k8s

### 1. Create new project replica-set
```bash
$ kubectl create ns replica-set
Now using project "replica-set"
```
### 2. Create replica-set
```bash
$ kubectl apply -f replicaSet.yml -n replica-set
replicaset.apps/hello-rs created
```

### 3. GEt replica-set
```bash
$ kubectl get rs -n replica-set
NAME       DESIRED   CURRENT   READY   AGE
hello-rs   2         2         2       16s
```

### 4. Describe replica-set
```bash
$ kubectl describe rs hello-rs -n replica-set
Name:         hello-rs
Namespace:    replica-set
Selector:     app=hello,tier in (backend)
Labels:       <none>
Annotations:  kubectl.kubernetes.io/last-applied-configuration:
                {"apiVersion":"apps/v1","kind":"ReplicaSet","metadata":{"annotations":{},"name":"hello-rs","namespace":"replica-set"},"spec":{"replicas":2...
Replicas:     2 current / 2 desired
Pods Status:  2 Running / 0 Waiting / 0 Succeeded / 0 Failed
Pod Template:
  Labels:  app=hello
           tier=backend
  Containers:
   hello:
    Image:        openshift/hello-openshift
    Port:         8080/TCP
    Host Port:    0/TCP
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Events:
  Type    Reason            Age        From                   Message
  ----    ------            ----       ----                   -------
  Normal  SuccessfulCreate  <invalid>  replicaset-controller  Created pod: hello-rs-lpvv5
  Normal  SuccessfulCreate  <invalid>  replicaset-controller  Created pod: hello-rs-7vr79
```

### 5. Scale replica-set to 5
```bash
$ kubectl scale rs hello-rs --replicas=5 -n replica-set
replicaset.extensions/hello-rs scaled
```

### 6. Get REplica set
```bash
$ kubectl get rs -n replica-set
NAME       DESIRED   CURRENT   READY   AGE
hello-rs   5         5         2       1m

$ kubectl get rs -n replica-set
NAME       DESIRED   CURRENT   READY   AGE
hello-rs   5         5         4       1m

$ kubectl get rs -n replica-set
NAME       DESIRED   CURRENT   READY   AGE
hello-rs   5         5         5       1m
```

### 7. Get Pod
```bash
$ kubectl get pods -n replica-set
NAME             READY   STATUS    RESTARTS   AGE
hello-rs-7vr79   1/1     Running   0          1m
hello-rs-ddw6x   1/1     Running   0          17s
hello-rs-k8ckz   1/1     Running   0          17s
hello-rs-lpvv5   1/1     Running   0          1m
hello-rs-zzdfs   1/1     Running   0          17s
```

### 8. Create Service and display Yaml file using command
```bash
$ kubectl expose rs hello-rs --port=8080  --selector='app=hello' -o yaml -n replica-set
apiVersion: v1
kind: Service
metadata:
  creationTimestamp: null
  name: hello-rs
spec:
  ports:
  - port: 8080
    protkubectlol: TCP
    targetPort: 8080
  selector:
    '''app': hello'
status:
  loadBalancer: {}
```

### 9. Get Service
```bash
$ kubectl get svc -n replica-set
NAME    TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)    AGE
hello   ClusterIP   172.30.51.95   <none>        8080/TCP   49s
```

### 10. check application using route url
```bash
$ curl <cluster-ip>:8080
Hello OpenShift!
```

### 11. Delete Replica Set
```bash

$ kubectl delete rs hello-rs -n replica-set
replicaset.extensions "hello-rs" deleted
```
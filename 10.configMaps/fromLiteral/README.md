## Deploy Pod using config-map-from-literals on Openshift/k8s

### Create POD without Configmap
```bash
$ kubectl apply -f pod.yml 
$ kubectl get pod,svc
NAME            READY   STATUS              RESTARTS   AGE
pod/color-app   0/1     ContainerCreating   0          12s

NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   5m7s

$ kubectl get po
NAME        READY   STATUS                       RESTARTS   AGE
color-app   0/1     CreateContainerConfigError   0          20s

$ kubectl describe pod color-app
Name:         color-app
Namespace:    default
Priority:     0
Node:         kube1.trainings.lab/10.1.10.7
Start Time:   Wed, 14 Jul 2021 10:29:14 +0530
Labels:       app=color-app
Annotations:  <none>
Status:       Pending
IP:           172.17.0.3
IPs:
  IP:  172.17.0.3
Containers:
  color-app:
    Container ID:
    Image:          anandnevase/color-app
    Image ID:
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Waiting
      Reason:       CreateContainerConfigError
    Ready:          False
    Restart Count:  0
    Environment Variables from:
      color-config-map  ConfigMap  Optional: false
    Environment:        <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-gpzcn (ro)
Conditions:
  Type              Status
  Initialized       True
  Ready             False
  ContainersReady   False
  PodScheduled      True
Volumes:
  default-token-gpzcn:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-gpzcn
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                 node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type     Reason     Age                From               Message
  ----     ------     ----               ----               -------
  Normal   Scheduled  43s                default-scheduler  Successfully assigned default/color-app to kube1.trainings.lab
  Normal   Pulled     29s                kubelet            Successfully pulled image "anandnevase/color-app" in 12.580708956s
  Normal   Pulled     26s                kubelet            Successfully pulled image "anandnevase/color-app" in 2.785218972s
  Warning  Failed     13s (x3 over 29s)  kubelet            Error: configmap "color-config-map" not found
  Normal   Pulled     13s                kubelet            Successfully pulled image "anandnevase/color-app" in 2.77947947s
  Normal   Pulling    0s (x4 over 42s)   kubelet            Pulling image "anandnevase/color-app"
```
### Create Config map
```
$ kubectl create configmap color-config-map --from-literal=APP_COLOR=red 
configmap/color-config-map created

$ kubectl get configmap 
NAME               DATA   AGE
color-config-map   1      5s

$ kubectl describe configmap color-config-map 
Name:         color-config-map
Namespace:    config-map-from-literals
Labels:       <none>
Annotations:  <none>

Data
====
APP_COLOR:
----
red
Events:  <none>
```

### create POD
```bash
$ kubectl apply -f pod.yml 
pod/color-app created
```

### create service
```bash
$ kubectl expose pod/color-app  --type=NodePort
service/color-app exposed
```

###  Accees application
Access application using <minikube-ip>:<nodeport>

  ### Delete All
```bash
$ kubectl delete all --all
```
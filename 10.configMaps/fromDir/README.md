## Deploy Pod using config-map-from-dir on Openshift/k8s

### Create config-map from literal
```bash
$ kubectl create configmap color-config-map --from-literal=APP_COLOR=red 
configmap/color-config-map created
```

### Create new project config-map from directory
```bash
$ kubectl create configmap color-config-map-dir --from-file=./config 
configmap/color-config-map-dir created
```

### GET All config-map
```bash
$ kubectl get configmaps 
NAME                   DATA   AGE
color-config-map       1      21s
color-config-map-dir   2      12s
```

### Describe all config-map 
```bash
$ kubectl describe configmap 
Name:         color-config-map
Namespace:    config-map-from-dir
Labels:       <none>
Annotations:  <none>

Data
====
APP_COLOR:
----
red
Events:  <none>


Name:         color-config-map-dir
Namespace:    config-map-from-dir
Labels:       <none>
Annotations:  <none>

Data
====
myconfig.conf:
----
config-file
testfile.txt:
----
Hello  - ConfigMap from File
Events:  <none>
```

### Create Pod
```bash
$ kubectl apply -f pod.yml 
pod/color-app created
```

### create service
```bash
$ kubectl expose pod/color-app  --type=NodePort
service/color-app exposed
```


### Accees application
Hit route url in Browser - You will observer following things
 - using URL : http://<minikube-ip>:<nodeport>
  HTML RED color Page, because in config map value of APP_COLOR is RED
 - using URL : http://<minikube-ip>:<nodeport>/read_file
  HTML Red color Page with text_file.txt content in text area


### Delete All
```bash
$ kubectl delete all --all
```
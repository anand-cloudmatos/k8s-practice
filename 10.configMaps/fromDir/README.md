## Deploy Pod using config-map-from-dir on Openshift/k8s

### 1. Create new project config-map-from-dir
```bash
$ kubectl create ns config-map-from-dir
Now using project "config-map-from-dir" on server "https://2886795320-8443-cykoria05.environments.katacoda.com:443".
```

### 2. Create config-map from literal
```bash
$ kubectl create configmap color-config-map --from-literal=APP_COLOR=red -n config-map-from-dir
configmap/color-config-map created
```

### 3. Create new project config-map from directory
```bash
$ kubectl create configmap color-config-map-dir --from-file=./config -n config-map-from-dir
configmap/color-config-map-dir created
```

### 4. GET All config-map
```bash
$ kubectl get configmaps -n config-map-from-dir
NAME                   DATA   AGE
color-config-map       1      21s
color-config-map-dir   2      12s
```

### 5. Describe all config-map 
```bash
$ kubectl describe configmap -n config-map-from-dir
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

### 6. Create Pod
```bash
$ kubectl apply -f pod.yml -n config-map-from-dir
pod/color-app created
```

### 7. Create service
```bash
$ kubectl expose pod color-app -n config-map-from-dir
service/color-app exposed
```


###  8. Accees application
Hit route url in Browser - You will observer following things
 - using URL : color-app-config-map-from-dir.2886795276-80-host18nc.environments.katacoda 
  HTML RED color Page, because in config map value of APP_COLOR is RED
 - using URL : color-app-config-map-from-dir.2886795276-80-host18nc.environments.katacoda/read_file
  HTML Red color Page with text_file.txt content in text area
## Deploy Pod using config-map-from-literals on Openshift/k8s

### Create new project config-map-from-literals
```bash
$ kubectl create ns config-map-from-literals
Now using project "config-map-from-literals" on server "https://2886795320-8443-cykoria05.environments.katacoda.com:443".
```

### create config-map from literals
```bash
$ kubectl apply -f pod.yml 
error: error parsing pod.yml: error converting YAML to JSON: yaml: line 9: mapping values are not allowed in this context

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
$ kubectl expose pod/color-app 
service/color-app exposed
```

###  Accees application
- using URL : color-app-config-map-from-literals.2886795320-80-cykoria05.environments.katacoda 
  HTML RED color Page, because in config map value of APP_COLOR is RED

  ### Delete All
```bash
$ kubectl delete all --all
```
## Deploy Pod using config-map-from-literals on Openshift/k8s

### 1. Create new project config-map-from-literals
```bash
$ kubectl create ns config-map-from-literals
Now using project "config-map-from-literals" on server "https://2886795320-8443-cykoria05.environments.katacoda.com:443".
```

### 2. create config-map from literals
```bash
$ kubectl apply -f pod.yml -n  config-map-from-literals
error: error parsing pod.yml: error converting YAML to JSON: yaml: line 9: mapping values are not allowed in this context

$ kubectl create configmap color-config-map --from-literal=APP_COLOR=red -n  config-map-from-literals
configmap/color-config-map created

$ kubectl get configmap -n  config-map-from-literals
NAME               DATA   AGE
color-config-map   1      5s

$ kubectl describe configmap color-config-map -n  config-map-from-literals
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

### 3. create POD
```bash
$ kubectl apply -f pod.yml -n  config-map-from-literals
pod/color-app created
```

### 4. create service
```bash
$ kubectl expose pod/color-app -n  config-map-from-literals
service/color-app exposed
```

###  5. Accees application
- using URL : color-app-config-map-from-literals.2886795320-80-cykoria05.environments.katacoda 
  HTML RED color Page, because in config map value of APP_COLOR is RED
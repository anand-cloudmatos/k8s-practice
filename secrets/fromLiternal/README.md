## Deploy Pod using secrets-from-literals on Openshift/k8s

### Create secret
```
$ kubectl create secret generic color-secret  --from-literal=APP_COLOR=red
secret/color-secret created

$ kubectl get secrets 


$ kubectl describe secret color-secret 
Name:         color-secret
Namespace:    default
Labels:       <none>
Annotations:  <none>

Type:  Opaque

Data
====
APP_COLOR:  3 bytes

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


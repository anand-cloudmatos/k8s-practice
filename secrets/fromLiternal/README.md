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
### Get Secret YAML
```bash
$ kubectl get secret color-secret -o yaml
apiVersion: v1
data:
  APP_COLOR: cmVk
kind: Secret
metadata:
  creationTimestamp: "2021-12-10T03:17:14Z"
  name: color-secret
  namespace: default
  resourceVersion: "123063"
  uid: 1f354fe9-bba8-4fd6-be31-9598ebb543bc
type: Opaque
```

### Decypt Secret Data
```bash
$ echo cmVk| base64 -d
```

### create POD
```bash
$ kubectl apply -f pod.yaml 
pod/color-app created
```
### Check ENV variable in POD
```bash
kubectl exec -i -t color-app -- env | grep APP
```

### create service
```bash
$ kubectl expose pod/color-app  --type=NodePort
service/color-app exposed
```

###  Accees application
```
Access application using <minikube-ip>:<nodeport>
```
  ### Delete All
```bash
$ kubectl delete all --all
```
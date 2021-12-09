## Labels in Openshift/k8s using kubectl run

### Create POD with label app=hello
```bash
$ kubectl run hello --image=openshift/hello-openshift --labels=app=hello
pod/hello created
```

### Show Labels
```bash
$ kubectl get pods --show-labels
NAME    READY   STATUS    RESTARTS   AGE   LABELS
hello   1/1     Running   0          30s   app=hello
```

### Add label tier=frontend to existing resource 
```bash
$ kubectl label pod hello tier=frontend
pod/hello labeled

$ kubectl get pods --show-labels
NAME    READY   STATUS    RESTARTS   AGE   LABELS
hello   1/1     Running   0          2m    app=hello,tier=frontend
```

### Update label
```bash
$ kubectl label pod hello tier=backend --overwrite
pod/hello unlabeled

$ kubectl get pods --show-labels
NAME    READY   STATUS    RESTARTS   AGE     LABELS
hello   1/1     Running   0          2m44s   app=hello,tier=backend
```

### Remove label
```bash
$ kubectl label pod hello tier-
pod/hello unlabeled

$ kubectl get pods --show-labels
NAME    READY   STATUS    RESTARTS   AGE     LABELS
hello   1/1     Running   0          3m53s   app=hello
```

### Delete Pod
```bash
$ kubectl delete po hello 
pod "hello" deleted
```
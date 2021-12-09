## Equality Base Labels in Openshift/k8s

### Create POD with label app=hello
```bash
$ kubectl run hello --image=openshift/hello-openshift --labels=app=hello,env=dev,tier=frontend
pod/hello created

$ kubectl run nginx --image=nginx --labels=tier=frontend,app=nginx,env=prod
pod/nginx created

$ kubectl get po --show-labels
NAME    READY   STATUS              RESTARTS   AGE   LABELS
hello   1/1     Running             0          14s   app=hello,env=dev,tier=frontend
nginx   0/1     ContainerCreating   0          4s    app=nginx,env=prod,tier=frontend
```

### Filter pod based on Equality based Labels
```bash
$ kubectl get po -l env=dev
NAME    READY   STATUS    RESTARTS   AGE
hello   1/1     Running   0          38s

$ kubectl get po -l env=dev --show-labels
NAME    READY   STATUS    RESTARTS   AGE   LABELS
hello   1/1     Running   0          48s   app=hello,env=dev,tier=frontend

$ kubectl get po -l env=prod --show-labels
NAME    READY   STATUS    RESTARTS   AGE   LABELS
nginx   1/1     Running   0          50s   app=nginx,env=prod,tier=frontend

$ kubectl get po -l env!=prod --show-labels
NAME    READY   STATUS    RESTARTS   AGE    LABELS
hello   1/1     Running   0          114s   app=hello,env=dev,tier=frontend

```

### Filter pod based on Set based Labels 
```bash
$ kubectl get po -l 'env in (prod)' --show-labels
NAME    READY   STATUS    RESTARTS   AGE     LABELS
nginx   1/1     Running   0          2m25s   app=nginx,env=prod,tier=frontend

$ kubectl get po -l 'env in (prod,dev)' --show-labels
NAME    READY   STATUS    RESTARTS   AGE     LABELS
hello   1/1     Running   0          2m41s   app=hello,env=dev,tier=frontend
nginx   1/1     Running   0          2m31s   app=nginx,env=prod,tier=frontend

$ kubectl get po -l 'env notin (prod)' --show-labels
NAME    READY   STATUS    RESTARTS   AGE     LABELS
hello   1/1     Running   0          3m16s   app=hello,env=dev,tier=frontend

```

### Delete Pod
```bash
$ kubectl delete po hello 
pod "hello" deleted
```
## Liveness and Readiness Healthcheck in Openshift/k8s


### Create POD  using liveness probe using exec type
```bash
$ kubectl apply -f exec-liveness.yaml

$ kubectl describe pod liveness-exec 
FirstSeen    LastSeen    Count   From            SubobjectPath           Type        Reason      Message
--------- --------    -----   ----            -------------           --------    ------      -------
24s       24s     1   {default-scheduler }                            Normal      Scheduled   Successfully assigned liveness-exec to worker0
23s       23s     1   {kubelet worker0}   spec.containers{liveness}   Normal      Pulling     pulling image "k8s.gcr.io/busybox"
23s       23s     1   {kubelet worker0}   spec.containers{liveness}   Normal      Pulled      Successfully pulled image "k8s.gcr.io/busybox"
23s       23s     1   {kubelet worker0}   spec.containers{liveness}   Normal      Created     Created container with docker id 86849c15382e; Security:[seccomp=unconfined]
23s       23s     1   {kubelet worker0}   spec.containers{liveness}   Normal      Started     Started container with docker id 86849c15382e
```

### Create POD  using liveness probe using HTTP type
```bash
$ kubectl apply -f http-liveness.yaml

# After 10 seconds, view Pod events to verify that liveness probes have failed and the container has been restarted:
$ kubectl describe pod liveness-http
```

### Create POD using liveness & rediness probe using TCP type
```bash
$ kubectl apply -f https://k8s.io/examples/pods/probe/tcp-liveness-readiness.yaml

$ kubectl describe pod  tcp-liveness-readiness
```

### Delete All
```bash
$ kubectl delete all --all
```
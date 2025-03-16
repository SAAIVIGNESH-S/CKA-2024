## Check out the task.md file for the hands-on exercises

## Cheatsheet for Kubernetes commands:
https://kubernetes.io/docs/reference/kubectl/quick-reference/

### Replication Controller (deprecated)
can manage only the pods that are created using it  
load balancing between the replicas is done by the replication conroller manager
https://kubernetes.io/docs/concepts/workloads/controllers/replicationcontroller/

```YAML
apiVersion: v1
kind: ReplicationController
metadata:
  name: nginx-rc
  labels:
    env: demo
spec:
  template:
    metadata:
      name: nginx-pod
      labels:
        env: demo
    spec:
      containers:
      - name: nginx-container
        image: nginx
  replicas: 3
```


### Replicaset
can manage existing pod as well  
https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/

![image](https://github.com/piyushsachdeva/CKA-2024/assets/40286378/3e9792d4-1127-44b4-a6ec-cdc2a82219e3)

(apiVersion is apps/v1 because explain gives the group as apps and version is v1)  
(manages the pod that matches the label env:demo)
```YAML
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nginx-rs
  labels:
    env: demo
spec:
  template:
    metadata:
      name: nginx-pod
      labels:
        env: demo
    spec:
      containers:
      - name: nginx-container
        image: nginx
  replicas: 3
  selector:
    matchLabels:
      env: demo
```
  
scale the replicas by modifying and applying the yaml  
edit the replicaset directly `kubectl edit rs/<replica_set>`  
using the imperative way `kubectl scale --replicas=<count> <replica_set>`


### Deployment
adds additional functionality to the replicaset  
can perform rolling updates (upgrade a pod in rs, while the other pod can serve old version)  
can also rollback changes to a particular version  
https://kubernetes.io/docs/concepts/workloads/controllers/deployment/

![image](https://github.com/piyushsachdeva/CKA-2024/assets/40286378/b888d272-c623-4a00-8381-45c25ce9d9c0)

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deploy
  labels:
    env: demo
spec:
  template:
    metadata:
      name: nginx-pod
      labels:
        env: demo
    spec:
      containers:
      - name: nginx-container
        image: nginx
  replicas: 3
  selector:
    matchLabels:
      env: demo
```

changing to a different container `kubectl set image deploy/<deploy_name> <container_name>=<image_name>:<image_version>`  
view revision history `kubectl rollout history deploy/<deploy_name>`  
rollback the changes `kubectl rollout undo deploy/<deploy_name>`

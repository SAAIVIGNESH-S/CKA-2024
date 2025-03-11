## Check out the task.md file for day07 task details

## Different ways of creating a Kubernetes object
- Imperative way ( Through command or API calls)  
    kubectl run <pod_name> --image=<image_id>:<image_tag> (tag is optional)  
    kubectl run nginx-pod --image=nginx:latest
- Declarative way ( By creating manifest files)

![image](https://github.com/piyushsachdeva/CKA-2024/assets/40286378/b038c4d3-87b7-474d-a3aa-5983d978f885)

kubectl run <pod_name> --image=<image_id>:<image_tag> --dry-run=client -o yaml/json (gives the yaml/json of the command by doing a dry run without applying the changes)  

kubectl explain pod (to get the version)  
kubectl delete pod <pod_name>  
kubectl describe pod <pod_name>  

kubectl create/apply -f <yaml/dir>
- apply can update existing resources if they already exist or create a new one, apply can be run multiple times without changing the outcome after the first run (used to create or update the resource)
- create will fail if the resource already exists (used only to create a resource)

kubectl edit pod <pod_name> (applies changes automatically as changes is made in resource)  
kubectl exec -it <pod_name> -- sh/bash  
kubectl get pod <pod_name> --show-labels

apiVersion, kind, metadata, spec are basic fields (supports only specific key)  
name key in the metadata key will be the name of the pod  
labels alone can have any key value pair  

specify the list of items  
students:  
  &ndash; name: a  
    age: 20  
  &ndash; name: b  
    age: 22  

## Below is the sample pod YAML used in the video:

```YAML
# This is a sample pod yaml

apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    env: demo
    type: frontend
spec:
  containers:
  - name: nginx-container
    image: nginx
    ports:
    - containerPort: 80
```


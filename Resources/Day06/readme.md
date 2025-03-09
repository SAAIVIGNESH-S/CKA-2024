### Please follow task.md for the Day6 assignment

**Documentation followed in this video:**
- Install [kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl)
- Kind cluster [docs](https://kind.sigs.k8s.io/docs/user/quick-start/)
- kind example config [yaml](https://raw.githubusercontent.com/kubernetes-sigs/kind/main/site/content/docs/user/kind-example-config.yaml)

**Below domains and all of its sub-domains are allowed to be referred in the exam**
- https://kubernetes.io/docs
- https://kubernetes.io/blog/
- Kubernetes cheat sheet : https://kubernetes.io/docs/reference/kubectl/quick-reference/  

**Create a cluster using kind**  
kind create cluster --image kindest/node:v1.32.2@sha256:f226345927d7e348497136874b6d207e0b32cc52154ad8323129352923a3142f --name &lt;cluster_name&gt;  

**Get the details of a cluster**  
kubectl cluster-info --context &lt;cluster_name&gt;    

**Create a cluster using kind with custom configuration**  

kind: Cluster  
apiVersion: kind.x-k8s.io/v1alpha4  
nodes:  
&ndash; role: control-plane  
&ndash; role: worker  
&ndash; role: worker  

kind create cluster --image kindest/node:v1.32.2@sha256:f226345927d7e348497136874b6d207e0b32cc52154ad8323129352923a3142f --name &lt;cluster_name&gt; --config config.yaml

**View the available contexts**  
kubectl config get-contexts  

**Switch between available contexts**  
kubectl config use-context &lt;cluster_name&gt;

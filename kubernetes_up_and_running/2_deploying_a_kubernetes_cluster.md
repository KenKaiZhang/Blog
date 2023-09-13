# 2. Deploying a Kubernetes Cluster

**_`kubectl`, the official command-line tool for interacting with Kubernetes API_**

## Some Commands

`kubectl get componentstatuses`: simple diagnostic for the cluster

- **controller-manager**: running various controllers that regulate behavior in the cluster
- **scheduler**: places different Pods into different nodes in the cluster
- **etcd-X**: storage for the cluster where all API objects are stored

`kubectl get nodes`: list out all of the nodes in the cluster

`kubectl describe nodes node1`: get more information aboute a specific node

`kubectl get daemonSets --namespace=kube-system kube-proxy`: shows information about a DaemonSet running in the `kube-system` namespace in a cluster

`kubectl get deployments --namespace=kube-system core-dns`: shows information about the deployments named `core-dns` in the `kube-system` namespace in a cluster

### Note

Nodes are seperated into **control-plane** nodes that contain containers like the API server, scheduler, etc. which manage the cluster and the worker nodes where the container runs

## Cluster Components

The **Kubernetes proxy** must be on every node in the cluster and is responsible for routing network traffic to load balanced services in the cluster

- "saved" in a Kubernetes API object `DaemonSet`

Kubernetes replicateion service is hosted on its **DNS** server that provides naming and discovery for the services that are defined in the cluster

**Kubernetes UI** provides a GUI to visualize the clusters

# Common `kubectl` Commands

**_Used to create objects and interact with the Kubernetes API_**

`kubectl --namespace=other-space`: refrences the objects in the `other-space` namespace (default is `default`)

- namespace is how Kubernetes organizes its objects in a cluster
  - partitions the cluster
- `--any-namespace` allows interaction with all namespaces

---

`kubectl config set-context new-context --namespace=other-space`: create a new context

- context is how clients can interact with kubernetes through `kubectl`
- helps shorten commands by setting default values (cluster, namespace, and/or user)
- by default, the `default` namespace is used so context permenantly changes that

`kubectl config use-context new-context`: use `new-context`

```commandline
Example

// Retrieve list of pods and deployments in namespace dev repectively
kubectl get pods -n dev
kubectl get deployments -n dev

// Create a new context targeting namespace dev
kubectl config set-context context-dev -n dev
kubectl config use-context context-dev

// Retrieves the same results as the first two commands
kubectl get pods
kubectl get deployments

```

---

`kubectl get <resource-name>`: get a listing of all resources in the current namespace

- add an `<object-name>` to specifiy a resource
- resources as in `pods`, `deployments`, `services`, etc.

`kubectl describe <resource-name> <object-name>`: provides details on a resource named `<object-name>`

`kubectl explain <resource-name>`: lists supported fields for the resource

---

`kubectl apply -f <file-name>.yaml`: creates a new Kubernetes object using a _yaml_ file (_json_ works too)

- add `--dry-run` flag to print the objects in the terminal without sending them to the server to see what happens without making any changes
- adding `view-last-applied` will show the last state that was applied to the object
  - `edit-last-applied`
  - `set-last-applied`

---

`kubectl delete -f <file-name>.yaml`: deletes an object (there will be no prompt)

- `kubectl delete <resource-name> <obj-name>` will also delete the object

---

`kubectl label <resource-name> <obj-name> color=red`: sets a color label to the object

`kubectl label <resource-name> <obj-name> color-`: removes the color label from the object

---

`kubectl logs <pod-name>`: show logs of a running pod

`kubectl exec -it <pod-name> -- bash`: execute a command in a running container and provides an interactive shell

`kubectl attach -it <pod-name>`: allows inputs to be send to the running process

`kubectl cp <pod-name>:</path/to/remote/file> </path/to/local/file>`: copies a file from the pod to the local machine

`kubectl port-foward <pod-name> 8080:80`: opens up connection that forwards traffic from local machine on port 8080 to remote port 80

---

`kubectl get events`: shows a list of the latest 10 events in a namespace

- add `--watach` to see a stream

# ReplicaSets

**_Multiple replicas of a container for redundancym, scale, sharding_**

A cluster wide Pod manager that ensures the right types and number of Pods are running at all times

- Pods are automatically resheduled under certain failure conditions

## Reconciliation Loops

**Desired state**: the state you want

- desired number of replicas and the definitions of the Pod to replicate

**Observed/current state**: current state of the system

- "there are only X \<pod-name\> Pods running"

Reconciliation loop constantly runs and observes the current state of the environment and takes action to maintain the observed state to match the desired state

- create new Pods to match the desired X Pods

## Relating Pods and ReplicaSets

**_ReplicaSet do not own the Pods they create_**

Uses label queries to identify the set of Pods they should be managing

To make replicas of a previously created Pod, it is better to create a new ReplicaSet with a desired replica count and same Pod template (where the labels and the containers are the same)

If a Pod is unhealthy, do not delete the Pod, but simply modify the label so the ReplicaSet will disassociate it (quaranteen)

## Creating a ReplicaSet

_Example ReplicaSet configuration_

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  labels:
    app: kuard
    version: "2"
  name: kuard
spec:
  replicas: 1
  selector:
    matchLabels:
      app: kuard
      version: "2"
  template:
    metadata:
      labels:
        app: kuard
        version: "2"
    spec:
      containers:
        - name: kuard
          image: "gcr.io/kuar-demo/kuard-amd64:green"
```

Run `kubectl apply -f <replica-set>.yaml` to submit a ReplicaSet

From the example above, a blank Kubernetes environment will recognize the `kuard` Pod does nto exist adn create a new Pod based on the template

Use `kubectl describe rs <replica-set>` to view the object

Use `kubectl get pods <pod-name> -o=jsonpath='{.metadata.ownerReferences[0].name}'` to see what ReplicaSet is managing the Pod

_Remember you Pods managed by a ReplicaSet are identified through labels_

## Scaling ReplicaSets

It is possible to scale up and down by updating the `spec.replicas` key in a ReplicaSet object

- Can be done with a command or YAML/JSON file
  - `kubectl scale replicasets kuard --replicas=4`
  - ```yaml
      ...
      spec:
          replicas: 3
      ...
    ```

By setting a `min` and `max` count of replications, it is possible for Kubernetes to autoscale based on the range and the allocated resources

- `kubectl autoscale rs kuard --min=2 --max=5 --cpu-percent=80`

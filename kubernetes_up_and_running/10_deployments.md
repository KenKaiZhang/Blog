# Deployments

**_Manages new verision releases and enables easy movement between versions_**

Manages ReplicaSets

It is possible to scale the Deployment and the ReplicaSet managed using the `scale` command

- If the desired replica of the Deployment than the ReplicaSet, the system will automatically readjust the replica back to the desired

```
$ kubectl scale deployments <deployment-name> --replicas=2
$ kubectl scale replicasets <pod-name> --replicas=1
```

_Will keep the replica count match the top level (deployment)_

## Creating Deployments

Similar to ReplicaSet spec but with a `strategy` object that dictates the different ways in which a rolout of a new software can proceed

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  annotations:
    deployment.kubernetes.io/revision: "1"
  creationTimestamp: "2023-08-31T20:03:03Z"
  generation: 3
  labels:
    run: kuard
  name: kuard
  namespace: default
  resourceVersion: "81715"
  uid: 3b883ca5-26fd-4752-930d-9883d5096462
spec:
  progressDeadlineSeconds: 600
  replicas: 1
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      run: kuard
  strategy:
    rollingUpdate:
      maxSurge: 25%
      maxUnavailable: 25%
    type: RollingUpdate
  template:
    metadata:
      creationTimestamp: null
      labels:
        run: kuard
    spec:
      containers:
        - image: gcr.io/kuar-demo/kuard-amd64:blue
          imagePullPolicy: IfNotPresent
          name: kuard
          resources: {}
          terminationMessagePath: /dev/termination-log
          terminationMessagePolicy: File
      dnsPolicy: ClusterFirst
      restartPolicy: Always
```

## Managing Deployments

Check out `kubectl describe deployments <deployment-name>`

Look for **`OldReplicaSets`** and **`NewReplicaSet`** which indicates if a ReplicaSet objects the Deployment is currently managing

- `OldReplicaSets` will be a value if there is a rollout otherwise `<none>`

## Updating Deployments

Most common operations are scaling and updates

### Scaling a Deployment

Best practice is to update the YAML file and then `apply` the changes

### Updating a Container Image

Best practice is to update the YAML file and then `apply` the changes

- Make sure to update the annotate template so a record is kept

Updating the Deployment will trigger an automatic rollout that can be monitored with `kubectl get replicasets -o wide`

- use `kubectl rollout pause deployments kuard` and `kubectl rollout resume deployments kuard` to pause and resume respectively

### Rollout History

Use `kubectl rollout history deployment kuard` to check the Deployment history

It is possible to rollback with `kubectl rollout undo deployments <deployment-name>` whihc will undo the last release

Add `revisionHistoryLinmit` in the Depolyment spec to customize the history size (defualt 10)

## Deployment Strategies

**_`Recreate` and `RollingUpdate` are the two available rollout strategies_**

**`Recreate`** updates the ReplicaSet to use the new image and terminates all Pods associated with the Deployment

- causes the ReplicaSet to recreate the Pods
- fast and simple but a lot of downtime

**`RollingUpdate`** allows a new version to be rolled out while the service runs by updating a fewPods at a time

## Deleting a Deployment

`kubectl delete deployments kuard` or `kubectl delete -f <deployment>.yaml`

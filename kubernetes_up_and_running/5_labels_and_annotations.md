# Labels and Annotations

**Labels**: arbitrary key/value pairs that can be attached to Kubernetes objects that are useful for identifying information

- foundation of group objects

**Annotations**: key/value pairs designed to hold nonidentifying information that tools and libraries can leverage

## Labels

**_A way to group, view, and operate on objects_**

To create Pods with labels, run `kubectl run <pod-name> --image=<image-location> --labels="<key>=<value>"`

To create Deployments with labels, there are a few steps:

1. Create a deployment with `kubectl create deployment <name> --image=<image-location>`
2. Overwrite the labels with `kubectl labels --overwrite deployment <name> <key>=<value>`

Example of what deployments with labels look like

```
$ kubectl get deployments --show-labels
NAME             READY   UP-TO-DATE   AVAILABLE   AGE     LABELS
alpaca-prod      1/1     1            1           2m44s   app=alpaca,env=prod,var=1
alpaca-test      1/1     1            1           2m25s   app=alpaca
bandicoot-prod   1/1     1            1           2m9s    app=bandicoot,env=prod,var=2
bandicoot-test   1/1     1            1           2m15s   app=bandicoot,env=test,var=2
```

The `-L <label-key>` flag with `kubectl get` will list out just the values

```
$ kubectl get deployments -L app
NAME             READY   UP-TO-DATE   AVAILABLE   AGE     LABELS
alpaca-prod      1/1     1            1           2m44s   alpaca
alpaca-test      1/1     1            1           2m25s   alpaca
bandicoot-prod   1/1     1            1           2m9s    bandicoot
bandicoot-test   1/1     1            1           2m15s   bandicoot
```

Labels can be removed with `kubectl label <resource> <object-name> <label-key>-`

`--selector` flag from `kubectl get` can filter out resources that have the label provided

- allows selecting multiple labels by using a comma
- allows selecting a range of values for a key ex: `--selector="app in (alpaca,bandicoot)"`

It is posisble to pass in an object to select

```yaml
selector:
  matchLabels:
    app: alpaca
  matchExpressions:
    - { key: var, operator: In, values: [1, 2] }
```

which is equivilent to `app=alpaca,var in (1,2)`

## Annotations

Provides more information on where an object came from, how to use it, or the policies around it

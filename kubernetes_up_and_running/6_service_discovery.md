# Service Discovery

**_Kubernetes is a system of placing Pods in nodes, make sure they are up and running, and rescheduling them as needed_**

**service discovery**: tools that help solve the problem of finding which processes are listening at which addresses for which services

- Domain Name System (DNS) is an internet service discovery

## The Service Object

**_The Kubernetes service discovery_**

Created with `kubectl expose`

Example of creating 2 deployments and services

```
$ kubectl create deployment alpaca-prod --image=gcr.io/kuar-demo/kuard-amd64:blue --port=8080
$ kubectl scale deployment alpaca-prod --replicas 3
$ kubectl expose deployment alpaca-prod

$ kubectl create deployment bandicoot-prod --image=gcr.io/kuar-demo/kuard-amd64:blue --port=8080
$ kubectl scale deployment bandicoot-prod --replicas 2
$ kubectl expose deployment bandicoot-prod

$ kubectl get services -o wide
NAME             TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE    SELECTOR
alpaca-prod      ClusterIP   10.101.140.60    <none>        8080/TCP   29s    app=alpaca-prod
bandicoot-prod   ClusterIP   10.102.197.152   <none>        8080/TCP   6s     app=bandicoot-prod
kubernetes       ClusterIP   10.96.0.1        <none>        443/TCP    101s   <none>
```

- Taking `alpaca-prod ClusterIP 10.101.140.60 <none> 8080/TCP 29s app=alpaca-prod` as an example, there is a **service** named `alpaca-prod` that is exposed internally on port 8080 with a ClusterIP of 10.101.140.60 and when called, it selects pods with the label `app=alpaca-prod`

Port forward an `alpaca` pod to access the service

```
$ ALPACA_POD=$(kubectl get pods -l app=alpaca -o jsonpath='{.items[0].metadata.name}')
$ kubectl port-forward $ALPACA_POD 48858:8080
```

1. Gets all pods with label `app=alpaca` and outputs it as a JSONPath (JSON object query language)
2. Sets `ALPACA_POD` as the name of the first result (Pod) returned
3. Port fowards the result to 48858

### Service DNS

Since the cluster IP is virtual and stable, it is given a DNS address

DNS service is installed when the cluster is first created and is exposed to Pods in the cluster

Example DNS name `<service-name>.<service-namespace>.svc.<cluster-domain-name>`

### Readiness Check

The Service object can track which Pods are ready via the a readiness check

_You can edit a object with `kubectl edit <resource> <object-name>`_

**_Needs revistiting..._**

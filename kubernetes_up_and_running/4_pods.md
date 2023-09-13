# Pods

**_A collection of application containers and volumes running in the same execution environment_**

Smallest deployable artifact in a Kubernetes cluster (all containers in a Pod land on the same machine)

- containers have individual cgroups but share:
  - namespaces
  - IP address and port space
  - host name
  - communication channels
- different Pods are isolated from one another

Host containers that can scale together in the same Pod

- "will these containers work correctly if they land on different machines"
  - **yes**: different pods
  - **no**: same pod

## The Pod Manifest

**_A JSON/YAML configuration file that defines a Pod's resources and constraints_**

Pods are scheduled to nodes by the API and do not move (must be destroyed and rescheduled)

```yaml
// Example of a Pod manifest

apiVersion: v1
kind: Pod
metadata:
  name: new-pod
spec:
  containers:
    - image: gcr.io/kuar-demo/kuard-amd64:blue
      name: kuard
      ports:
        - containerPort: 8080
          name: http
          protocol: TCP
```

### Creating a Pod

Can be done by using an image like:

```
$ kubectl run <pod-name> --image=<public-image-repository>
pod/<pod-name> created

$ kubectl get pod <pod-name>
NAME         READY   STATUS    RESTARTS   AGE
<pod-name>   1/1     Running   0          27s
```

or by making a Pod manifest such as the one above

## Running Pods

It is possible to start a pod with a manifest by running `kubectl apply -f <pod-manifest>.yaml`

- This will submit the manifest to the Kubernetes API server and the Pod will be scheduled on a healthy node

When listing pods with `kubectl get pods`, the status `Pending` indicates the pod has not been scheduled

Run `kubectl describe pods <pod-name>` to get even more details on a specific pod

## Accessing Pods

**Port forwarding** allows access to the Pod through a web browser

- `kubectl port-forward <pod-name> <local-port>:<pod-port>` forwards the pod's port to http://localhost:\<local-port\>

View the events performed bu a Pod live with `kubectl logs <pod-name> -f`

Start an interactive session with `kubectl exec -it <pod-name> ash`

Copy files (securely) from

- local machine to remote: `kubectl cp <pod-name>:/path/to/file ./path/to/save/file/locally`
- remote machine to local: `kubectl cp /path/to/file <pod-name>:/path/to/save/file/remotely`

## Health Checks

**_Applications are automatically kept alive using a process health check_**

Liveness health checks run application-specific logic to make sure the application is alive and well

- must be defined in manifest since they are unique to the application

```yaml
...
spec:
    containers:
        - image: <image-location>
          name: <container-name>
          livenessProbe:
            httpGet:
                path: /healthy
                port: 8080
            initialDelaySeconds: 5
            timeoutSeconds: 1
            periodSeconds: 10
            failureThreshold: 3
        ports:
...
```

Adding `livenessProbe` creates a probe in the Pod to perfom and HTTP `GET` request against the `/healthy` endpoint on port `8080` in the container

- probe will not startup until 5s all containers in the Pod are created
- probe has 1s to respond with a status code between 200 and 400
- probe will be called on every 10s and after 3 failed attempts, the container will fail and restart

The process can be viewed through localhost (assuming you port forward)

_There is also a readiness probe that checks if a container is ready to server user request. If not, it is removed from the service load balancers_

## Resource Management

It is possible to request a minimum and a cap on container allocated resources

Add a resources section to set a minimum and a limit on the allocated resources for the container

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: new-pod
spec:
  containers:
    - image: <image-location>
      name: new-container
      resources:
        requests:
          cpu: "500m"
          memory: "128Mi"
        limits:
          cpu: "1000m"
          memory: "254Mi"
      ports:
        - containerPort: 8080
          name: http
          protocol: TCP
```

to set the maximum allowed resources for the container

This means any actions that allocates more memory than allowed by the manifest (such as mallocing over 256MB) will cause the container to fail

## Persisting Data with Volumes

**_Makes sure that a new container can pick up data at the state the old one crashed in_**

Volume outlives the containers in a Pod and can be consumed by any number of containers

Add a volume by

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: new-pod
spec:
  volumes:
    - name: "pod-data"
      hostPath:
      path: "/var/lib/pod"
  containers:
    - image: <image-location>
      name: new-container
      volumeMounts:
        - mountPath: "/data"
        name: "pod-data"
      ports:
        - containerPort: 8080
        name: http
        protocol: TCP
```

`volumes` defines all of the volumes that may be accessed by containers in the Pod

`volumeMounts` defines the volume to be mounted to the container and the container path to mount it

### Why to use volumes with pods

1. Communication/synchronization
2. Cache
3. Persistent data
4. Mounting the host filesystem
5. Pesisting data using remote disks
   - ```yaml
     volumes:
       - name: pod-data
         nfs:
           server: nfs.server.location
           path: "/exports"
     ```

A final look at an example manifest including all the tools above

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: "new-pod"
spec:
  volumes:
    - name: "pod-data"
      nfs:
        server: nfs.server.location
        path: "/exports"
  containers:
    - image: <image location>
      name: "pod-container"
      ports:
        - containerPort: 8080
          name: http
          protocol: TCP
      resources:
        requests:
          cpu: "500m"
          memory: "128Mi"
        limits:
          cpu: "1000m"
          memory: "256Mi"
      volumeMOunts:
        - mountPath: "/data"
          name: "pod-data"
      livenessProbe:
        httpGet:
          path: /healthy
          port: 8080
        initialDelaySeconds: 5
        timeoutSeconds: 5
        periodSeconds: 10
        failureThreshold: 3
      readinessProbe:
        httpGet:
          path: /ready
          port: 8080
        initialDelaySeconds: 30
        timeoutSeconds: 1
        periodSeconds: 10
        failureThreshold: 3
```

# Definitions

Check out [Kubernetes Glossary](https://kubernetes.io/docs/reference/glossary/?fundamental=true) for full list

**Cluster**: a collection of **nodes** that gets managed through a control plane

**Node**: a worker machine (VM/physical) with daemons and services necessary to run Pods assigned to it

- usually `kubelet` and a **CRI** is inclued in the daemon

**Pod**: a collection of **containers**

**Container**: a lightweight and portable executable **image** that contains software and all its dependencies

**Image**: a way of packaging software that holds a set of software needed to run an application

**CRI**: an interface for `kubelet` to communicate with **Container Runtime**

**Container Runtime**: a componenet responsible for managing the execution and lifecycle of containers within a Kubernetes environment

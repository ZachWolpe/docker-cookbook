# Kubernetes (K8s)

Kubernetes is a container orchestration system that allows you to run and manage containers at scale. It is an open source project created by Google.

Kubernetes is essentially a set of _APIs_ in containers that runs on top of Docker.

Provides an `API/CLI` to manage containers across multiple hosts/servers.

----
# Orchestration

_Orchestration:_ The process of automating the deployment, management, scaling, networking, and availability of container-based applications. 

Concretely, orchestration takes a series of servers (or nodes), and turns them into a single pool of resources. This pool of resources is then used to run containers.


---
# Why Orchestration?

Orchestration is next step to DevOps. A simple heuristic is given by the formula:

``Servers + Change Rate = Benefit of Orchestration``


----
# Kubernetes Architecture

Kubernetes is a set of APIs that run on top of Docker. It is a set of containers that run on top of Docker.

----
# Kubernetes or Docker Swarm?

_Swarm_: Easy to deploy/manage, but lacks features.

_Kubernetes_: More features & flexibility, but more complex to deploy/manage.


**Swarm**

Advantages:

- Comes with Docker.
- Single vendor container platform.
- Easy to deploy/manage.
- Works well out of the box.
- Lightweight and runs wherever docker runs.
- Runs anywhere Docker runs:
    - local, cloud, datacentre
    - ARM, Windows, 32-bit, etc.
- Secure by default.
- Easier to troubleshoot.

Disadvantages:

- Lacks features, 

**Kubernetes**

Advantages:

- "level up" from Swarm.
- Cloud will deploy/manage Kubernetes for you.
- Infrastucture vendors are building Kubernetes into their products.
- Widespread adoption. 
- Flexible: covers wide range of use cases.
- _"No one ever got fired for buying IBM."_


----
# Kubernetes Concepts

- _Kubernetes_, or _K8s_ or _Kube_, is the entire orchestration system.
- _Kubectl_ is the CLI configuration tool for Kubernetes (pronounced _kube control_).
- _Node_ is a single server in the Kubernetes cluster.
- _Kubelet_ is the agent that runs on each node in the cluster. It is responsible for starting/stopping containers.
- _Pod_ is a group of containers that are deployed together on the same host (node). A pod is the smallest unit of deployment in Kubernetes.
- _Control Plane_ the set of containers that run on the master node. It is responsible for managing the cluster, equivalent to the Swarm manager.
- _Service_: network endpoint to connect to a pod.
- _Namespace_: Filtered group of objects in cluster.

**Master Nodes**
- etcd
- API
- Scheduler
- Controller Manager
- Core DNS

**Nodes**
- Kubelet
- Kube-proxy


----
# Basic Commands

`kubectl get nodes` - list nodes in cluster
`kubectl get pods` - list pods in cluster
`kubectl run <name> --image=<image>` - run a pod
`kubectl create deployment <name> --image=<image>` - run a pod
`kubectl describe pod <name>` - describe a pod
`kubectl delete pod <name>` - delete a pod
`kubectl logs <name>` - get logs for a pod
`kubectl apply -f <file>` - apply a configuration file


`run` is only for creating a single pod. `create` is for creating a deployment, which is a set of pods.


----
# Deployment

A deployment is a set of pods. A pod is a set of containers. A deployment is responsible for managing the pods. It does not create the pod directly but rather creates a replica set, which in turn creates the pods.

This allows us to achieve _rolling updates_ and _rollbacks_ (high availability). This process can be seen in the Kubernetes dashboard, or by running `kubectl get rs` or `kubectl get all`.


shutdown all kube processes: `sudo systemctl stop kubelet.service kube-proxy.service kube-controller-manager.service kube-scheduler.service`

Show all kube processes: `ps aux | grep kube`


----
# Scaling Replicas (Pods)

`kubectl scale deployment <name> --replicas=<number>` - scale a deployment

-----
# Exposing Kubernetes Services

A service is an endpoint that can be used to connect to a pod. It is a load balancer that sits in front of a set of pods, responsible for routing traffic to the pods.

_kubectrl expose_ creates a service for existing pods. _kubectl create service_ creates a service and a deployment.

A service is a stable address for pod(s). We need a service if we wish to connect pod(s).

_CoreDNS_ allows us to resolve services by name.

There are four types of services:
    - ClusterIP (default)
    - NodePort
    - LoadBalancer
    - ExternalName


----
# Kubernetes Services DNS

Kubernetes has its own DNS server, which is responsible for resolving service names to IP addresses. This is called _CoreDNS_.

`curl <hostname>` will resolve to the IP address of the service.

`curl <hostname>.<namespace>.svc.cluster.local` will resolve to the IP address of the service.


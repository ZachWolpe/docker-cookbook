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


----
# Inspect Kubernetes

`kubectl get all`:list all common resources.

`kubectl create deployment <name> --image=<image> --replicas 2`: create a deployment with 2 replicas.

Can also get specific resources, e.g. `kubectl get pods` or `kubectl get deployments`.

`kubectl get --help` for more info.


`kubectrl logs <name>`: get logs for a pod.

`kubectl describe pod <name>`: describe a pod.

`kubectl exec -it <name> --bin/bash`: get a shell inside a pod.

`stern <name>`: tail logs for a pod.



----
# Management Techniques

Kubernetes is unopinionated (whereas swarm has many best practices to follow). Here are some tips on managing `Kubernetes` workflows.

_Resource Generators_ are tools that generate configuration files for Kubernetes. They are useful for generating configuration files for complex applications. Every resource in Kubernetes has a _spec_.

For example

`kubectrl create deployment sample --image nginx --dry-run=client -o yaml`

- `--dry-run-client -o yaml`: shows the output of the command without actually running it.

----
# Imperative vs Declarative

- _Imperitive_: focus on _how_ a program operates.
- _Declarative_: focus on _what_ program should accomplish.

#### Imperative

Imperative is about giving explicit instructions on how to do something.

- Easier starting out.
- Great for learning a new tool.
- Harder to maintain.
- Difficult to automate.


Examples:
    - `kubectl run`
    - `kubectrl create deployment`
    - `kubectrl update`


#### Declarative

Declarative is about describing the desired state of the system.

- Great for maintenace.
- Easier to automate.
- Harder to learn.


Examples:
    - `kubectl apply -f <file>`
    - `kubectl apply -f <directory>`


Largely done with `yaml` and `gitOps`.

#### 3 Management Approaches

**Imperative commands**

- Do everything line by line.
- Commands: `run, expose, scale, edit, create deployment, ...`
- Easy to learn, hard to manage over time.

**Imperative objects**

- Middle ground.
- Commands: `create -f file.yml, replace -f file.yml, delete, ...`
- Forces `yaml` for great documentation but allows for stepwise implementation.

**Declarative objects**

- Declarative obejcts: `apply -f file.yml` or `dir\`, or `diff`.
- Best for prod, easier to automate.
- Harder to understand and predict changes.


**Notes for Use**:

- Learn the imperative command line but move to declarative asap.
- Don't mix the three approaches.
- Best to move to the declarative as soon as possible.
- Move to a `git` model as soon as possible - storing `yaml` changes.
- Move towards `gitOps`/`DevOps` asap.



----
# Declarative Kubernetes YAML

- `kubectl apply -f <file.yaml>`: apply a configuration file.
- `kubectl apply -f <directory>`: apply all configuration files in a directory.
- `kubectl apply -f <url>`: apply a configuration file from a url.


Kubernetes configuration:

- `yaml` or `json` format.
- each file contains one or more manifests.
- each manifest describes an API object (deployment, job, secret).
- each manifest needs four parts (root key:values in the file).
    - _apiVersion_
    - _kind_
    - _metadata_
    - _spec_



_apiVersion_: the version of the Kubernetes API that we are using. This is important because the API changes over time. See `kubectl api-versions` for a list of available API versions.

_kind_: the type of object that we are creating. See `kubectl api-resources` for a list of available object types.

_metadata_: only name is required. This is a unique name for the object.

_spec_: the desired state of the object. This is where we define the object's configuration. This is the most important part of the configuration file.



#### Building Your YAML spec

- Use `kubectl create` to generate a template.
- Use `kubectl explain` to get more info on a resource.
- Use `kubectl explain <resource>.<field>` to get more info on a field.
- Use `kubectl explain <resource>.<field> --recursive` to get more info on a field and its children.


```yaml
    apiVersion: v1
    kind: Pod
    metadata:
        name:
        labels:
            app:
    spec:
        containers:
            - name:
              image:
              ports:
                - containerPort:      
```


#### Dry Run

- `--dry-run=client` will show the output of the command without actually running it.
- `--dry-run=server` will send the request to the server but not actually create the object.

The optional argument `-o yaml` will format the output in `yaml`.

- `kubectl diff` will show the difference between the current state and the desired state of the object.

*Labels and Label Selectors*

- Labels are key:value pairs that are attached to objects.
- Labels are used to select objects & filter objects. 


#### Next Steps and the Future of Kubernetes

Kubernetes is a fast moving project. We assume a container is _stateless_ - meaning without persistant data.

Tips:
    - Not recommended for first deployments.
    - Cloud databases are ideal.
    - Requires extensive additional work and testing.

**Persistant Data (Storage)**
    - Volumes:
        - Tied to a lifecycle of a Pod
        - All containers in a single Pod can share them
    - Persistent Volumes:
        - Tied to the lifecycle of a cluster
        - All Pods can share them
    -CSI (Container Storage Interface) plugins:
        - Access to storage through CSI APIs.
        - Cloud storage
        - NFS
        - etc.

**Ingress**

- None of our Service types work at OSI Layer 7 (HTTP). _Ingress_ is a way to route traffic to a Service based on the request's host and path.
- Ingress Controllers (optional) do this with 3rd parties proxies. They are not part of the Kubernetes project.

**CRDs and The Operator Pattern**

- You can add 3rd party Resources and Controllers.
- Kubernetes has become a platform.
- This extends Kubernetes API and CLI.
- A pattern is starting to emerge of using these together.
- Operator: automate deployment and management of complex apps: Databases, monitoring tools, backups and custom ingresses.

**Higher Deployment Abstractions**

- All our _Kubectl_ commands just talk to Kubernetes API.
- Kubernetes has limited built-in templating, versioning, tracking and app management.


**Templating YAML**

- Many of the deployment tools have templating options.
- You'll need a solution as the number of enviroments/apps grows.
- _Helm_ was the first winner in this space, but can be complex.
- Official _Kustomize_ feature works out-of-the-box.
- _docker app_ and _compose-on_kubernetes_ are Docker's approach.


**Kubernetes Dashboard**

- GUI for "upstream" Kubernetes.
- Clouds don't have it by default.
- Let's you view your resources/clusters and upload YAML etc.
- Safety first: documented cases of vulnerabilities through this dashboard.


**Namespaces & Context**

- Namespaces are a way to group resources.
- Virtual clusters/views.
- Can be used for security, resource quotas, etc.
- Not related to Docker/Linux namespaces.
- Built-in namespaces (run `kubectl get namespaces`) to hide system ops from the _kubectl_ users:
    - default
    - kube-system
    - kube-public
    - > `kubectl get namespaces`
    - > `kubectl get all --all-namespaces`
- Contexts are a way to switch between clusters and namespaces.
- See `~/.kube/config` file.


**Future of Kubernetes**

- Kubernetes is a platform for building platforms.
- Kubernetes _*"Needs to get boring"*_, focus on stability and security.
    - Improving features like `server-side dry-run`.
- Recent security audit has created a backlog.
- Strong push for better auditing and change management.
- _Helm 3.0_ (easier deployment, chart repos, libs).
- More declarative-style features.
- Better Windows Server support.
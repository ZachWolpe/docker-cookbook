# Swarm

How do we deal with the container lifecycle in a cluster?

Swarm is a server clustering solution built inside Docker. It is a native clustering solution for Docker.


----
# Manager vs Worker Nodes

## Manager Nodes

- Manage the cluster
- Maintain cluster state
- Schedules services
- Orchestrates worker nodes

## Worker Nodes

- Run containers
- Report back to manager nodes


----
# Getting Started


- See if swarm installed by looking at the  `Swarm: <status>` in: `docker info`
- Initialize swarm: `docker swarm init`
- View the swarm nodes: `docker node ls`
- `service` replaces `run` in swarm mode.
- get service details by running `docker service inspect <service name>`.
- `docker service ps <service name>` shows the tasks of the service.

Note that the `docker service update` command has many more options than the equivalent `docker run update` command. This is because it is built to be used in production, allow for zero downtime updates etc.


----
# Basic Commands

- `--driver overlay` creates a network that spans all the nodes in the swarm. Used for inter-container communication. Optional IPSec (AES) encryption.


----
# Routing Mesh

- Swarm mode has a built-in load balancer called the routing mesh.
- Routes ingress (incoming) packets for a Service to proper Task.
- Spans all nodes in Swarm.
- Uses IPVS from Linux kernel.
- Load balances Swarm Services across their Tasks.
- DNS Round Robin is used to load balance between nodes.
- Routing mesh is stateless (does not use session cookies).


----
# Stacks: Production Grade Compose

- Stacks accept compose files as thier declarative definition for services, networks and volumes.
- `docker stack deploy` deploys a stack to the swarm.
- Stacks managers all objects for us, including services, networks and volumes. 
- Compoes file now takes features: `deploy` and `placement`, but not `build`.
- The general consensus is that one should not `build` in production, but rather use a registry, to avoid having to install build tools on production servers (incurring resource, time and security risks). Build should be done in CI/CD pipeline.
- It is possible to have single compose files for both development and production, using the `docker-compose.override.yml` file.
- requires `version: 3.0` or higher.
- Swarm secrets can be used to store sensitive data, such as passwords, keys etc. They are encrypted at rest and in transit. They are only available to services in the swarm, not to individual containers.

Run with

`docker stack deploy -c docker-compose.yml <stack name>`



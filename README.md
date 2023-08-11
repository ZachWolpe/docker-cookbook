# Docker Cookbook

Docker comprises of $3$ core components:

- `Build`:  The container `image` is really a universal package manager.
- `Ship`:   The Docker `registry` is a universal package repository.
- `Run`:    The Docker `container` is a universal package runtime.


Benefits:

$3$ key features contribute to Docker's success:

1. `Isolation`: Containers are isolated from each other and the host OS. This reduces the infrustructure overhead, improves simplicity and security. It provides many of the benefits of VMs without the overhead of running a separate kernel/OS for each application.

2. `Environments`: addresses the _"works on my machine"_ problem. Docker containers are immutable, so the environment is consistent from development to production. Consider the "Matrix from Hell" (a schematic representing all possible OS/dev stack combinations) - it is inconcievable to cover all cases efficiently. The container abstracts the OS and dev stack from the host OS, upheld by the `OCI` (Open Container Initiative) standards.

3. `Speed`: Docker containers are lightweight and fast. They can be started in seconds and are ideal for microservices. They are also portable, so they can be run anywhere, on any machine or OS. This works wonders for delivering software in a CI/CD pipeline.


CI/CD Speed improvements over each decade:

Mainframe --> PC/Baremetal ($1990$s) --> VMs ($2000$s) --> Data Centres --> Cloud ($2010$s) --> Containers/Serverless ($2020$s)


### References

- [Docker](https://www.docker.com/)
- [Docker Hub](https://hub.docker.com/)
- [OCI (Open Container Initiative) Standards](https://opencontainers.org/)
- [Kubernetes](https://kubernetes.io/)


---
```
: Zach Wolpe
: zach.wolpe@medibio.com.au
```
---
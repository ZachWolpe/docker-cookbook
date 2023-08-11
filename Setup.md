# Setup

How to run Docker containers.

There are $3$ ways to run Docker containers:

1. `locally`: On your machine (Docker Desktop, RD).
2. `Server`:  On a remote server (AWS, GCP, Azure, etc).
3. `PaaS`:   On a managed platform (Heroku, GCP, Could Run, Fargate, etc).


Most tools to run Docker will typically install and manage a tiny Linux VM on your machine to run the containers. Most docker containers run on `Linux`.

### Docker Desktop

Docker `desktop` is not for servers, Docker `engine` is a subset of Docker Desktop that runs on servers.

Docker desktop includes (but is not limited to):

- Docker Engine
- Docker CLI
- Docker Compose
- Docker BuildKit
- Kubernetes
- Docker App
- Scan, sbom, etc


---
# Basics Commands

Open Docker desktop from the terminal:

```open -a Docker```

See your docker version:

```docker version```

See your docker info:

```docker info```

List all running containers:

```docker ps```

List all docker commands:

```docker```

Note that the management commands are grouped into $4$ categories:
- `build`:    Build images from a Dockerfile.
- `run`:      Run a command in a new container.
- `image`:    Manage images.
- `container`:Manage containers.

Management commands are uses a `docker $command$ $subcommand$` syntax for readability/conciseness.

```docker <command> <sub-command>```
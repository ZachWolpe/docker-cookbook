# Compose

Configure relationships between containers. Save docker container run settings in an easy to read file.


Docker compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application's services. Then, with a single command, you create and start all the services from your configuration.

A Docker compose consists of 2 components:
- YAML-formatted file: defines containers, services, networks, and volumes. 
- CLI tool (docker-compose): used for local dev/test automation with YAML files.


1. `docker-compose.yml` file is used to configure your application's services. It is used to define the services that make up your app so they can be run together in an isolated environment.  

2. `docker-compose` CLI tool is used for local dev/test automation with YAML files.

---
## docker compose.yml

Template for docker compose.yml file:

```yaml

# version isn't needed as of 2020 for docker compose CLI. 
# All 2.x and 3.x features supported
# Docker Swarm still needs a 3.x version
# version: '3.9'

services:  # containers. same as docker run
  servicename: # a friendly name. this is also DNS name inside network
    image: # Optional if you use build:
    command: # Optional, replace the default CMD specified by the image
    environment: # Optional, same as -e in docker run
    volumes: # Optional, same as -v in docker run
  servicename2:

volumes: # Optional, same as docker volume create

networks: # Optional, same as docker network create

```

It provides:
- great documentation
- readibility 
- replaces a shell script


----
## docker-compose CLI

Command line interface for docker compose. Not production-grade, but great for local development and testing.

Common commands:

`docker compose up`     # setup volumes/networks and start all containers.
`docker compose down`   # stop all containers and remove cont/vol/net.



----
## Build at Startup

Docker compose can build images at startup. This is great for development, but not recommended for production.

It will check the cache first and only if the image does not exist will it build it.

```yaml
services:
  proxy:
    build:
      context: .
      dockerfile: Dockerfile
    image: <Image to Build>
    ports:

```yaml

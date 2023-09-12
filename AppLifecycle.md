# Swarm App Lifecycle

It is possible to use a single set of compose files for:
    - local `docker-compose up` development environment
    - remote `docker compose up` CI environment
    - remote `docker stack deploy` production environment

Command:

`docker-compose -f <compose file> -f <compose override file> config`


----
## Service Updates

- `docker service update --image <image name> <service name>` updates the image of a service.
- Provides rolling replacement of tasks/containers in a service.
- Limits zero downtime updates, by updating one container at a time.
- Update has many options, including rollback and health checks.
- A stack deploy (if pre-existing) is identical to a service update.


Update an image used to a newer version:

`docker service update --image <image name> <service name>`

Note that when performing an update, each node is updated incrementally (rolling updates). 

Tip: force rebalancing by running `docker service update --force <service name>`.

### Healthchecks

- `HEALTHCHECK` was added in docker 1.12.
- Supported by dockerfile, compose, docker run and swarm services.
- `HEALTHCHECK` will run a command inside the container, and use the exit code to determine the health of the container.
- Expected exit codes:
    - 0: success
    - 1: unhealthy
    - 2: reserved (do not use)
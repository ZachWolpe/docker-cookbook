# Containers

_*Image*_: Binaries, libraries & source code that make up an application.

_*Container*_: A running instance of an image.

_*Registry*_: A collection of repositories. A repository is a collection of images, like a git repository (docker hub).


----
## Container vs VM

A container is not just a mini VM. It's a process running on the OS kernel. Docker desktop however does run a tiny Linux VM on your machine to run the containers.


----
## Commands

Launch a new container. `--publich 80:80` published to local host. `--detech` or `-d` runs in background.

```docker container run --publish 80:80 --detech <image>```

View running containers:

```docker container ls```

View all containers:

```docker container ls -a```

Stop a container:

```docker container stop <container id>```

View the logs of a container:

```docker container logs <container id>```

Force stop a container:

```docker container kill <container id>```

View the processes running in a container:

```docker container top <container id>```

View the current stats of a container:

```docker container stats <container id>```

View the container's metadata/config:

```docker container inspect <container id>```

---
## Launching a Shell Inside Containers

Launch a shell inside a container:

```docker container run -it <image> <command>```

`-it` is a combination of `-i` and `-t`. `-i` is interactive, `-t` is a pseudo terminal.

Launch a shell inside a running container:

```docker container exec -it <container id> <command>```

terimate these sessions with `exit`.

Restart the container:

```docker container start -ai <container id>```

where `-a` is attach and `-i` is interactive.

---
## Docker Networking

View the networks:

```docker network ls```

See which ports are exposed:

```docker container port <container id>```


---
## Searching a containers Config

Instead of using `| grep`, specific fields can be searched with `--format`:

```docker container inspect --format '{{ .NetworkSettings.IPAddress }}' <container id>```


---
## Docker Networks

Show the networks:

```docker network ls```

Inspect a network:

```docker network inspect <network name>```

Create a new network:

```docker network create <network name>```

Attach a network to a container:

```docker network connect <network name> <container id>```

Detach a network from a container:

```docker network disconnect <network name> <container id>```

DNS: Docker daemon has a built-in DNS server that containers use by default. Containers on the same network can reach each other by name.
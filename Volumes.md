# Volumes

_Containers_ are designed to be _immutable_ and _ephemeral_. This means that they are not designed to be changed and they are not designed to be permanent. Designed to be disposable.

----
## Separation of Concerns

If containers are immutable and ephemeral, then how do we persist data?

----
## Persistent Data

_Volumes_ and _Bind Mounts_ are docker's _Persistent Data_ solutions. They allow us to store data outside of the container's writable layers.

The container sees it as a local file path, but it's actually stored on the host.

----
## Volumes

_Volumes_ are the preferred way to persist data in Docker. They are managed by Docker and are completely managed by Docker. The require manual deletion.

specification:

`docker container run --volume (or -v) <volume name> <image>`

----
## Bind Mountings

_Bind Mounts_ are a map between a _host file_ or _directory_ and a _container_ _file_ or _directory_. Two locations point to the same file(s) (managed by the user not Docker).

Skips UFS (Union File System) and host files overwrite any in container.

specification:

`... run -v <host path>:<container path> ...`

Note: the bound mount starts with a `/` and the volume does not.

----
## Use Cases

- `Iterative Development`: Mounting a file or directory is a great way to develop locally and see changes in real time.

- `Database Storage`: Mounting a database's data directory allows us to persist data between container runs.

- `Secrets`: Mounting a file with secrets allows us to keep secrets out of the image and out of source control.


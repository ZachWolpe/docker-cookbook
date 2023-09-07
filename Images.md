# Images

Images are the application binaries and dependencies with metadata on how to run the image (app).

Officially, an image is _"and ordered collection of root filesystem changes and the corresponding execution parameters for use within a countainer runtime."_


An image is not a complete OS. No kernel, kernel modules (drivers), kernel dependent services (systemd), etc.

An image can be as small as one file (your app binary), such as a goland static binary or include an entire OS (CentOS, Debian, Ubuntu, etc).


---
# Union Filesystem

An image is a collection of layers. Each layer is a filesystem change. The layers are stacked on top of each other to create a single filesystem. This is called a _union filesystem_.

Each layer is uniquely identified by a `SHA256` hash. The hash is the same for the same layer, regardless of the image it is in.

----
# Docker History

The `docker history` command shows the layers of an image.

----
# Docker Inspect

The `docker inspect` command shows the layers of an image, along with other metadata.

----
# Image Tags

An image can have multiple tags. A tag is a human readable name for an image. A tag is a pointer to an image.

Images do not have names. Only tags have names. A tag is a pointer to a specific image commit.

----
# Docker File

The docker file is a text file that contains instructions on how to build an image. The docker file is used by the `docker build` command.

See the (dockerfile reference)[https://docs.docker.com/engine/reference/builder/] for more information.


### File Structure

Default name: `Dockerfile`

Frequently used stanzas (commands) are placed at the top of the file to take advantage of caching. This speeds up the build process.


`FROM` <distribution> # usually a minimal linux distribution such as debian or alpine. Empty container: FROM scratch.

`ENV` <environment variable> <value> # set optional environment variables (for downstream use).

`RUN` <shell command> && <shell command> # note: using the _&&_ to chain commands is a common way to reduce the number of _layers_ in an image.

`EXPOSE` <port> # expose ports to the docker virtual network. Does not expose ports to the host (see `docker run -p`).

`CMD` <command> # required: the command to run when the container starts. Only one CMD per dockerfile. If multiple CMDs are specified, only the last one is used.

Example:

```
FROM debian:jessie
ENV NGINX_VERSION 1.9.3-1~jessie
RUN apt-key ...
    && ...
EXPOSE 80 443
CMD ["nginx", "-g", "daemon off;"]
```

Note: often another image is used in the FROM command. This is called a _base image_. The base image is the first layer of the image being built. This allows us to chain images together to create a new image.
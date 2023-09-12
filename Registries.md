# Container Registries

An image registry is an essential part of a containerized workflow. It is a repository for storing and distributing container images.


----
# Docker Hub

- Docker Hub is the default registry for Docker.
- Offers lightweight image building.
- Linking to Github/BitBucket and auto-building images on commit.
- Private repositories.
- Automated builds.
- Webhooks (a way to trigger a build of an image when a certain event occurs. For example, a webhook can be triggered when a commit is made to a Github repository).
- Organizations (a way to group repositories and users).

_Notes:_

- Automated build (linked to a git repo or bitbucket repo) is the recommended way to build images.
- If your image builds <FROM> another image, ensure to setup `repository links` in the `Build Settings` of the image. This will ensure that the image is rebuilt when the base image is updated. This will trigger a build of the image when the base image is updated.
- Additional customizable triggers are also available.


----
# Docker Registry

Barebones registry server. It is the open source version of Docker Hub. At its core it's just a web server that stores and distributes Docker images.

- Written in GoLang.
- de facto in private container registries.
- Can be used to host private registries.
- Can be used to host a mirror of Docker Hub.
- Storage supports local, S3, Azure, OpenStack Swift, Alibaba, GCP, etc.

Security:
    - secture your registry with TLS.

Storage cleanup:
    - Garbage collection is not enabled by default.


Private Docker Registry: Core Commands:

Run the registry image:

`docker run -d -p 5000:5000 --restart=always --name registry registry:2`

Tag an image:

`docker tag <image name> localhost:5000/<image name>`

Push an image:

`docker push localhost:5000/<image>


Summary: _The Docker Registry is a standalone server application that can be used to host private registries, while Docker Hub is a cloud-based registry provided by Docker. The Docker Registry can be run locally on your own infrastructure._


----
# Private Docker Registry with Swarm

- Works the same way as localhost.
- Because of Routing Mesh, all nodes can see 127.0.0.1:5000.
- If you want to use a different port, you can use the `--publish` flag to publish the port on the host.
- NB: decide how to store images (volume driver).
- All nodes must be able to access images.
- Tip: Use hosted SaaS registry if possible. Popular options include: Quay.io, Google Container Registry, Amazon EC2 Container Registry, Azure, etc.


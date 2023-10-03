# DevOps Docker Tips

- _Scanning_ is a great way to check for vulnerabilities in your containers/clusters.
- _The Alpine Problem_ is a common issue when using Alpine images. Alpine images are small, but they are not as secure as you might think. They are small because they don't include a lot of the tools that you might need to secure your container. You can use the `apk` package manager to install the tools you need, but this will increase the size of your image.
- Scanners do not always find all vulnerabilities. You should always check the CVE database for vulnerabilities in your images.
_apt_ is the most complete package manager for Debian-based images. It is also the most secure. You should use it whenever possible. The advantages of _Apline_ may be overstated.
- *Permissions*: File permissions can be difficult when using Docker. You should always use the `USER` command to set the user for your container. You should also use the `WORKDIR` command to set the working directory for your container. This will help you avoid permission issues. _chown_ is a good way to change the owner of a file or directory. _chmod_ is a good way to change the permissions of a file or directory.
- Default to more containers if possble. This will make your containers more secure and easier to manage. If certain processes can be bundled (like Apache servers) it may not be worth the marginal gain in resources by pooling them.
- Never more than once app or concern per container.



### DevOps on Raspberry Pi

- You can use Docker on Raspberry Pi to create a cluster of Raspberry Pis. This is a great way to learn about Docker and Kubernetes.
- Use _ARM64_ FROM statements to dev locally on your Mac and then deploy to your Raspberry Pi cluster.
- See _docker qemu_ for more info on how to emulate ARM64 on your Mac.


### Traefik

- Traefik is a great way to manage your Docker containers. It is easy to use and has a lot of features.

### Swarm vs Compose

- Use swarm wherever possible.
- You cannot do rolling updates with Compose.

### Enviroment Variables

- _*12 Factor Apps*_ should use environment variables for configuration.
- *(12 Factor Apps)[https://12factor.net/].*
- One factor is strict separation of config from code.
- Secrets can go in files to avoid leaking them in logs. 


### ENTRYPOINTS vs CMD

- Entrypoint script should be a shell script that runs the CMD.

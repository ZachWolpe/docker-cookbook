# Docker File Tips
## Tips from Live Reviews on YouTube

- version and date images.
- `||` runs an `or` in `bash`.
- `&&` runs an `and` in `bash`.
- Use a single `RUN` line for each independent process. You will often see multiple commands within one huge `RUN` line, splitting commands can be dangerous and cause a number of downstream issues:
    - `cache busting`: If you build on any system more than once, the `RUN` line will be cached and not run again. This can cause issues dependency issues if cached data is imcompatible with (downstream) changes in the current build.
- Clean up: If `RUN` processes are sufficiently isolated, delete the cache after each `RUN` line, as well as files no longer in use.
- `COPY` vs `ADD`: `COPY` is only for copying file out of the repo you are in. `ADD` does the same thing but it's best practise to only use `ADD` when we want to download from the internet and unzip/untar. Use `ADD` where possible.
- Use a config file to mount config file at runtime (if using an oschestrator), to remove hardcoding configurations/ssl's etc. Do not contain any secrete data in the image.
- Always include `CMD` and `ENTRYPOINTS`.
    - Repeat the `cmd`/`ENTRYPOINTS` even if it's not necessary, it's good practise to have it there for colaboration.
- `versioning` is important. Use `tags` to version your images. Within images version packages wherever possible.
- Look out for lanuage specific docker commands (such as php).
- Set limits as environment variables, as apposed to hard coded values, so they can be changed at runtime.
- Always scan your images, beware using `Alpine` images.
- Include `HEALTHCHECKS` in your docker file.
- Shutdown connections.
- `DRY`: Don't repeat yourself.
- For template see [BretFisher](https://github.com/BretFisher/php-docker-good-defaults) or [autopilot.io](https://autopilot.io/).
- Add `.dockerignore` file to ignore files that don't need to be copied into the image.
    - Copy the `.gitignore` file and rename it.
    - add the `.git`.
    - Add `node_modules` if applicable.
- Change user to not run as root. `USER node`.

    

### Multi-Stage Builds

Contain stages within a single docker file.

- base.
- dev, from base.
- prod, from base.

- Use multi-stage builds to reduce the size of your images.
- Split the `build` dependencies from the `production` dependencies.
- Use standard: build, test, prod stages.

A more extensive pipeline that includes automated testing:

- base
- dev,      from base
- source,   from base
- test,     from source + dev
- prod,     from source

_*Note*_: You don't want to combine test and prod because you don't want to include the test dependencies in your production image.

### ENTRYPOINTS

The Docker `ENTRYPOINT` command has two forms:
    - `ENTRYPOINT ["executable", "param1", "param2"]` (exec form, preferred) which allows an arbitrary executable to be run, and 
    - `ENTRYPOINT command param1 param2` (shell form) which uses the shell form of the command.

The entrypoint is a command that is run when the container is started. It is the first command that is run. It is often used to run a shell script that starts the application.
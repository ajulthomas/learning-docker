## Creating images using Dockerfile

Docker can build images automatically by reading the instructions from a `Dockerfile`.  A `Dockerfile` is a text document that contains all the commands a user could call on the command line to assemble an image. 

go to [official Dockerfile reference](https://docs.docker.com/engine/reference/builder/)

###### `build` command

-------------------

`docker build <file-path> ` command is used to run commands provided in `Dockerfile`. 

```sh
// running docker build in current directory
$ docker build .
```



> The build is run by the `Docker daemon`, not by the CLI. The first thing a build process does is send the entire context (recursively) to the daemon. In most cases, it’s best to start with an empty directory as context and keep your Dockerfile in that directory. Add only the files needed for building the Dockerfile.

Recommended Reading:

1) [Dockerignore](https://docs.docker.com/engine/reference/builder/#dockerignore-file)
2) [Best practices for writing `Dockerfile` ](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)

### Dockerfile Commands

--------

###### FROM

`FROM` command sets the base image to build upon.

```dockerfile
# syntax:
FROM [--platform=<platform>] <image>[:<tag>] [AS <name>]

FROM ubuntu:latest
```



###### RUN

`RUN` command has two forms:

1) _shell form_

   ```dockerfile
   RUN <command>
   ```

   The default shell for the *shell* form can be changed using the `SHELL` command.

   In the *shell* form you can use a `\` (backslash) to continue a single RUN instruction onto the next line. 

   ```dockerfile
   # For example, consider these two lines:
   RUN /bin/bash -c 'source $HOME/.bashrc; \
   echo $HOME'
   
   # Together they are equivalent to this single line:
   RUN /bin/bash -c 'source $HOME/.bashrc; echo $HOME'
   ```

   

2) _exec form_

   ```dockerfile
   RUN ["executable", "param1", "param2"]
   ```



###### CMD

`CMD`commands has three forms:

1) _exec form_ (preferred form)

   `CMD ["executable","param1","param2"]`

2) _default parameters to ENTRYPOINT_

   `CMD ["param1","param2"]`

3) _shell form_

   `CMD command param1 param2`



###### EXPOSE

```dockerfile
EXPOSE <port> [<port>/<protocol>...]
```



The `EXPOSE` instruction informs Docker that the container listens on the specified network ports at runtime. You can specify whether the port listens on TCP or UDP, and the default is TCP if the protocol is not specified.

> The environment variables set using `ENV` will persist when a container is run from the resulting image. 

You can view the values using `docker inspect`, and change them using `docker run --env <key>=<value>`.

> Environment variable persistence can cause unexpected side effects. 

For example, setting `ENV DEBIAN_FRONTEND=noninteractive` changes the behavior of `apt-get`, and may confuse users of your image.

If an environment variable is only needed during build, and not in the final image, consider setting a value for a single command instead:

```
RUN DEBIAN_FRONTEND=noninteractive apt-get update && apt-get install -y ...
```

Or using [`ARG`](https://docs.docker.com/engine/reference/builder/#arg), which is not persisted in the final image:

```
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y ...
```



###### COPY

`COPY` has two forms:

```dockerfile
COPY [--chown=<user>:<group>] <src>... <dest>
COPY [--chown=<user>:<group>] ["<src>",... "<dest>"]
```

This latter form is required for paths containing whitespace.

The `COPY` instruction copies new files or directories from `<src>` and adds them to the filesystem of the container at the path `<dest>`.



###### VOLUME

```dockerfile
VOLUME ["/data"]
```

The `VOLUME` instruction creates a mount point with the specified name and marks it as holding externally mounted volumes from native host or other containers.



###### WORKDIR

```
WORKDIR /path/to/workdir
```

The `WORKDIR` instruction sets the working directory for any `RUN`, `CMD`, `ENTRYPOINT`, `COPY` and `ADD` instructions that follow it in the `Dockerfile`.
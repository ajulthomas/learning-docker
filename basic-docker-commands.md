## Basic Docker Commands

#### run
------
```docker run <image-name:tag>``` command is used to start a docker container from image.

Example:

``` sh
$ docker run nginx // starts an nginx container
```

```sh
$ docker run -d redis // starts a redis container in background(detached mode)
$ docker run -d --name my_app nginx // starts a container and names it to my_app
```


* ###### Interactive Terminal
    ```sh
    /**  
    * runs container in interactive terminal mode
    *  -i stands for interactive mode
    *  -t attaches terminal
    */
    $ docker run -it --name my_db postgresql:latest
    
    ```

* ###### Port Mapping in Docker
  syntax:
  ```docker run -p <host-port>:<container-port> <image-name>``` 
  Above syntax is used for port mapping. The container listens to the host-port on mapping of host port to container port.

  ```sh
  /**
  * port publishing/ exposing ports
  * -p denotes port mapping/publishing
  * -p port_on_host:port_on_container
  */
  $ docker run -p 80:4200 my_repo/my_web_app
  ```

* ###### Volume Mapping in Docker
  
  ```docker run -v <host-location>:<container-location> <image-name>```   command helps us in persisting data in host machine even if we have     permanently deleted or removed the container.    
  
  Example:

  ```sh
  $ docker run -v /app/data:/var/lib/mysql mysql
  ```

* ###### Environment Variables

  syntax: 

  ```docker run -e <env-variable>=<value> <image-name>```

  `-e` flag is used for passing environment variables.

  Example:
  
  ```sh
  $ docker run -d -e PGDATA=/var/lib/postgresql/data/pgdata postgresql
  ```
  



#### ps

----

```docker ps``` command lists all running containers.

Example:

```sh
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED           STATUS              PORTS               NAMES
  d851c801e4d0        nginx               "/docker-entrypoint.…"   14 seconds ago      Up 13 seconds       80/tcp              jolly_volhard
  
$ docker ps -a // lists all containers including currently running and   stopped ones
  
$ docker ps -q // lists container ids only
  
$ docker ps -a -q -f "status=exited" // lists all stopped containers
									 // -f tag is used to filter results
```



#### stop

----

```docker stop <container-id>``` or ```docker stop <container-name>``` shuts down a running container.

Example:

````sh
$ docker stop jolly_volhard // stops container with name jolly_volhard

$ docker stop d851c801e4d0 // stops container with container-id d851c801e4d0

$ docker stop $(docker ps -q) // stops all running containers
````



#### rm

-----

```docker rm <container_name>``` removes a stopped or exited container permanently.

Example:

```sh
$ docker rm jolly_volhard // if it returns the image back, the container is removed
jolly_volhard

$ docker rm $(docker ps -a -d) // removes all docker containers
```

  

#### pull

------

```docker pull <image_name>``` downloads the image from Docker-hub and saves the image in local for later use.

Example:

```sh
$ docker pull nginx // downloads the nginx image from DockerHub
```



#### attach

-------

```docker attach <container_name>``` or ```docker attach <container_id>``` to run the container in attached mode.

```sh
$ docker run -d redis
29bcf76b76f2190f2b80d424d5a9af5ecee3c2989424e27d41c97ba1f94aaf7d

$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
29bcf76b76f2        redis               "docker-entrypoint.s…"   45 seconds ago      Up 44 seconds       6379/tcp            boring_ramanujan

$ docker attach boring_ramanujan
```



#### inspect

--------

```docker inspect <container-name>``` lists additional details about a container. It has details like state, mount, network config e.t.c

Example:

```sh
$ docker inspect boring_ramanujan // lists additional details about a container

```



#### logs

--------

```docker logs <container-name>``` logs the docker-container logs.

Example:

```sh
$ docker logs boring_ramanujan

```


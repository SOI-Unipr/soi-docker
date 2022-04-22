# soi-docker
Docker files for SOI class exercises.

### generic commands
build an image with tag --rm means "Remove intermediate containers after a successful build"
```
docker build --rm -t apache2 .
```

see all images
```
docker image ls
```

inspect an image
```
docker inspect 9c1b6dd6c1e6be9fdd2b1987783824670d3b0dd7ae8ad6f57dc3cea5739ac71e
```

attach to a container started with -it flag
```
docker attach todo-server 
```
then CTRL-p CTRL-q key sequence to exit

launch a container: -d detached -it Allocate a pseudo-tty and Keep STDIN open even if not attached
```
docker run -dit --name todo-app -p 8080:80 apache2
```

docker exec -it devtest bash

create container with a volume (the volume can be shared between containers)
```
docker create --name devtest --mount source=myvol,target=/app nginx:latest
```

the command `docker run` is the same of `docker create` + `docker start` adding an optional command


create a network
```
docker network create mynetwork --subnet=10.10.0.0/16
```

inspect the network bridge
```
docker network inspect mynetwork

exec a command
```
docker container exec -it mycontainer sh
```

run docker compose
```
docker-compose up
```



### See the README file on frontend and backend directories for details on single container.

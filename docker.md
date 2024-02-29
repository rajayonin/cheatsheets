# rajayonin's Docker cheatsheet
My personal cheatsheet for Docker stuff so I don't forget about 'em (I'll still will).  
More info on https://docs.docker.com/go/guides/.

## Installing Docker
APT (Debian, Ubuntu, etc.):
```
sudo apt update
sudo apt install docker docker-compose -y
```
Pacman (Arch, Manjaro, etc.):
```
sudo pacman -Syu install docker docker-compose
```

It is recommended to allow docker to be run by the current user (without the need for sudo), but that depends on the installation:
```
sudo usermod -aG docker $USER
```

## Docker commands
- `docker ps`: List all docker containers currently running.
- `docker exec <container> <cmd>`: Run _cmd_ inside _container_.
    - `docker exec -it <container> /bin/bash/`: Open terminal in _container_ (`-it` allows tty).
- `docker logs <container>`: Open the logs for _container_.
- `docker cp`: Copy
- `docker pause <container>`
- docker start
- docker restart
- docker stats
- docker kill
    - docker kill $(docker ps -q)
- docker system prune -a
- `docker run --name <name> -it <image> /bin/bash -i`
- docker rm
- docker system df

### Dockerfiile
<!-- TODO -->

## Docker-compose commands
Docker compose is an utility to build one or more containers and specifying its properties by using a config file. It is the preffered way to use docker.  
For using it you need a `docker-compose.yaml` file (see [docker-compose.yaml](#docker-compose.yaml))
- `docker-compose build [<path>]`: Builds the containers as per the config file.  It takes _path_ (by default, `.`), and searches down for a docker-compose.yaml file to use.
- `docker-compose up <container> [-d]`: Initializes _container_. Include `-d` to run it as a daemon (in background), which is reccomended.
- `docker-compose down`


### docker-compose.yaml
<!-- TODO -->

<!--
las imágenes se guardan en `/var/lib/docker`
docker image prune
docker container prune
docker volume prune
-->
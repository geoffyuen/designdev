## The simplist docker-compose.yml for LAMP dev

https://github.com/celsocelante/docker-lamp

    git clone https://github.com/celsocelante/docker-lamp.git
    docker-compose up -d
    docker-compose down

## List images

- `docker ps` in use
- `docker ps -a` all images

## Remove an image

1. `docker images`
1. `docker rmi  <IMAGE ID>`

## Remove all containers

    docker rm $(docker ps -a -q)

## Remove all images

    docker rmi $(docker images -q)

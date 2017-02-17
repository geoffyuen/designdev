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

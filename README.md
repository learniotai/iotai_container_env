# iotai_container_env

Container environment using Docker for Learning IoT and AI

See [Wiki](https://github.com/learniotai/iotai_container_env/wiki)

## Prerequisites
docker
docker-compose

## Build

`docker-compose build`

Creates

```
iotai_infer_gpu
iotai_train_gpu
```

* `iotain_infer_gpu`: use for training models. 
    `iotain_train_gpu` builds on `iotain_infer_gpu` adding development tools.
* `iotain_infer_gpu`: use for runnign models in production. 

## Run

~/.bashrc
```
export CURRENT_UID=$(id -u):$(id -g)
```

### Training container 
```
docker-compose up -d train
```

### Inference container
```
docker-compose up -d infer
```

### Connect to running container

List running containers
`docker ps`

Connect
`docker exec -it iotai_container_env_train_1`

## Setup launch command alias as alternative to launching with `docker-compose`

## Inference container
`alias iotai_infer='docker run --rm -u $(id -u):$(id -g) --name iotai_infer --runtime=nvidia -it -v  "/etc/passwd:/etc/passwd:ro" -v  "/etc/group:/etc/group:ro" -v "/home:/home" --memory=16g  --shm-size=16g -p "780:80" -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=$DISPLAY iotai_infer_gpu:latest bash'`

## Training container
`alias iotai_train='docker run --rm -u $(id -u):$(id -g) --name iotai_train --runtime=nvidia -it -v  "/etc/passwd:/etc/passwd:ro" -v  "/etc/group:/etc/group:ro" -v "/home:/home" --memory=16g  --shm-size=16g -p "780:80" -p "7888:8888" -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=$DISPLAY iotai_train_gpu:latest bash'`

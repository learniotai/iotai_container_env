# IoTAI Training Docker image

## Build

`docker-compose build`

### Check build

`docker images`

## Setup launch command alias 

`alias iotai_train='docker run --rm -u $(id -u):$(id -g) --name iotai_train --runtime=nvidia -it -v  "/etc/passwd:/etc/passwd:ro" -v  "/etc/group:/etc/group:ro" -v "/home:/home" --memory=16g  --shm-size=16g -p "780:80" -p "7888:8888" -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=$DISPLAY iotai_train_gpu:latest bash'`

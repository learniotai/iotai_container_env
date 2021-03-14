# IoTAI Inference Docker image

## Build

`docker-compose build`

### Check build

`docker images`

## Setup launch command alias 

`alias iotai_infer='docker run --rm -u $(id -u):$(id -g) --name iotai_infer --runtime=nvidia -it -v  "/etc/passwd:/etc/passwd:ro" -v  "/etc/group:/etc/group:ro" -v "/home:/home" --memory=16g  --shm-size=16g -p "780:80" -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=$DISPLAY iotai_infer_gpu:latest bash'`

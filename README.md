# iotai_container_env

Container environment using Docker for Learning IoT and AI

See [Wiki](https://github.com/learniotai/iotai_container_env/wiki)

## Prerequisites
docker
docker-compose

## Build 
Build infer/ subdirectory first 
Then build train/ subdirectory  

## NVIDIA 

### Docker-compose with NVIDIA 
https://stackoverflow.com/questions/41346401/use-nvidia-docker-compose-launch-a-container-but-exited-soon#comment73796775_41947086

## Run

~/.bashrc 
```
export CURRENT_UID=$(id -u):$(id -g)
```

```
docker-compose up 
```


# Docker

## Basic Command

### Container to image
```console
$ docker commit your_container target_image
```

###  Image to tar file
```console
$ docker save -o file.tar your_image
```

###  Tar file to docker Image 
```console
$ docker load -i yourFile.tar
```

###  Container to Tar file 
```console
$ docker export your_container targetFile.tar
```

###  Tar to Image 
```console
$ docker import yourFile.tar
```

### Tag Docker Image
```console
$ docker tag src_img:tag target_img:tag
```

### push
```console
$ docker push localhost:5000/hello-world
```

### tag
```console
$ docker tag hello-world localhost:5000/hello-world
```

---

## Install Docker in Ubuntu

```console
$ sudo apt-get update | sudo apt-get upgrade
$ sudo apt-get install curl
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
$ sudo apt-get install docker-ce
```

## Share Host PC X-Server with Container

> Run GUI App such as gedit, qt creator in container, we need to share Host PC X-server.

In Host PC:
```console
$ sudo xhost +si:localuser:root
```
Run A Docker Image In Host Terminal:
```console
sudo docker run -i -t --gpus all --network host -it -e DISPLAY=$DISPLAY -v /tmp/.X11-unix/:/tmp/.X11-unix --name test_container imageA
```
In Container:
```console
$ apt-get update
$ apt install libcanberra-gtk-module libcanberra-gtk3-module
```

## docker warning config.json permission denied

```console
$ sudo chown "$USER":"$USER" /home/"$USER"/.docker -R
$ sudo chmod g+rwx "/home/$USER/.docker" -R
```

## Shared Memory

Use the `--ipc` flag and the `--shm-size` flags to be able to **create and register shared memory regions** with Triton when running in a docker.

> IPC (POSIX/SysV IPC) namespace provides separation of named shared memory segments, semaphores and message queues.

[more](https://docs.docker.com/engine/reference/run/#ipc-settings---ipc)

e.g.
```console
$ docker run --gpus=1 -v /dev:/dev --ipc=host --shm-size=1g --rm -p8000:8000 -p8001:8001 -p8002:8002 \
-v /examples/model_repository:/models \
nvcr.io/nvidia/tritonserver:21.03-py3 \
tritonserver --model-repository=/models
```

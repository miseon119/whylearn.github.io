---
sort: 1
---

# Docker Notes

# Install Docker in Ubuntu

```console
$ sudo apt-get update | sudo apt-get upgrade
$ sudo apt-get install curl
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
$ sudo apt-get install docker-ce
```

# Share Host PC X-Server with Container

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

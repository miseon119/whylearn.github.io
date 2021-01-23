---
sort: 10
---

# IDE And Environment Setting

## VS Code Remote SSH Setting

**Local PC Setting**

Create your local SSH key pair:
```console
$ ssh-keygen -t rsa -b 4096
```

Connecting to a Linux SSH host:

```console
$ export USER_AT_HOST=user-name@hostname
$ export PUBKEYPATH=$HOME/.ssh/id_rsa.pub

$ ssh-copy-id -i "$PUBKEYPATH" "$USER_AT_HOST"
```

SSH file and folder permissions:
```console
$ chmod 700 ~/.ssh
$ chmod 600 ~/.ssh/config
$ chmod 600 ~/.ssh/id_rsa.pub
```

## Connect To A Remote Host In VS Code

Step 1: In VS Code, Command Palette (F1)

Step 2: Search  `Remote-SSH: Connect to Host` and Click

Step 3: Type `user@hostname`

---

## Install cuDNN: 7.6.5 in Ubuntu 18.04 (x64)

Debian Installation:

1. [Download](https://developer.nvidia.com/rdp/cudnn-archive) `cuDNN Runtime Library for Ubuntu18.04 (Deb)`, `cuDNN Developer Library for Ubuntu18.04 (Deb)`, `cuDNN Code Samples and User Guide for Ubuntu18.04 (Deb)`

2. Install 

Install runtime:
```console
$ sudo dpkg -i libcudnn7_7.6.5.32-1+cuda10.2_amd64.deb
```
Install developer library:
```console
$ sudo dpkg -i libcudnn7-dev_7.6.5.32-1+cuda10.2_amd64.deb
```
Install code samples 
```console
$ sudo dpkg -i libcudnn7-doc_7.6.5.32-1+cuda10.2_amd64.deb
```

[reference](https://docs.nvidia.com/deeplearning/cudnn/install-guide/index.html#installlinux-deb) 

## Install TensorRT 7.0 in Ubuntu 18.04 (x64)

1. [Download](https://developer.nvidia.com/compute/machine-learning/tensorrt/secure/7.0/7.0.0.11/local_repo/nv-tensorrt-repo-ubuntu1804-cuda10.2-trt7.0.0.11-ga-20191216_1-1_amd64.deb) 

2. Install

```console
$ sudo dpkg -i nv-tensorrt-repo-ubuntu1804-cuda10.2-trt7.0.0.11-ga-20191216_1-1_amd64.deb
$ sudo apt-get update
$ sudo apt-get install tensorrt libcudnn7
```
using Python 3:
```console
$ sudo apt-get install python3-libnvinfer-dev
```

Use TensorRT with TensorFlow:
```console
$ sudo apt-get install uff-converter-tf
```

Verify the installation:
```console
$ dpkg -l | grep TensorRT
```

[reference](https://docs.nvidia.com/deeplearning/tensorrt/archives/tensorrt-700/tensorrt-install-guide/index.html#installing-debian)

---

##  Install DeepStream 5.0

Nvidia said...
*You must install the following components: - Ubuntu 18.04 - GStreamer 1.14.1 - NVIDIA driver 450.51 - CUDA 10.2 - TensorRT 7.0.X*

Install dependencies:
```console
$ sudo apt install \
libssl1.0.0 \
libgstreamer1.0-0 \
gstreamer1.0-tools \
gstreamer1.0-plugins-good \
gstreamer1.0-plugins-bad \
gstreamer1.0-plugins-ugly \
gstreamer1.0-libav \
libgstrtspserver-1.0-0 \
libjansson4
```

[Download](https://developer.nvidia.com/assets/Deepstream/5.0/ga/secure/deepstream_sdk_5.0.1_amd64.deb) DeepStream 5.0 dGPU Debian package


Install `.deb` file
```console
$ sudo apt-get install ./deepstream-5.0_5.0.1-1_amd64.deb
```


[reference](https://docs.nvidia.com/metropolis/deepstream/dev-guide/text/DS_Quickstart.html#dgpu-setup-for-ubuntu)
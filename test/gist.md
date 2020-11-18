---
sort: 6
---

# Nvidia Jetson Series 

Swap memory for Jetson nano

Step 1: check current swap status.
```console
$ free -m
```
![free-result](free.png)

Step 2: Disable nvzram
```console
$ sudo systemctl disable nvzramconfig
```
![disable-nvz](disable-nvzram.png)

Step 3: 
```console
$ sudo fallocate -l 4G /mnt/4GB.swap
$ sudo chmod 600 /mnt/4GB.swap
$ sudo mkswap /mnt/4GB.swap
```

Step 4: modifiy fstab file
```console
$ sudo vim /etc/fstab
```
Add this line,
```text
/mnt/4GB.swap swap swap defaults 0 0
```
![afterswap](after-swap.png)
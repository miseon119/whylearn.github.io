---
sort: 6
---

# Nvidia Jetson Series 

## SD Card Backup & Restore

### Backup

Step 1: Check your SD card in your host Linux PC
```console
$ sudo parted -l
```
This command sample result:
> Model: Generic MassStorageClass (scsi)
> Disk /dev/sdb: 31.9GB
> Sector size (logical/physical): 512B/512B
> Partition Table: msdos
> Disk Flags: 
> 
> Number  Start   End     Size    Type     File system  Flags
 > 1      4194kB  31.9GB  31.9GB  primary  fat32        lba

Step 2: Check SD card unmount
```console
$ sudo umount /dev/your-sd-card
```
sample result:
> sudo umount /dev/sdb
> umount: /dev/sdb: not mounted.

Step 3: save as image file
```console
$ sudo dd if=/dev/yourSdCard conv=sync,noerror bs=64K | gzip -c > ~/backup_nano.img.gz
```
### Restore
Step 1: 
```console
 $ sudo su
```

Step 2: 
```console
 $ gunzip -c ~/backup_nano.img.gz | dd of=/dev/YourSdCard bs=64K
```

## Swap memory for Jetson nano

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
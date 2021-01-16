---
sort: 4
---

# Linux

## Chown Command

Change File or Folder's Owner 

### Check Folder or File's Owner

```console
$ ls -lt
```

sample result:
```
drwxr-xr-x   2 root root       4096 Jan 15 23:34 foo
```

### Change Owner To Specific User

```console
$ sudo chown user1:user1 <file>
```
sample:
```console
$ sudo chown wendy:wendy foo
```

Or use User ID:
```console
$ chown 1000:1000 foo.txt
``` 

Check User ID:
```console
$ id
```
sample result:
```
uid=1000(wendy) gid=1000(wendy) groups=1000(wendy),4(adm),20(dialout),24(cdrom),27(sudo),30(dip),46(plugdev),116(lpadmin),126(sambashare)
```

### Change To Root
```console
$ sudo chown root foo
```


### Change Group To Root
```console
$ sudo chown :root foo
```


### Chaner Folder's Owner
```console
$ chown -R wendy:wendy foo-folder
```


---

##  Git Basic Commands

### Commit
```console
$ git commit -m "your note"
```

### Add Remote Repository
```console
$ git remote add origin {remote repository Address}
```

### Add
```console
$ git add .
```
```

### Push
```console
$ git push origin {branch name}
```
eg. branch name is master or main.

---

## SSH Config Setting

### SSH Config File Sample

Common Remote Control Command via SSH:
```console
$ sudo ssh Jane@192.168.0.1 
```

If you want to SSH your remote PC by short command such as 'ssh JanePC', or you control many remote PCs.
Maybe you need this 'config' file instead. It usually locates in `~/.ssh/config`. If not, create one.

Sample config file:
```
Host JanePC 
    HostName 192.168.0.1
    User Jane

Host BillPC 
    HostName 192.168.0.2
    User Bill

```
After saving the config file, and then open terminal type `ssh JanePC`. 
You can access `Jane@192.168.0.1`.

---

### SSH X11 Forwarding

**Server PC Requirement:**

Step 1: 
```console
$ sudo apt-get install xauth
```
Step 2: Modify `/etc/ssh/sshd_config` file
```
X11Forwarding yes
```

**Client PC Requirement:**

Step 1: vim `~/.ssh/config`, add `ForwardX11 yes`

Sample config
```
 Host JanePC 
    HostName 192.168.0.1
    User Jane

Host BillPC 
    HostName 192.168.0.2
    User Bill

 Host *
  ForwardX11 yes
```

Step 2: Test 
```console
ssh -X Jane@192.168.0.1
```
```console
$ gedit
```

---

### SSH Remote Control Without Password

Step 1: Generate public key
```console
$ ssh-keygen
```
This will create `id_rsa.pub` key under `~/.ssh/` directory.

Step 2: Copy the key around remote PC
```console
$ ssh-copy-id -i .ssh/id_rsa.pub Jane@192.168.0.1
```

Step 3: Test
```console
$ ssh Jane@192.168.0.1
```

[More SSH Config Reference](http://man.openbsd.org/OpenBSD-current/man5/ssh_config.5#ForwardX11).

---

###  Enable Or Disable X11 Forwarding in SSH server

Modify sshd configuration file:
```console
$ sudo vim /etc/ssh/sshd_config
```

Search `X11Forwarding`:
```
X11Forwarding no
```

Reload or restart SSH server service:
```console
$ sudo systemctl restart sshd
```

[Reference](https://www.simplified.guide/ssh/enable-x11-forwarding)

---

##  Swap Memory

> In Linux OS, whenever RAM has an insufficient amount of memory to hold a process, it borrows some amount of memory from the secondary storage to store its inactive content. Here, the borrowed space from the hard disk is called **Swap Memory**.
> Linux swap is a very useful way to extend the RAM. Because it provides the necessary additional memory when RAM space has been exhausted and a process has to be continued. 

![swap](swap.png)

Pros:

- Swap saves from crashes
- It can easily hold those inactive blocks of RAM that are hardly used once or twice and then they are never used. The freed up RAM can then be used to hold more programs that have a higher priority

Cons:

- Swap is slower than RAM. Adding a swap space won't make your computer faster, it will only help to overcome some limitations posed by the RAM size.

> The safest: RAM = SWAP

| RAM     | SWAP     |
| ------- | -------- |
| < 1Gb   | 2Gb      |
| 2-4Gb   | 2-4Gb    |
| 8Gb     | 4Gb      |

### Check Swap Command

```console
$ swapon
```

```note
For reference, see: https://linuxhint.com/swap_memory_linux/
```


### Cut Command

Cut text's words by specific colume

```console
 cut -c 5- < file1.txt > file2.txt
```
- [5-] cut start point which is 5th character.

file1.txt
```
aaaaabbbbbccccc
```
after hitting command:

file2.txt
```
abbbbbccccc
```

---

## Troubleshooting

### Check Service log
```console
$ journalctl -u service-name.service
```

for the current boot:
```console
$ journalctl -u service-name.service -b
```
[reference1](https://sysops.tistory.com/115)

[reference2](https://www.digitalocean.com/community/tutorials/how-to-use-journalctl-to-view-and-manipulate-systemd-logs)

[log reference](https://www.loggly.com/ultimate-guide/python-logging-basics/)


### apt-get update failed

In some cases, update error like this:
> Err:11 http://ppa.launchpad.net/inameiname/stable/ubuntu bionic Release   
  404  Not Found [IP: 91.189.95.85 80]

It mentioned `inameiname` message in this error.

**Solution**

Step 1:
```console
$  cd /etc/apt/sources.list.d/
```

Step 2: Check your `.list` files:
```console
$ ls -l
```
In my case, it's similar like this:
```
user@user:/etc/apt/sources.list.d$ ls -l
total 36
-rw-r--r-- 1 root root  71 Dec 29 10:34 gazebo-stable.list
-rw-r--r-- 1 root root  71 Dec 29 10:34 gazebo-stable.list.save
-rw-r--r-- 1 root root 189 Dec 29 10:34 google-chrome.list
-rw-r--r-- 1 root root 189 Dec 29 10:34 google-chrome.list.save
-rw-r--r-- 1 root root 138 Dec 29 10:34 inameiname-ubuntu-stable-bionic.list
-rw-r--r-- 1 root root 338 Dec 29 10:34 nvidia-container-runtime.list
-rw-r--r-- 1 root root 336 Dec 29 10:34 nvidia-container-runtime.list.save
-rw-r--r-- 1 root root 193 Dec 29 10:34 vscode.list
-rw-r--r-- 1 root root 193 Dec 29 10:34 vscode.list.save
```

`-rw-r--r-- 1 root root 138 Dec 29 10:34 inameiname-ubuntu-stable-bionic.list` this file maybe caused error.

Step 3:
```console
$ sudo rm inameiname-ubuntu-stable-bionic.list
```

Step 4:
```console
$ sudo apt-get update
```

---

## dpkg common commands

**Install package**
```console
$ sudo dpkg -i your.deb
```

**Search installed package**
```console
$  sudo dpkg -l pkg_name
```
or 
```console
$  sudo dpkg --list pkg_name
```

```console
$ dpkg -l | grep part_of_pkgName
```

**remove**
```console
$ sudo dpkg --remove pkg_name
```
and 
```console
$  sudo dpkg --purge pkg_name
```

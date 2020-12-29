---
sort: 4
---

# Linux

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

___
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

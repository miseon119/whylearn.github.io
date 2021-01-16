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
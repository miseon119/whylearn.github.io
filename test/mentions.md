---
sort: 8
---

# Python

## Python3 Setting

### Install pip3

```console
$ sudo apt-get install python3 python3-pip python3-dev python3-setuptools
```
```colsole
$ sudo pip3 install --upgrade pip
```
### Install virtualenv (if need)

```console
$ virtualenv venv
```
```console
$ source venv/bin/activate
```
#### Save pip3 package list to .txt file
```console
$ pip3 freeze > requirements.txt
```
### Remove virtualenv
```console
sudo apt-get remove --auto-remove virtualenv
```
```console
sudo apt-get remove virtualenv
```
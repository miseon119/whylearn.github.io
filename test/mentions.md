---
sort: 8
---

# Python

## Version Check

### Tensorflow Version

```python
import tensorflow as tf
 tf.__version__
```

### gstreamer version

```console
dpkg -l | grep gstreamer
```

## Python3 Setting

### Install pip3

```console
$ sudo apt-get install python3 python3-pip python3-dev python3-setuptools
```
```colsole
$ sudo pip3 install --upgrade pip
```
### Install virtualenv (if need)

**Install**
```console
$ pip3 install virtualenv
```

**Create a virtual environment**
```console
$ virtualenv venv
```

**Activate virtual environment**
```console
$ source venv/bin/activate
```

**Deactivate**
```console
$ deactivate
```

### virtualenvwrapper

**install**
```console
$ pip3 install virtualenvwrapper
```

**Create a virtual environment**
```console
$ mkvirtualenv venv
```

**Work on a virtual environment**
```console
$ workon venv
```

### Save pip3 package list to .txt file
```console
$ pip3 freeze > requirements.txt
```
### Remove virtualenv
```console
$ sudo apt-get remove --auto-remove virtualenv
```
```console
$ sudo apt-get remove virtualenv
```

### Install jupter notebook

Step 1: Install Package
```console
$ sudo apt update && sudo apt -y upgrade
$ sudo apt install python3-pip python3-dev
$ sudo -H pip3 install --upgrade pip
$ sudo -H pip3 install virtualenv
```
Step 2: create vitual env
```console
$ virtualenv jupyterenv
$ source jupyterenv/bin/activate
$ pip install jupyter
```
[more](https://speedysense.com/install-jupyter-notebook-on-ubuntu-20-04/)

Step 3: Run notebook
```console
$ jupyter notebook --port 9999
```
or
```console
$ jupyter execute notebook.ipynb
```

---

### Example of Inheritance

**Before using inheritance**

```python
class Panda:
	def __init__(self, name, age):
		self.name = name
		self.age = age
	def speak(self):
		print("bamboo")

class Rabbit:
	def __init__(self, name, age):
		self.name = name
		self.age = age
	def speak(self):
		print("carrot")
```

**After using inheritance**

```python
class Animal:
	def __init__(self, name, age):
		self.name = name
		self.age = age
	def show(self):
		print(f"I'm {self.name}. I am {self.age}")	
		
class Panda(Animal): # inheriting upper level class
	def __init__(self, name, age, color):
		super().__init__(name, age)
		self.color = color

	def speak(self):
		print("bamboo")

class Rabbit(Animal): # inheriting upper level class
	def speak(self):
		print("carrot")

temp1 = Panda("lingling", 10, "blackwhite")
temp1.show()

temp2 = Rabbit("Tom", 5)
temp2.show()
```

---

### Edit Specific Line

Original `test.txt`

```
aaa
bbb
ccc
```

Run this piece:

```python
ss = open("test.txt", "r")
list_of_lines = ss.readlines()
list_of_lines[1] = "kkk\n"

ss = open("test.txt", "w")
ss.writelines(list_of_lines)
ss.close()
```

Modified `test.txt`

```
aaa
kkk
ccc
```

---

### Array and List

**Convert Array/List**

```python
import numpy as np
from numpy import array

custom_roi_points = array([(50,60),(50,100),(100,50),(100,100)])

# array to list
custom_roi_list = custom_roi_points.tolist()

# list to array
custom_roi_arr = array(custom_roi_list)

```

### List

**Create**

```
List = []
```
```
List = [1, 2, 3]
```
```
List = [[10,10], [20,20]]
```

**Size of list**

`len(List)`

**Add element**

1. Use `append()`, you can add one elements in the end of the list :
```
List.append(x)
```
2. Use `insert`, you can add element in specific position:
```
List.insert(index, data)
```
```
List.insert(1, 5)
```
3. Use `extend`, you can add multiple elements in the end of the list:
```
List.extent([x, y , z])
```
```
List.extent([3, 4 , 5])
```

4. clear()
```python
list.clear()
```

**Access Element**

Access last element: 
```
List[-1]
```

**deeo copy list**
```python
import copy
a = [1, 2, 3]
b = copy.deepcopy(a)
```

### ls Directory using glob

sorting by create time
```python
sorted_files = sorted(glob.glob('*'), key=os.path.getctime) 
for i in sorted_files:
	pass
```

sorting by touched time
```python
sorted_files = sorted(glob.glob('*'), key=os.path.getatime) 
for i in sorted_files:
	pass
```

sorting by modified time
```python
sorted_files = sorted(glob.glob('*'), key=os.path.getmtime) 
for i in sorted_files:
	pass
```

sorting by size
```python
sorted_files = sorted(glob.glob('*'), key=os.path.getsize) 
for i in sorted_files:
	pass
```

---


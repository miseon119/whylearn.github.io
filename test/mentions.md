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

### Class Sample
```python
class Panda:
	def __init__(self, name, age):
		self.name = name
		self.age = age
	def get_name(self):
		return self.name
	def get_age(self):
		return self.age
	def set_age(self):
		self.age = age

temp = Panda("lingling", 10)
temp.set_age(11)
```
### Example of Inheritance in Python

Before using inheritance:
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
After using inheritance:
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

### Class Attributes

```python
class Person:
	number_of_people = 0
	def __init__(self, name):
		self.name = name
		Person.number_of_people += 1

p1 = Person("Jane")
p2 = Person("Bob")
print(Person.number_of_people)

```
Result:
```
2
```

### Class Methods
```python
class Person:
	a = 0
	def __init__(self, name):
		self.name = name
		Person.add_person()

	@classmethod
	def number_of_people(cls):
		return cls.a

	@classmethod
	def add_person(cls):
		cls.a += 1

p1 = Person("Jane")
p2 = Person("Bob")
print(Person.number_of_people())
```

### Class Static Methods
```python
class Person:

	@staticmethod
	def age(x):
		return x + 5

print(Person.age(5))
```
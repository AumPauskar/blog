+++
title = 'Oops'
date = 2023-11-16T10:07:41+05:30
draft = false
+++

# Chapter summary - Unit 4
**Object Oriented Programming:**
Define and use your own classes: An introduction to classes and objects, define a class,
object composition, encapsulation; \
**Inheritance:** Inheritance, override object methods; \
**Design an object oriented program:** Techniques for object-oriented design
Text Book 1 – Chapters 14,15,16

## Creating your own class
A class can be created in python by using the class keyword
```py
class MyClass:
  x = 5
```
This creates a blueprint for the objects to be defined. Methods and members can be defined in the class.

## Constructors
Python classes need constructors to initialise the members and methods, it is initiated by the **init** keyword.

```py
# user class
class MyClass:

	# constructor
	def __init__(self):
		msg = "hello world"

	# accessing members
	def println(self):
		print(self.msg)

# creating the object
obj = MyClass()
obj.println()
```
The self keyword acts as a self pointing object.
Here when the object is generated the constructor is called and the msg variable is initiated. The usage of the self keyword is also crutial is called methods within classes.

This code can be also changed to accept paramatrised constructor
```py
# user class
class MyClass:

	# constructor
	def __init__(self, arg):
		self.msg = "hello world"

	# accessing members
	def println(self):
		print(self.msg)

# creating the object
obj = MyClass("")
obj.println()
```
The self keyword here also sometimes acts like the _super_ keyword in java.

## Lambda functions
Lambda functions are functions are anoymous functions, it can have n number of arguments but can only have one expression. \
Example:
```py
# program written with lambda functions
# to print sum
func = lambda num1, num2:num1+num2
print(func(3,6))

# program done with functions
def add(num1, num2):
	return num1 + num2
print(add(3, 6))
```

## Encapsulation
Encapsuation is the way of wrapping the data and the functions withing a class isolated from the ouytside interference. Encapsualation can be achieved in python by using private and public attributes at stretigic places to ensure the data safety. 

```py
class MyData:
	# constructor to get the data
	def __init__(self, val):
		self.__x = val
	def printData(self):
		print(self.__x)
```

## Inheritance
Inheritance is a way for the derived class to get all the properties of base class including the class methods and class members.

Syntax of inheritance
```py
class MainClass:
    # methods/members
class DerivedClass(MainClass):
    # methods/members
```

Example of a program that follows polymorphism

```py
class Vehicle:
	def __init__(self, cc, bhp):
		self.__cc = cc
		self.__bhp = bhp

	def printStd(self):
		print(f"The car is {self.__cc} cc and has {self.__bhp} bhp")

class OpenWheeler(Vehicle):
	def __init__(self, cc, bhp):
		super().__init__(cc, bhp)

	def getDownforce(self, downforce):
		self.__downforce = downforce

	def printStd(self):
		super().printStd()
		print(f"The car has {self.__downforce} downforce")

car1 = Vehicle('100', '9')
f11976 = OpenWheeler('3000', '500')
f11976.getDownforce('300')

car1.printStd()
f11976.printStd()
```

### IsInstance in python

The `isinstance()` function in Python is used to check if an object is an instance of a specified class. The syntax of the isinstance() function is

```py
isinstance(object, classinfo)
```
Here is an example of the isinstance() function showing the difference between two inherited classes
```py
class Animal:
  def speak(self):
    print("I am an animal")

class Dog(Animal):
  def speak(self):
    print("Woof!")

d = Dog()

print(isinstance(d, Animal))    # True
print(isinstance(d, Dog))       # True
print(isinstance(d, str))       # False
```
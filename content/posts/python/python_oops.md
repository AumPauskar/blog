+++
title = 'OOPS with Python and packages'
date = 2023-11-23T13:21:20+05:30
draft = false
tags = ["python", "oops", "programming"]
author = "Aum Pauskar"
description = "A comprehensive guide to OOPS in python and packages"
+++

# Python

## Chapter summary - Unit 1
- Unit 1 \
**Python Fundamentals:** \
**An Introduction to Python programming:** Introduction to Python, IDLE to develop programs; \
**How to write your first programs:** Basic coding skills, data types and variables, numeric data,
string data, five of the Python functions; \
**Control statements:** Boolean expressions, selection structure, iteration structure; \
**Define and use Functions and Modules:** define and use functions, more skills for defining and
using functions and modules, create and use modules, standard modules

### Contents
- What is python? \
Python is a high level interpreted language that is preffered in rapid development of programs due to it's easy and simple syntax.
- IDLE \
IDLE is the short form of _integrated development learning environment_.
- [Data types in python](https://www.geeksforgeeks.org/python-data-types/) \
int(5), string('this is a string' or this is a string), tuple( (5,3,5) ), float(5.3), bool(true/false) ...
- Python interation structure \
Unlike other languages python uses indententation instead of using brackets.

### Comments
Comments are a piece of code that is essentially "dead code" these are essential to show the programmer what the code does and not to do anything. \
Comments in python -
```py
# this is a comment
```

### Basic IO in python
1. Printing a statement \
```py
print("your_message")
```
Putting another variable in the output message
```py
print("your_message", another_variable)
```
- Concatenation
Concatenation is the process of joining two or more strings. Concatenation can be done in python by the following way.
```py
var1 = "hello"
var2 = "world"
print(var1 + " " + var2)
```
Here we have added a space to seperate the hello and the world.

2. Getting input by a python statement
```py
var = input("Please give an input: ")
print(var) # to print out the values
```
3. fstrings \
fstrings make it easier for the user to shove in multiple variables in the same print statement.
```py
fname = "John"
lname = "Doe"
age = 35
# without fstrings
print("Hi my name is" + fname + " " + lname + "my age is" + age)
# with fstrings
print(f"Hi my name is {fname} {lname} my age is {age}")
```

### Function chaining, taking numerical inputs and type casting
Inputs in python can be easily be obtained from the input command, however this command only provides the data to the interpretor as a string to the variable. To change the datatype for the variable we have to use **explicit type casting**. 
```py
num = int(input("Enter a number: "))
type(num)
```
This will give the output as an integer since we have used explicit type conversion. \

**Note** \
Implicit type conversion is when the program automatically changes the datatype of a variable to suit the needs of the further process. Explicit type conversion is when the programmer has to manually change the datatype of a value for the change of the datatype.
### Loops
Python has mainly two loops, these are for and while loops \
For loop is a collection based loop, that is it works by operating on a set where as while works as a condition based loop where the loop operates on a condition.
Syntax of **for loops** \
```py
for i in range(starting_num, ending_num, step):
	# code
```
Python interpretor will prioritise the arguments in the ...range() function in this way ending_num > starting_num > step. So using an
Syntax of **while loops** \
```py
while logical_statement:
	# code
```
Examples of the loops - printing numbers from 1 to 9
```py
# for loop
for i in range(10):
	print(i)
# while loop
while i < 10:
	print(i)
```

### Multiline statements in python
Since python uses indentation for its language instaed of having code inside of brackets it is not natural to write multiline statements inside python. Usage of the "\\" symbol signals the interpretor that its a multiline statement.
```py
# single line statement
print("hello world")
# multi line statement
print("hello\
world")
# single line statement
for i in range(0, 10):
    print(i, end='')
# multi line statement
for i\
	in range(0, 10):
    print(i, end='')
```

### Logical statements
There are a few logical statements in python this includes **if, else, elif, and, or**. \
Example
There are a few logical statements in python this includes **if, else, elif, and, or**. \
The usage of basic if-else statements
Example
```py
# program to check even and odd whole number
num = int(input("Enter a number: "))
if num % 2 == 0:
	print("The number is even")
elif num % 2 == 1:
	print("The number is odd")
else:
	print("The number is not a whole number")
```
The usage of compound if-else statement with and/or
```py
# program to check if a number is even, odd whole number
num = int(input("Enter a number: "))
if num % 2 == 0 and num > 0:
	print("The number is even and whole number")
elif num % 2 == 1 and num > 0>:
	print("The number is odd and whole number")
elif num % 2 == 0 or num < 0:
	print("The number is an even number or not a whole number")
```
### Switch statements
Switch statements are the extension of if-else ladder and built for shotening the syntax. However this feature is only supported on python versions above 3.10. \
Syntax
```py
option = int(input("Options [1, 2, 3] \n Enter choice: "))
match option:
    case 1:
        print("You are a weekday guy: ")
    case 2:
        print("You are a weekend guy: ")
    case 3:
        print("You are a raceweek guy: ")
    case _:
        print("Bruh")
```
- Option can be replaced with the veariable you want the switch to run
- Case 1, 2, 3 can be replaced the the value of variable you want to be and it also supports string values
- The `case _` gives the default value and executes if none of the cases match
### Functions
Functions is a set of code that can be called by the user at anytime based on the need. A function is reusable any number of times. \
Syntax of a function
```py
def function_name(function_parameter1, function_parameter_2):
	# code
	return your_variable # optional
```

### Modules
Modules or packages are a way to package your code into a collective for another program. There are a lot of modules in python such as numpy and math. \
Example
```py
# Import math library
import math

# Round a number upward to its nearest integer
print(math.ceil(1.4))
```
Creating your own package
1. In a python file make functions
2. Save the file in which your other program is present
3. Import the module into your own file. \
[Link](https://www.w3schools.com/python/python_modules.asp)

### Default arguments
Default arguments are the what the funcion seeks to when the user provides no arguments when a function is called.
```py
def myFunction(arg1, arg2, arg3 = 3):
	print(arg1 + arg2 + arg3)

myFunction(1, 2, 7)
myFunction(1, 2)

# O/P
# 10
# 6
```
Default arguments must always be given from right to left

### Global variables
There are two types of variables in python, local and global variables. **Local variables** are only **defined within a function block** and **global variables** are defined within the **whole program**.
```py
x = 10
def plusOne():
	global x
	x += 1

plusOne()
print(x)
```
Typically global variables are frowned upon, since they posess potential security vurnerablities.
### Multiple variable assignments
In python multiple variable values can be assigned in the same line, this can be extensively used if you use a swapping function.
```py
i = 34
j = 41

i, j = j, i
```
This will swap the values


## Chapter summary - Unit 2
**Higher Data Constructs:** Lists and tuples: Basic skills for working with lists, list of lists, more skills for working with lists,
tuples; \
**Dictionaries:** get started with dictionaries, more skills for working with dictionaries; \
**Strings:** Basic skills for working with strings, split and join strings;
Dates and times: get started with dates and times
Text Book 1 – Chapters 6,12,10,11 


### Datatypes - complex
1. Lists: A list is a mutable datatype in which all the elements are indexed from 0 to n
```py
myList = [5,7,3,7]
```
2. Tuples: A tuple is an immutable datatype in which all the elements are indexed from 0 to n
```py
myTuple = (6,2,5,5)
```
3. Dictionaries: A dictionary is a complex mutable datatype in which the elements are indexed upon the user's needs, this is called the key value pairs.
```py
myDict = {"key1":54, "key2":87}
```
4. Sets: A set is a datatype of unordered, unindiexed and non-duplicated elements.
```py
myset = {"apple", "banana", "cherry"}
```

### Lists in python
Lists are a datatype that can hold multiple values of different datatypes and is mutable i.e. values can be changed without fundamentally changing the variable.

- Initialising a list
```py
myList = []
myList2 = [4, 6, 3, 9]
```
- Accessing and printing the list
```py
myList = [3, 5, 6]
print(myList)
print(myList[2])
```
- List methods \
**Note:** In the below example if _return_ is specified means the orignal list is not modified and just returns a value in the variable. If _return_ is not specified means that the list will be **modified.** If the function modifies the orignal list then the function/method **will not be applicable for tuples.**
```py
myList = [4, 3, 6, 6]
myList.append(5) # adds an element
myList.pop(0) # removes an element from list index, returns value
myList.pop() # removes last element, returns value
myList.insert(2, 6) # inserts element at given index (index, value)
myList.remove(4) # removes given element, doesn't return value
myList.count(6) # returns occurances of given element
myList.reverse() # reverses given list
myList.sort() # sorts the list
sorted(myList) # returns sorted list
min(myList) # returns the minimun of the list
max(myList) # returns the maximum of the list
```
Functions that require the random module
```py
import random
random.choice(myList) # returns a random element from the list
random.shuffle(myList) # shuffles the orignal list
```
- List spiclng \
The lists in python can be divided into subparts, this is known as splicing.
```py
myList2 = myList[start : stop : step]
```
Here start gives the value of which index to start from, stop gives the final index and step gives the increment count.

### Shallow and deep copy
There are a couple of difference in how the interpretor accesses a list compared to an immputable object. Whenever an immutable object is referred by another variable it copies the value of the object at that very instance, so if the variable's data is changed the variable's data gets destroyed and a new object is created. So in an nutshell if it's an immutable object then the value remains same even if the host variable's data is changed.
```py
var1 = 10
var2 = var1
print(var2)
var1 = 20
print(var2)
```
In the case of a mutable Object is referred then the interpreter makes a shallow copy of the object what this means is when the host object data is changed the others variables data also changes. The other variable doesn't take the exact snapshot of the variable when the object was first referred to the variable references the variable and if the host variable changes the second variable also changes.
```py
list1 = [2, 4, 5]
list2 = list1
print(list2)
list1.append(5)
print(list2)
```
To remove this anomaly python introduces a new module called as copy. So as we have seen in the previous instances the python interpreter makes a shallow copy of the object. With the use of the copy Module we can make a deep copy of the object that is given above . With the deep copy method if the main object is changed the secondary object takes an exact snapshot of the main object and even after the main object changes the secondary object never changes.
```py
import copy
cpyList1 = [1, 2, 3]
cpyList2 = copy.deepcopy(cpyList1)
print(cpyList2)
cpyList1.append(4)
print(cpyList2)
```

### Tuples
Tuples are the mutable conterpart of lists. This is an **ordered, indexed and immutable** datatype. Almost all the list methods are compatable except those which change lists value.

Refer the list functions above where the orignal list is not modified. If the functions/methods **don't modify** the orignal list then the function is **also applicable for tuples.**

```py
# creating a tuple
tup = (4, 3, "hello")

# creating a one element tuple
singleTup = (3,)
```

### Sets
Sets are **ordered, unindexed, immutable** datatype with **no duplicates**.
```py
# creating a set
mySet = {4, 6, 7}
```

### Dictionary
Dictionaries are ordered indexed and mutable datatype with custiom key-value pairs.
```py
# creating a dictionary
dict = {"key": "value"}

# obtaining values
print(dict["key"])
```
Using a for loop to print out keys and values of the text
```py
myDict = {"key1": 4, "key2": 5, "key3": 2, "key4": 7}

print("Printing the keys")
for i in myDict:
	print(i, end=", ")

print("\nPrinting the values")
for i in myDict:
	print(myDict[i], end=", ")
```
**Note:** There are a couple of points to remember when working with dictionaries. The value of an item can be anything, however the key of an item is only limited to **immutable datatypes and no duplicates.**

Dictionary methods
```py
myDict.clear() # Removes all the elements from the dictionary
myDict.copy() # Returns a copy of the dictionary
myDict.fromkeys() #Returns a dictionary with the specified keys and value
myDict.get() # Returns the value of the specified key
myDict.keys() # Returns a list containing the dictionary's keys
myDict.pop() # Removes the element with the specified key
myDict.popitem() # Removes the last inserted key-value pair
myDict.update()	# Updates the dictionary with the specified key-value pairs
myDict.values()	# Returns a list of all the values in the dictionary
```
### Strings
A string is a combination of more than one charecters.
- [String operations](https://www.w3schools.com/python/python_ref_string.asp)
1. capitalize()
2. count()
3. find()
4. isalnum()
5. isdigit()...
### Creation and modification of datetime
- Showing values
```py
import datetime

x = datetime.datetime.now()

print(x.year)
print(x.strftime("%A"))
```
- Creating objects
```py
import datetime

x = datetime.datetime(2020, 5, 17)

print(x)
```


## Chapter summary - Unit 3
**File I/O:** An introduction to file I/O, test files, CSV files, binary files; \
**Exception Handling:** handle a single exception, handle multiple exceptions, Two more skills; \
**Work with a database:** An introduction to relational databases, SQL statements for data
manipulation, SQLite Manager to work with a database, use Python to work with a database

### File write modes
1. "x" - Create - will create a file, returns an error if the file exist
2. "a" - Append - will create a file if the specified file does not exist
3. "w" - Write - will create a file if the specified file does not exist
```py
f = open("myfile.txt", "x")
```
This will create a file object, and operations can be made from the folllowing file object.


### Working with csv files
- Writing to a csv file
1. import csv module
2. obtain the writer object
```py
writer = csv.writer(file)
```
3. write data to the csv file
```py
writer.writerows(data)
```

- Reading from a csv file
1. import csv module
2. ontain the reader onject
```py
reader = csv.reader(file)
```
3. read data using the reader obbject
```py
for line in reader:
	print(line)
```

- Example of working with a simple csv file
```py
import csv

myData = [['val', 'data'],['val2', 'data2']]
with open ('data.csv', 'w') as file:
	writeObj = csv.writer(file)
	writeObj.writerows(myData)
```
Output
```
val,data

val2,data2


```

- Example of working with a csv files with fields
```py
import csv

fields = ['no', 'name', 'championships']
rows = [ ['1', 'Schumacher', '7'],
		['2', 'Hamilton', '7'],
		['3', 'Prost', '4'],
		['4', 'Senna', '3'],
		['5', 'Fangio', '5'],
		['6', 'Clark', '3']]

with open ('data.csv', 'w', newline = '') as file:
	writeObj = csv.writer(file)
	writeObj.writerow(fields)
	writeObj.writerows(rows)
```
Output
```
no,name,championships
1,Schumacher,7
2,Hamilton,7
3,Prost,4
4,Senna,3
5,Fangio,5
6,Clark,3
```
- Example of reading from a csv file
```py
import csv

with open ('data.csv', 'r') as file:
	readObj = csv.reader(file)
	for line in readObj:
		print(line)
```
Output
```
['val', 'data']                                                                                                                       
[]                                                                                                                                    
['val2', 'data2']                                                                                                                     
[]       
```

- Example of working with binary files in python \
Binary files can be opened with the pickle module

```py
# writing binary file
import pickle
with open ("file.bin", "wb") as binFile:
	text = "This is a string of text"
	pickle.dump(text, binFile)

# reading binary file
with open ("File.bin", "rb") as binFile:
	print(pickle.load(binFile))

```

### Exception handling in python
Whenever an error is occured any program spits out an error message and genrally terminates the program. With exception hadling in python, the interpretor manages the error in a specific way and enables the user to handle the exception in a custom manner. \
Exception handling in python
```py
x = 5
y = "hello"
try:
    z = x + y
except:
    print("Error: cannot add an int and a str")
```
This error code can be also written in this way to specify the custom error.
```py

x = 5
y = "hello"
try:
    z = x + y
except TypeError:
    print("Error: cannot add an int and a str")
```
Here type error is a custom error, this can be replaced by the [following errors](https://www.geeksforgeeks.org/python-exception-handling/).

- Raising an exception in python \
A standard exception in python can be raised whenever a condition is met
```py
# program to determine if a number is positive or not
num = int(input("Enter a number"))
if num >= 0:
	print("Number is a positive number")
else:
	raise ValueError("Negetive numbers entered")
```

- Use of finally in python
The **finally clause is executed regardless of whether or not an exception occurs** in the try block. The **finally clause is often used to close files or free up resources.**

Here is an example of how to use the finally clause with the try...except statement:
```py
def divide(x, y):
  try:
    return x / y
  except ZeroDivisionError:
    print("Division by zero")
  finally:
    print("Closing file")

print(divide(10, 2))
```
### SQLite with Python

SQLite is a lightweight, embedded relational database management system (RDBMS) that is included in the Python standard library. It is a popular choice for storing small to medium-sized amounts of data, and it is often used in web applications, desktop applications, and scientific computing.

To use SQLite with Python, you can import the `sqlite3` module. This module provides a simple API for creating, connecting to, and querying SQLite databases.

Here is an example of how to create a new SQLite database and add a row to it:

```py
import sqlite3

# Create a connection to a new database file
conn = sqlite3.connect("my_database.db")

# Create a cursor object
cur = conn.cursor()

# Create a table
cur.execute("CREATE TABLE my_table (name TEXT, age INTEGER)")

# Insert a row
cur.execute("INSERT INTO my_table (name, age) VALUES ('John Doe', 30)")

# Commit the changes
conn.commit()

# Close the connection
conn.close()
```

You can also use the `sqlite3` module to query SQLite databases. Here is an example of how to select all rows from the `my_table` table:


```py
import sqlite3

# Create a connection to the database
conn = sqlite3.connect("my_database.db")

# Create a cursor object
cur = conn.cursor()

# Select all rows from the my_table table
cur.execute("SELECT * FROM my_table")

# Fetch the results
rows = cur.fetchall()

# Print the results
for row in rows:
    print(row)

# Close the connection
conn.close()
```

#### Operations in SQlite
1. Fetchall - Fetches all the rows and columns as a array 
2. Fetchone - Fetches one line in the form of a string (recursive call needed)
3. Commit - Commit the saves
4. Execute - Runs the command in the command script

## Chapter summary - Unit 4
**Object Oriented Programming:**
Define and use your own classes: An introduction to classes and objects, define a class,
object composition, encapsulation; \
**Inheritance:** Inheritance, override object methods; \
**Design an object oriented program:** Techniques for object-oriented design
Text Book 1 – Chapters 14,15,16

### Creating your own class
A class can be created in python by using the class keyword
```py
class MyClass:
  x = 5
```
This creates a blueprint for the objects to be defined. Methods and members can be defined in the class.

### Constructors
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

### Lambda functions
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

### Encapsulation
Encapsuation is the way of wrapping the data and the functions withing a class isolated from the ouytside interference. Encapsualation can be achieved in python by using private and public attributes at stretigic places to ensure the data safety. 

```py
class MyData:
	# constructor to get the data
	def __init__(self, val):
		self.__x = val
	def printData(self):
		print(self.__x)
```

### Inheritance
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

#### IsInstance in python

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

## Virtual environments in python
Before proceeding to the packages module in python, it is important to know about virtual environments. Note that you may proceed to packages without knowing about virtual environments, however it is recommended to know about virtual environments because it helps in keeping isolated packages for different projects as some deprecated packages might not work on newer projects and similarly newer packages may not work on legacy projects.

### Requiremnets
1. Python 3
2. Pip

### Steps
1. Installing virtual environemnt package
	- Windows
		```bat
		pip install virtualenv
		```
	- Linux
		```
		pip3 install virtualenv
		```

2. Creating virtual environent
	- Windows - cmd/powershell
		```ps
		py -m venv {your_env_name}
		```
	- Linux
		```bash
		python3 -m venv myworld
		```

3. Activating virtual environemt
	- Windows - cmd
		```bat
		myworld\Scripts\activate.bat
		```
	- Windows - powershell
		```ps
		myworld\Scripts\activate.ps1
		```
	- Linux
		```bash
		source myworld/bin/activate
		```

4. Downloading required packages
	- Windows
		```ps
		py -m pip install {required_package}
		```
	- Linux
		```bash
		python3 -m pip3 install {required_package}
		```

## Chapter summary - Unit 5
**Packages:**
How to build a GUI Program: Create a GUI that handles an event, more skills for working
with components; \
**Numpy Basics:** Arrays and Vectorized Computation: Creating ndarrays, Data Types for
ndarrays, Operations between Arrays and Scalars, Basic Indexing and Slicing, Indexing with
slices, Boolean Indexing, Transposing Arrays and Swapping Axes; \
**Getting started with Pandas:** Introduction to Pandas Data Structures, Summarizing and
Computing Descriptive Statistics, Handling missing data; \
**Plotting and Visualization:** A Brief matplotlib API Primer, Plotting Functions in panda

### GUI with Tkinter
Tkinter is a package in python that aids graphical applications. Installation of Tkinter can be done by
```
pip install tkinter
```

#### Creating a window
```py
from tkinter import *
root = Tk()

root.mainloop()
```
Mainloop aids the program in running recursively. This can be further improved by naming each part of the root window.
```py
from tkinter import *

# root properties
root.title('rootname')
root.geometry('640x360')

root.mainloop()
```

- Widgets: Widgets are the graphical objects that are found in tkinter. This inclues the root window all the labels and the entry field etc. The widgets should be mapped to other objects in order to work which can be a **canvas** or the **root** window as a base window.

Some example of widgets
1. Label: displays text or image on the screen
2. Button: adds a clickable button to the application
3. Entry: allows single line text input from user
4. Text: allows multi-line text input and formatting
5. Frame: holds and organizes other widgets
6. Scale: provides a graphical slider to select a value
7. Listbox: displays a list of items to choose from
8. Checkbutton: displays a toggle button with two states (on/off)
9. Radiobutton: displays a button that can be selected from a group of buttons 

Calling function in tkinter
```py
from tkinter import *
root = Tk()

def change():
	label1.config(text = "New text")

label1 = Label(root, text = "Sample text")
label1.pack()
button = Button(root, command=change)
root.mainloop()
```

An application made in Tkinter
```py
# importing main module
from tkinter import *

# root functionalities
root = Tk()
root.title('Calculator')
root.geometry('640x360')

# will house the display
canvas1 = Canvas(root)
canvas1.pack()

# will house the buttons
canvas2 = Canvas(root)
canvas2.pack()

num1 = 0
num2 = 0
# ------------------------------

# functions
def fnInitialize():
	global num1, num2
	num1 = float(entryNum1.get())
	num2 = float(entryNum2.get())

def fnAddNum():
	fnInitialize()
	ans = num1 + num2
	labelAnsVal.config(text = f"Answer: {str(round(ans, 2))}")

def fnSubNum():
	fnInitialize()
	ans = num1 - num2
	labelAnsVal.config(text = f"Answer: {str(round(ans, 2))}")

def fnMulNum():
	fnInitialize()
	ans = num1 * num2
	labelAnsVal.config(text = f"Answer: {str(round(ans, 2))}")

def fnDivNum():
	fnInitialize()
	ans = num1 / num2
	labelAnsVal.config(text = f"Answer: {str(round(ans, 2))}")

# ------------------------------
# widgets

# first number prompt
lablelNum1 = Label(canvas1, text = "Enter num 1:")
lablelNum1.grid(row = 1, column = 1)

# first number will be here
entryNum1 = Entry(canvas1)
entryNum1.grid(row = 1, column = 2)

# second number prompt
lablelNum2 = Label(canvas1, text = "Enter num 2:")
lablelNum2.grid(row = 2, column = 1)

# second number will be here
entryNum2 = Entry(canvas1)
entryNum2.grid(row = 2, column = 2)

# answer prompt
lablelAns = Label(canvas1, text = "Answer")
lablelAns.grid(row = 3, column = 1)

# answer label
labelAnsVal = Label(canvas1)
labelAnsVal.grid(row = 3, column = 2)

# addition button
ButtonAdd = Button(canvas2, text = "Add", command = fnAddNum)
ButtonAdd.grid(row = 1, column = 1)

# subtraction button
ButtonSub = Button(canvas2, text = "Sub", command = fnSubNum)
ButtonSub.grid(row = 1, column = 2)

# multiplication button
ButtonMul = Button(canvas2, text = "Mul", command = fnMulNum)
ButtonMul.grid(row = 1, column = 3)

# division button
ButtonDiv = Button(canvas2, text = "Div", command = fnDivNum)
ButtonDiv.grid(row = 1, column = 4)

# looping trough the program
root.mainloop()
```

### Numpy
The numpy library is a python library that can be used to manupulate and work on complex numberical applications. NumPy supports numpy array which is ideal to perform large array operations since the faster access time. The NumPy library also supports broadcasting which is performing an operation throughout the array without using a for loop.

#### N dimentional array (Nd Array)
- Why is NumPy faster than lists
1. NumPy arrays are stored at one continuous place in memory unlike lists, so processes can access and manipulate them very efficiently.
2. This behavior is called locality of reference in computer science.
3. This is the main reason why NumPy is faster than lists. Also it is optimized to work with latest CPU architectures.
4. Operating on the elements in a list can only be done through iterative loops, which is computationally inefficient in Python.
5. The NumPy package enables users to overcome the shortcomings of the Python lists by providing the data storage object called ndarray
6. The ndarray is similar to lists, but rather than being highly flexible by storing different types of objects in one list, only the same type of element can be stored in each column.
7. For example, with a Python list, you could make the first element a list and the second another list or dictionary. With NumPy arrays, you can only store the same type of element, e.g., all elements must be floats, integers, or strings.
8. Despite this limitation, ndarray wins hands down when it comes to operation times, as the operations are sped up significantly.

- Creating ND array
```py
import numpy as np
nDarr = np.array(5) # creating a scalar array
nDarr1 = np.array([5,6]) # creating a 1d array
nDarr2 = np.array([[1, 2], [3, 4]]) # creating a 2d array

# finding the shape of the arrays
print(nDarr.ndim)
print(nDarr1.ndim)
print(nDarr2.ndim)

# finding the dimentions of the arrays
print(nDarr.shape)
print(nDarr1.shape)
print(nDarr2.shape)
```

- Slicing the ND array
```py
import numpy as np
nDarr = np.array(5) # creating a scalar array
nDarr1 = np.array([5,6]) # creating a 1d array
nDarr2 = np.array([[1, 2], [3, 4]]) # creating a 2d array

print(nDarr1[0:1])
```
The slicing works in a similar fashion as compared to for loops (except the step). You can nest string slicing to reduce the dimentions of the nDarray.
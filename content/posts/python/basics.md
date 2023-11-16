+++
title = 'Basics'
date = 2023-11-16T10:05:13+05:30
draft = false
description = "Basics of python"
+++

# Chapter summary - Unit 1
- Unit 1 \
**Python Fundamentals:** \
**An Introduction to Python programming:** Introduction to Python, IDLE to develop programs; \
**How to write your first programs:** Basic coding skills, data types and variables, numeric data,
string data, five of the Python functions; \
**Control statements:** Boolean expressions, selection structure, iteration structure; \
**Define and use Functions and Modules:** define and use functions, more skills for defining and
using functions and modules, create and use modules, standard modules

## Contents
- What is python? \
Python is a high level interpreted language that is preffered in rapid development of programs due to it's easy and simple syntax.
- IDLE \
IDLE is the short form of _integrated development learning environment_.
- [Data types in python](https://www.geeksforgeeks.org/python-data-types/) \
int(5), string('this is a string' or this is a string), tuple( (5,3,5) ), float(5.3), bool(true/false) ...
- Python interation structure \
Unlike other languages python uses indententation instead of using brackets.

## Comments
Comments are a piece of code that is essentially "dead code" these are essential to show the programmer what the code does and not to do anything. \
Comments in python -
```py
# this is a comment
```

## Basic IO in python
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

## Function chaining, taking numerical inputs and type casting
Inputs in python can be easily be obtained from the input command, however this command only provides the data to the interpretor as a string to the variable. To change the datatype for the variable we have to use **explicit type casting**. 
```py
num = int(input("Enter a number: "))
type(num)
```
This will give the output as an integer since we have used explicit type conversion. \

**Note** \
Implicit type conversion is when the program automatically changes the datatype of a variable to suit the needs of the further process. Explicit type conversion is when the programmer has to manually change the datatype of a value for the change of the datatype.
## Loops
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

## Multiline statements in python
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

## Logical statements
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
## Switch statements
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
## Functions
Functions is a set of code that can be called by the user at anytime based on the need. A function is reusable any number of times. \
Syntax of a function
```py
def function_name(function_parameter1, function_parameter_2):
	# code
	return your_variable # optional
```

## Modules
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

## Default arguments
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

## Global variables
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
## Multiple variable assignments
In python multiple variable values can be assigned in the same line, this can be extensively used if you use a swapping function.
```py
i = 34
j = 41

i, j = j, i
```
This will swap the values

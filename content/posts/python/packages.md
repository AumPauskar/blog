+++
title = 'Packages'
date = 2023-11-16T10:08:09+05:30
draft = false
+++

# Chapter summary - Unit 5
**Packages:**
How to build a GUI Program: Create a GUI that handles an event, more skills for working
with components; \
**Numpy Basics:** Arrays and Vectorized Computation: Creating ndarrays, Data Types for
ndarrays, Operations between Arrays and Scalars, Basic Indexing and Slicing, Indexing with
slices, Boolean Indexing, Transposing Arrays and Swapping Axes; \
**Getting started with Pandas:** Introduction to Pandas Data Structures, Summarizing and
Computing Descriptive Statistics, Handling missing data; \
**Plotting and Visualization:** A Brief matplotlib API Primer, Plotting Functions in panda

## GUi with Tkinter
Tkinter is a package in python that aids graphical applications. Installation of Tkinter can be done by
```
pip install tkinter
```

### Creating a window
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

## Numpy
The numpy library is a python library that can be used to manupulate and work on complex numberical applications. NumPy supports numpy array which is ideal to perform large array operations since the faster access time. The NumPy library also supports broadcasting which is performing an operation throughout the array without using a for loop.

### N dimentional array (Nd Array)
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
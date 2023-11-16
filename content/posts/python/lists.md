+++
title = 'Lists'
date = 2023-11-16T10:07:18+05:30
draft = false
+++

# Chapter summary - Unit 2
**Higher Data Constructs:** Lists and tuples: Basic skills for working with lists, list of lists, more skills for working with lists,
tuples; \
**Dictionaries:** get started with dictionaries, more skills for working with dictionaries; \
**Strings:** Basic skills for working with strings, split and join strings;
Dates and times: get started with dates and times
Text Book 1 – Chapters 6,12,10,11 


## Datatypes - complex
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

## Lists in python
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

## Shallow and deep copy
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

## Tuples
Tuples are the mutable conterpart of lists. This is an **ordered, indexed and immutable** datatype. Almost all the list methods are compatable except those which change lists value.

Refer the list functions above where the orignal list is not modified. If the functions/methods **don't modify** the orignal list then the function is **also applicable for tuples.**

```py
# creating a tuple
tup = (4, 3, "hello")

# creating a one element tuple
singleTup = (3,)
```

## Sets
Sets are **ordered, unindexed, immutable** datatype with **no duplicates**.
```py
# creating a set
mySet = {4, 6, 7}
```

## Dictionary
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
## Strings
A string is a combination of more than one charecters.
- [String operations](https://www.w3schools.com/python/python_ref_string.asp)
1. capitalize()
2. count()
3. find()
4. isalnum()
5. isdigit()...
## Creation and modification of datetime
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

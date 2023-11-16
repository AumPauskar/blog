+++
title = 'Data'
date = 2023-11-16T10:06:26+05:30
draft = false
+++

## Chapter summary - Unit 3
**File I/O:** An introduction to file I/O, test files, CSV files, binary files; \
**Exception Handling:** handle a single exception, handle multiple exceptions, Two more skills; \
**Work with a database:** An introduction to relational databases, SQL statements for data
manipulation, SQLite Manager to work with a database, use Python to work with a database

## File write modes
1. "x" - Create - will create a file, returns an error if the file exist
2. "a" - Append - will create a file if the specified file does not exist
3. "w" - Write - will create a file if the specified file does not exist
```py
f = open("myfile.txt", "x")
```
This will create a file object, and operations can be made from the folllowing file object.


## Working with csv files
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

## Exception handling in python
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
## SQLite with Python

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

### Operations in SQlite
1. Fetchall - Fetches all the rows and columns as a array 
2. Fetchone - Fetches one line in the form of a string (recursive call needed)
3. Commit - Commit the saves
4. Execute - Runs the command in the command script
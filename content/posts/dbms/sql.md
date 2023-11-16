+++
title = 'Sql'
date = 2023-11-16T14:41:25+05:30
draft = false
+++

# Sql documentation

## Installation
The installation and usage of MySQL can be done in many ways; one is to install WAMP/XAMPP server and using SQL through it another is to use an [online sql emulator](https://www.programiz.com/sql/online-compiler/), the best way is to use a [MySQL server](https://dev.mysql.com/downloads/installer/).  
## Getting started with MySQL

All the operations in SQL can be classified into 3 types \
**DDL:** Data definition language includes operation like **create, alter, drop** \
**DML:** Data manipulation language includes operation like **select, insert, update, delete** \
**DCL:** Data control language includes operations like **commit, rollback, grant, revoke**

## Basic commands

1. Showing all the databases \
There are diffenet databases that resides inside your computer at any point of time. Using this command shows all the avalable databases on your local machine.
```sql
SHOW DATABASES;
```

2. Creating a database \
To use or import and use a database, a database should always be created
```sql
CREATE DATABASE DATABASE_NAME
```

3. Using a database \
To view/edit/modify table data the _use_ keyword is used to enter a database.
```sql
USE DATABASE_NAME
```
4. Showing all the tables within a table \
There can be multiple table with a database.
```sql
SHOW TABLES;
```
5. Showing all the data from a database \
The _*_ keyword is for all in MySQL, you can also use individual column names to show the data.
```sql
SELECT * FROM TABLE_NAME;
```
6. Fully deleting a database **drop database** \
There are two types of deletion in SQL one is _delete_ which just deletes the values inside the table and not deletes the whole table, meanwhile using the _drop_ keyword deletes the table along with the table structure.
```sql
DROP DATABASE_NAME;
```
6. Fully deleting a table **drop table** \
```sql
DROP TABLE_NAME;
```

## Creating tables in MySQL
Tables can be created in MySQL by using the create command.
```sql
CREATE TABLE TABLE_NAME (
COLUMN_NAME DATATYPE CONSTRAINTS
COLUMN_NAME DATATYPE CONSTRAINTS
COLUMN_NAME DATATYPE CONSTRAINTS

PRIMARY KEY (COLUMN_NAME));
```
Note that using constraints and primary key is optional, but highly reccommended since they reduce the potential errors in the future.

## Datatypes in MySQL
There are 3 major datatypes in MySQL namely string, numeric and datetime datatypes.

| Srno | Name | Use | Type |
| ----- | ----- | ----- | ----- |
| 1 | CHAR(SIZE) | Stores a fixed length charecter | string |
| 2 | VARCHAR(SIZE) | Stores a variable length charecter | string |
| 3 | TEXT(SIZE) | Stores text | string |
| 4 | INT | Stores integer | numeric |
| 5 | FLOAT(PRECISION) | Stores float | numeric |
| 6 | DATE | Stores date in YYYY/MM/DD format | datetime |
| 7 | DATETIME | Stores date and time | datetime |
| 8 | TIMESTAMP | Stores time | datetime |

## Wildcards



## Modifying tables
A SQL table can be modified by the use of the alter command.

1. Adding a column
```sql
ALTER TABLE table_name
ADD column_name datatype;
```
2. Removing a column
```sql
ALTER TABLE table_name
DROP column_name;
```
3. Renaming a column
```sql
ALTER TABLE table_name
RENAME COLUMN old_name to new_name;
```
4. Changing column datatype
```sql
ALTER TABLE table_name
MODIFY COLUMN column_name datatype;
```

## Updating and deleting values

- Command for deleting
This deletes a column from the sql table
```sql
DELETE FROM TABLE_NAME
WHERE VALUE = ‘123456789’;
```
This deletes all the values but retains the table structure
```sql
DELETE FROM TABLE_NAME;
```

## College stuff
Problem statement

1. Retrieve the details of all employees working in the company.

```sql
SELECT * FROM EMPL;
```
2. Retrive the firstname, lastname, ssn, salary of all the employees.
```sql
SELECT FNAME, LNAME, SSN, SAL FROM EMPL;
```
3. Display the details of all the employees whose SSN is H55.
```sql
SELECT * FROM EMPL WHERE SSN = H55;
```

Problem statement
1. Find the sum of salaries of all the employees, the max sal, min sal and the avg sal
```sql
SELECT MAX(SAL) FROM EMPL;
SELECT AVG(SAL) FROM EMPL;
SELECT MIN(SAL) FROM EMPL;
```
2. Retrieve the total no of employes in the company.
```sql
SELECT COUNT(*) FROM EMPL;
```
3. Retrieve the total no of employes in the research department
```sql
SELECT * FROM EMPL WHERE DEPT = "RESEARCH";
```
4. Count the number of distinct salary values in the database
```sql
SELECT COUNT(DISTINCT SAL) FROM EMPL;
```

Updating SQL tables
```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

## Extra stuff
redis, sql vs nosql, graph database

- **REDIS:** Redis (remote dictionary server) is an in memory database highly optimized to store and serve data which needs to be retrived and modified faster, something like metadata of a server.

## Relational algebra
These are the following signs used in relational algebra and the use of them.
1. The Select operator: The select operator is used in horizontal partitioning i.e. showing all the rows and columns selected its symbol is **$\sigma$**. Select is commutative, although using two or more select statements is very seldom.
2. The project operator: The project operator is used to show all rows selected however very rarely this includes all columns and selected columns need to be specified. Its symbol is **$\pi$**. Project is not commitative.
3. Rename operation: The rename operation is denoted by the symbok **$\rho$**.
4. Union operator: The union operator is denoted by the symbol **$\cup$**.
5. Intersection operator: The intersection operator is denoted by the symbol **$\cap$**.
6. Set difference operator: The set difference operator is denoted by the symbol **-**.
7. Join operator: The join operator is denoted by the symbok **$\bowtie$**. The operator shown here is the natural jon, for outer join there are 3 types, namely left outer join, right outer join and full outer join. There also exists another function called as equijoin.
8. Aggregate functions: The **F** symbol is used to display aggregate function.
9. Division: Division can be used to divide the rows and columns where the argument or the data in column 1 matched with column 2.

## Anomalies
Database anomalies
There are 3 kinds of database anomalies, update anomaly, insert anomaly and delete anomaly. Changing of data using update may change the values for all the tuples which inlclude the same key. Same with insert with the databases being not assigned. Delete causing all the tuples related to a certain value being deleted.

- Ways to reduce this
1. Minimize NULL values
2. There should not be any spurious values (repeted values)
3. Join relations using equijoin

- Partial Dependency: When an non-key attribute is determined by a part, but not the whole, of a COMPOSITE primary key.
- Transitive Dependency: When a non-key attribute determines another non-key attribute.

## Normalization of data
Data and database creation may be a tedious task with multiple tables, multiple values and these stuff may bring out a error in the long term of the lifeycle of the program. This might also be suboptimal in the lifespan of the program. To resolve this we use normal forms and normalisation of data there are 4 forms of normalization that will be covered in this part and will follow **ACID**.
1. 1NF: **Atomicity** refers to the deletion of multivalued attribute.
2. 2NF: **Complete** dependency refers to the removal of any partial dependency of one column to other.
3. 3NF: Transitive dependency refers to the removal of any transitive properties in which 
4. BCNF: BCNF states that the left side of any key must be candidate key or super key.

## Transactions
- Singleuser
- Multiusers
- Concurrency
	- Interleaved processing
	- Parallel processing

**What is a transaction?** \
**Why is transaction recovery needed?**

- Type of transaction failure
	- Computer failure
	- Transaction failure
	- Local errors
	- Concurrency enforcement
	- Disk failure
	- Physical problem 

- Desirable properties of transaction
	- Atomicity
	- Consistency
	- Isolation
	- Durablity

- Possible problems
	- Lost update problem
	- Remproary update problem
	- Incorrect summary problem

- 2PL
	- Growing phase
	- Shrinking phase

- Lock based protocols
	- Shared lock
	- Exclusive lock
	
- Composite vs candiadte key vs super key

## PL/SQL
PL/SQL stands for procedural language  sql developed by oracle in the 1980s to give procedural generated sql code. This can be used in mysql in the following way.

```sql
DELIMITER //

CREATE PROCEDURE HelloWorld()
BEGIN
    SELECT 'Hello, World!' AS Message;
END //

DELIMITER ;

-- To execute the stored procedure and see the output
CALL HelloWorld();
```
However before writing the code the user must select the database on which the PLSQL should be run upon whether operating on that very database or working independently.

Code for generating fibonacci series in PLSQL
```sql
DELIMITER //

CREATE PROCEDURE GenerateFibonacci(IN n INT)
BEGIN
    DECLARE a INT DEFAULT 0;
    DECLARE b INT DEFAULT 1;
    DECLARE i INT DEFAULT 2;
    
    IF n = 0 THEN
        SELECT 0 AS Fibonacci;
    ELSEIF n = 1 THEN
        SELECT 0 AS Fibonacci UNION ALL SELECT 1;
    ELSE
        SELECT 0 AS Fibonacci;
        SELECT 1 AS Fibonacci;
        
        WHILE i <= n DO
            SET @temp := a + b;
            SET a := b;
            SET b := @temp;
            
            SELECT @temp AS Fibonacci;
            
            SET i := i + 1;
        END WHILE;
    END IF;
END //

DELIMITER ;

CALL GenerateFibonacci(10); -- Replace 10 with the desired input value
```
Note that when you are declaring variables the name of the variable comes first followed by the variable type. The delimiter only works if you are using mysql and if an older oracle database is being used then it is not needed.

Code to check whether a number is prime or not
```sql
DELIMITER //

CREATE FUNCTION IsPrime(number INT) RETURNS BOOLEAN
BEGIN
    DECLARE i INT;
    
    IF number <= 1 THEN
        RETURN FALSE;
    END IF;

    IF number <= 3 THEN
        RETURN TRUE;
    END IF;

    IF number % 2 = 0 OR number % 3 = 0 THEN
        RETURN FALSE;
    END IF;

    SET i = 5;

    WHILE i * i <= number DO
        IF number % i = 0 OR number % (i + 2) = 0 THEN
            RETURN FALSE;
        END IF;
        SET i = i + 6;
    END WHILE;

    RETURN TRUE;
END //

DELIMITER ;

-- call function here
SELECT IsPrime(17); -- Replace 17 with the number you want to check
```

### Loops in PL/SQL
In MySQL, you can use loops to repeat a block of code multiple times until a certain condition is met. There are two main types of loops in MySQL: `WHILE` loops and `LOOP` loops.

1. WHILE Loops:

   A `WHILE` loop repeats a block of code as long as a specified condition evaluates to `TRUE`. Here's the basic structure of a `WHILE` loop:

   ```sql
   WHILE condition DO
       -- Code to be executed repeatedly
   END WHILE;
   ```

   For example, you can use a `WHILE` loop to iterate over a set of rows in a table:

   ```sql
   DECLARE counter INT DEFAULT 0;
   
   WHILE counter < 10 DO
       -- Code to be executed repeatedly
       SET counter = counter + 1;
   END WHILE;
   ```

   In this example, the loop will continue executing as long as the `counter` variable is less than 10.

2. LOOP Loops:

   A `LOOP` loop is an unconditional loop that continues to execute until you explicitly use the `LEAVE` statement to exit the loop. Here's the basic structure of a `LOOP` loop:

   ```sql
   LOOP
       -- Code to be executed repeatedly
       IF condition THEN
           LEAVE;
       END IF;
   END LOOP;
   ```

   You can use a `LOOP` loop when you need to perform an action at least once and then decide whether to continue or exit based on a condition.

   Here's an example:

   ```sql
   DECLARE counter INT DEFAULT 0;

   LOOP
       -- Code to be executed repeatedly
       SET counter = counter + 1;

       IF counter >= 10 THEN
           LEAVE;
       END IF;
   END LOOP;
   ```

   In this example, the loop will execute at least once and then exit when the `counter` variable is greater than or equal to 10.

Loops can be useful in MySQL for tasks such as iterating through result sets, implementing control structures, and performing repetitive calculations. However, it's important to use them carefully to avoid infinite loops, which can lead to high resource consumption and system instability. Always ensure that your loop conditions will eventually evaluate to `FALSE` to exit the loop.

Program for generating fibonacci serie

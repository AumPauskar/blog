+++
title = 'MongoDB'
date = 2024-06-27T23:21:23+05:30
tags = ["dbms", "nosql", "database", "cheatsheet", "nosql"]
author = "Aum Pauskar"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "A show tutorial on how to work with a NoSQL database using MongoDB"
disableShare = false
disableHLJS = false
hideSummary = false
searchHidden = true
ShowReadingTime = true
ShowBreadCrumbs = true
ShowPostNavLinks = true
ShowWordCount = true
ShowRssButtonInSectionTermList = true
UseHugoToc = true
[editPost]
    URL = "https://github.com/AumPauskar/blog/content/posts/"
    Text = "Suggest Changes"
    appendFilePath = true
+++

# MongoDB

## Introduction 
NoSQL databases are non-relational databases that are used to store and retrieve data. MongoDB is a popular NoSQL database that is used to store data in the form of documents.

| Feature                | SQL (Relational Databases)                                                                 | NoSQL (Non-Relational Databases)                                                                                   |
|------------------------|-------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| Schema                 | Fixed schema                                                                              | Dynamic schema for unstructured data                                                                               |
| Scalability            | Vertical scalability (scale-up by adding more powerful CPU, RAM, SSD)                     | Horizontal scalability (scale-out by adding more servers)                                                          |
| Complexity             | Tables with rows and columns, complex queries with JOINs                                  | Document, key-value, wide-column, or graph formats, simpler queries                                                 |
| Transactions           | ACID properties (Atomicity, Consistency, Isolation, Durability) for reliable transactions | BASE properties (Basically Available, Soft state, Eventual consistency) less strict than ACID                      |
| Development Model      | Mature, with established standards                                                        | More flexible and evolving rapidly                                                                                  |
| Use Cases              | Well-suited for complex queries and transactions, e.g., banking systems                   | Well-suited for hierarchical data storage, big data solutions, and real-time web applications                      |
| Data Integrity         | High, due to ACID compliance                                                              | Variable, depending on the specific NoSQL system and its configuration                                             |
| Query Language         | Structured Query Language (SQL) is standardized                                           | No standard; queries are based on the specific NoSQL database system (e.g., MongoDB uses BSON)                     |
| Relationship Handling  | Efficient handling of relationships between entities                                      | Relationships can be handled, but often less efficiently than SQL databases; denormalization is commonly practiced |

## Installation
There are two ways of working with a mongoDB database, one is to run it locally on your machine and the other is to use a cloud service like MongoDB Atlas. For this tutorial, we will be using MongoDB with mongosh and compass installed.

**What is mongosh and what is compass?**\
MongoDB Shell (mongosh) is a shell-centric cross-platform MongoDB shell that provides a rich programming experience for MongoDB. MongoDB Compass is the GUI for MongoDB. It allows you to explore your data, run queries, and interact with your data with full CRUD functionality.

**Installation can be found here**
- [MongoDB - compass included](https://www.mongodb.com/try/download/community)
- [MongoDB - mongosh](https://www.mongodb.com/try/download/shell)

## Basics of MongoDB
MongoDB stores data in the form of documents. A document is a data structure composed of field and value pairs. MongoDB documents are similar to JSON objects. The values of fields may include other documents, arrays, and arrays of documents.

## Commands 

### Basics
- **Launching mongo:** To launch mongoDB from the terminal, type `mongosh` and hit enter. This should open a mongo shell provided you have installed it and rebooted your computer.
- **Showing databases:** To show all the existing databases on the server, type `show dbs`.
- **Creating a database:** To create a new database, type `use <database_name>`. This will create a new database if it doesn't already exist. If the database already exists, it will switch to that database.
- **Clearing screen:** Using `cls` will clear the screen. 
- **Showing current database:** To see the current database you are working on, type `db`. However it is also reflected in the shell prompt always.
- **Exiting:** Using `exit` will exit the mongo shell.
- **Collections:** Using `show collections` will show all the collections in the current database.

### What are collections and documents?
- **Collections:** A collection is a group of MongoDB documents. It is the equivalent of an RDBMS table. A collection exists within a single database. Collections do not enforce a schema. Documents within a collection can have different fields. Typically, all documents in a collection are of similar or related purpose.
- **Documents:** A document is a set of key-value pairs. Documents have dynamic schema. Dynamic schema means that documents in the same collection do not need to have the same set of fields or structure, and common fields in a collection's documents may hold different types of data.

### CRUD Operations
- **Create:** To insert a document into a collection, use the `insertOne()` method. For example, `db.collection_name.insertOne({field1: value1, field2: value2})`.
    - **Insert Many:** To insert multiple documents into a collection, use the `insertMany()` method. For example, `db.collection_name.insertMany([{field1: value1, field2: value2}, {field1: value3, field2: value4}])`.
- **Read:** To read documents from a collection, use the `find()` method. For example, `db.collection_name.find()`.
    - **Limit:** To limit the number of documents returned, use the `limit()` method. For example, `db.collection_name.find().limit(5)`.
    - **Sort:** To sort the documents returned, use the `sort()` method. For example, `db.collection_name.find().sort({field1: 1})` (ascending) or `db.collection_name.find().sort({field1: -1})` (descending).
- **Update:** To update a document in a collection, use the `updateOne()` method. For example, `db.collection_name.updateOne({field1: value1}, {$set: {field2: value2}})`.
- **Delete:**  To delete a document from a collection, use the `deleteOne()` method. For example, `db.collection_name.deleteOne({field1: value1})`.
+++
title = 'Mern tutorial'
date = 2024-03-29T16:36:16+05:30
tags = ["web", "mern", "nodejs", "react", "expressjs", "mongodb", "javascript", "fullstack"]
author = "Aum Pauskar"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "A quick tutorial on how to create a MERN stack application focued on a fullstack book library application."
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

# MERN Stack Tutorial

## 01-Running express js

### Preface
Express is a minimal and flexible Node.js web application framework that provides a robust set of features for web and mobile applications. It is an open-source framework developed and maintained by the Node.js foundation. It is designed for building web applications and APIs. It is the standard server framework for Node.js.

Before starting with express js, ensure that you have node.js, npm and a code editor installed on your system. The installation of node.js and npm can be verified by running the following commands in the terminal.
```bash
node -v
npm -v
```

In my environment I'm using node version `v20.11.1` and npm version `10.2.4` on a wsl environment.

You must also ensure that a `.gitignore` file is created in the root of the project directory. This file would contain the following lines:
```gitignore
node_modules/
```
This would prevent the `node_modules` directory from being pushed to the remote repository.

### Installing npm packages
To start a new project with express js, first create a new directory named `expressjs` and navigate to it. Run the following command within it.

```bash
npm init -y
```
This would create a `package.json` file with default values. Next, install the `express` and `nodemon` packages by running the following command.
```bash
npm i express nodemon
```
Here, `express` is the package that would be used to create the server and `nodemon` is a package that would be used to restart the server automatically when changes are made to the code.

### Changing the `package.json` file
A couple of changes would be made to the `package.json` file. The `type` field would be set to `module` and a new script would be added to the `scripts` field. The `scripts` field would look like this:
```json
"type": "module",
  "scripts": {
    "start": "node index.js",
    "dev": "nodemon index.js"
  },
```

### Coding 
Create a new file named `index.js` and add the following code to it.
```javascript
import express from "express";
import { PORT } from "./config.js";

const app = express();

app.listen(PORT, () => {
    console.log(`Server is running on port ${PORT}`);
});
```
The `PORT` variable is imported from a file named `config.js` which would be created next. The `config.js` file would look like this:
```javascript
export const PORT = 5000;
```
### Running the server
To start the server, run the following command in the terminal.
```bash
npm run dev
```
This would start the server on port `5000`. To verify that the server is running, open a web browser and navigate to `http://localhost:5000`. You should see a message that says `Cannot GET /`.

### Epilogue
If you want to follow this tutorial section by section please refer to the git commit history.

## 02-HTTP request

### HTTP request methods
- GET: Retrieve data from the server
- POST: Send data to the server
- PUT: Update data on the server
- DELETE: Remove data from the server
- PATCH: Update data partially on the server
- HEAD: Retrieve headers from the server
- OPTIONS: Retrieve supported methods from the server

### HTTP response code
- 200: OK
- 201: Created
- 204: No Content
- 400: Bad Request
- 401: Unauthorized
- 403: Forbidden
- 404: Not Found
- 405: Method Not Allowed
- 500: Internal Server Error
- 503: Service Unavailable

### Sending an HTTP request using express
Open the previously created `index.js` file and add the following code:

```javascript
app.get('/', (req, res) => {
    console.log(req);
    return res.status(234).send('Hello from server');
});
```

The total code will be as follows:

```javascript
import express from "express";
import { PORT } from "./config.js";

const app = express();

app.get('/', (req, res) => {
    console.log(req);
    return res.status(234).send('Hello from server');
});

app.listen(PORT, () => {
    console.log(`Server is running on port ${PORT}`);
});
```

In the above code, we have created a simple server that listens on port 3000 and sends a response with status code 234 and a message "Hello from server" when a request is made to the root URL.

Now to verify this you can run `npm run dev` and open the link given in the terminal. You will see the message "Hello from server" on the browser. To verify the status code, you can open the developer tools and check the network tab.

Another method to verify the status code is to use postman. You can install postman from [here](https://www.postman.com/downloads/). Postman is a tool that allows you to send HTTP requests and view the response. You can use postman to send a GET request to the server and check the status code and response. 

## 03=MongoDB

### Introduction
MongoDB is a NoSQL database that stores data in JSON-like documents. It is a popular choice for many modern web applications because it can handle large amounts of data and is scalable. There are two ways to access MongoDB. One way is to install the MongoDB server on your computer and use the command line interface to interact with it. The other way is to use a cloud-based service like MongoDB Atlas. Here we will focus on using MongoDB Atlas.

### Prerequisites
Before you start, you will need to have a MongoDB Atlas account. You can sign up for free at [https://www.mongodb.com/cloud/atlas](https://www.mongodb.com/cloud/atlas). Create a new account and proceed. Be sure to select the free tier option when creating your cluster if yo are planning to use it as a hobby project and don't wish to pay for the services.

### Setting up MongoDB Atlas
Create a strong password and store it in a safe place. You will need it to connect to your database and authenticate with **username** and **password**. Name the db cluster and click **finish**. This will take a couple of minutes to set up. Once it's done, click on the **connect** button. Click on **drivers** and select the latest version of **Node.js**. Copy the connection string and store it in `backend/config.js` file. **Note that we will store the password in this file itself so be sure to remove this file from the git repository and add it to the `.gitignore` file.**

### Connecting to MongoDB Atlas
Copy the connection string from the MongoDB Atlas dashboard and paste it in the `backend/config.js` file. Replace the password with the password you used to create the cluster. The connection string should look something like this:
```javascript
export const mongoDBURL = 'mongodb+srv://<username>:<password>@<cluster>.mongodb.net/<dbname>?retryWrites=true&w=majority'
```

### Connecting to MongoDB using Mongoose
Mongoose is an Object Data Modeling (ODM) library for MongoDB and Node.js. It manages relationships between data, provides schema validation, and is used to translate between objects in code and the representation of those objects in MongoDB. To connect to MongoDB using Mongoose, you will need to install the `mongoose` package. Run the following command in the terminal:
```bash
npm i mongoose
```
Now the `index.js` file in the `backend` directory should look something like this:
```javascript
import express from "express";
import { PORT, mongoDBURL } from "./config.js";
import mongoose from "mongoose";

const app = express();

app.get('/', (req, res) => {
    console.log(req);
    return res.status(234).send('Hello from server');
});

mongoose.connect(mongoDBURL).then(() => {
    console.log('Connected to MongoDB');
    app.listen(PORT, () => {
        console.log(`Server is running on port ${PORT}`);
    });
}).catch((err) => {
    console.log('Failed to connect to MongoDB', err);
});
```
Hwew we include the `mongoose` package and use the `connect` method to connect to the MongoDB database. If the connection is successful, we start the server. If the connection fails, we log the error to the console. Now you can run the server using the following command:
```bash
cd backend #if you are not already in the backend directory
npm run dev
```
If the connection is successful, you should see the following message in the terminal:
```
Connected to MongoDB
Server is running on port 5000
```

## 04-Book model

To create a new model, we need to create a new file in the `backend/models` directory. Let's create a new file called `bookModel.js` and add the following code:

```javascript
import mongoose from 'mongoose';

const bookSchema = mongoose.Schema(
    {
        title: {
            type: String,
            required: true,
        },
        author : {
            type: String,
            required: true,
        },
        publishYear: {
            type: Number,
            required: true,
        },
    },
    {
        timestamps: true,
    }
);
export const Book = mongoose.model('Book', bookSchema);
```

This code creates a new schema for the book model. The schema defines the structure of the document that will be stored in the database. The `title`, `author`, and `publishYear` fields are required and of type `String`, `String`, and `Number` respectively. The `timestamps` option creates two fields, `createdAt` and `updatedAt`, to store the creation and update times of the document. The `Book` model is created using the schema and exported.

## 05-Saving a book using Mongoose

To save a book to the database, we need to create a new route in index.js file in the `backend` directory. Let's create a new route called `/books` and add the following code:

```javascript
import express, { response } from "express";
import { PORT, mongoDBURL } from "./config.js";
import mongoose from "mongoose";
import { Book } from "./models/bookModel.js";

const app = express();
app.use(express.json());

app.get('/', (req, res) => {
    console.log(req);
    return res.status(234).send('Hello from server');
});

app.post('/books', async (req, res) => {
    try {
        if (
            !req.body.title ||
            !req.body.author ||
            !req.body.publishYear
        ) {
            return res.status(400).send({
                message: 'Please fill all required fields'
            });
        }
        const newBook = {
            title: req.body.title,
            author: req.body.author,
            publishYear: req.body.publishYear,
        };
        const book = await Book.create(newBook);
        // Send a response back to the client
        return res.status(201).send(book);
    } catch (error) {
        console.log(error.message);
        res.status(500).send({ message: error.message});
    }
});


mongoose.connect(mongoDBURL).then(() => {
    console.log('Connected to MongoDB');
    app.listen(PORT, () => {
        console.log(`Server is running on port ${PORT}`);
    });
}).catch((err) => {
    console.log('Failed to connect to MongoDB', err);
});
```
Here we have added a new route `/books` that listens for POST requests. When a POST request is received, we check if the required fields are present in the request body. If they are, we create a new book using the `Book` model and send a response back to the client. If the required fields are not present, we send a 400 status code with a message asking the client to fill all required fields. If an error occurs, we log the error to the console and send a 500 status code with the error message to the client.

Note that we have added `app.use(express.json());` to parse the request body as JSON. This is required to access the request body in the POST request.

Now you can run the server using the following command:
```bash
cd backend #if you are not already in the backend directory
npm run dev
```

This code cannot be tested via the browser and should be tested via a REST client like [Postman](https://www.postman.com/). You can use the following code to test the route:
**Postman set up** 
URL: `http://localhost:5000/books`\
Method: `POST`\
Body: `raw`\
Headers: `Content-Type: application/json`\

```json
{
    "title": "name",
    "author": "authname",
    "publishYear": 2077
}
```

If the request is successful, you should see the following message in the terminal:
```
Connected to MongoDB
Server is running on port 5000
```

And this output in the postman shell (might differ in your case):
```json
{
    "title": "name",
    "author": "authname",
    "publishYear": 2077,
    "_id": "60f3e3e3e3e3e3e3e3e3e3e3",
    "createdAt": "2021-07-18T14:00:00.000Z",
    "updatedAt": "2021-07-18T14:00:00.000Z",
    "__v": 0
}
```

## 06-Getting books from the database 

In the previous module we have used the **post** method to add books to the database. In this module we will use the **get** method to retrieve books from the database. In order to d othis we can create a new `get` route for the `/books` endpoint. 

```javascript
app.get('/books', async (req, res) => {
    try {
        const books = await Book.find({});
        return res.status(200).send(books);
    } catch (error) {
        console.log(error.message);
        res.status(500).send({ message: error.message});
    }
});
```

This method can further be modified for a more detailed search by modifying the json output. 

```javascript
app.get('/books', async (req, res) => {
    try {
        const books = await Book.find({});
        return res.status(200).json({ 
            count: books.length,
            data: books
        });
    } catch (error) {
        console.log(error.message);
        res.status(500).send({ message: error.message});
    }
});
```

Similarly to the previous module the endpoints are to be tested using Postman. But instead of using the **post** method, we will use the **get** method.

The final output (from postman) should look like this:

```json
{
    "count": 1,
    "data": [
        {
            "_id": "65ef564e810c88d123eea864",
            "title": "name",
            "author": "authname",
            "publishYear": 2077,
            "createdAt": "2024-03-11T19:06:55.000Z",
            "updatedAt": "2024-03-11T19:06:55.000Z",
            "__v": 0
        }
    ]
}
```

## 07-Getting books by id

What if we want to retrieve a specific book from the database? We can do this by creating a new `get` route for the `/books/:id` endpoint. 

```javascript
app.get('/books/:id', async (req, res) => {
    try {
        const { id } = req.params;
        const book = await Book.findById(id);
        return res.status(200).json(book);
    } catch (error) {
        console.log(error.message);
        res.status(500).send({ message: error.message});
    }
});
```
Here the `:id` is a route parameter which is used to retrieve the book with the given id, this id is then used to query the database and retrieve the book.

In my case the id was `65ef564e810c88d123eea864`. So the argument in postman must be using the **get** method and the url must be `http://localhost:3000/books/65ef564e810c88d123eea864`. The final output (from postman) should look like this:

```json
{
    "_id": "65ef564e810c88d123eea864",
    "title": "name",
    "author": "authname",
    "publishYear": 2077,
    "createdAt": "2024-03-11T19:06:55.000Z",
    "updatedAt": "2024-03-11T19:06:55.000Z",
    "__v": 0
}
```

## 08-Updating books

### Use of the `put` method
The `put` method is used to update a book in the database. In order to do this we can create a new `put` route for the `/books/:id` endpoint. 

```javascript
app.put('/books/:id', async (req, res) => {
    try {
        if (
            !req.body.title ||
            !req.body.author ||
            !req.body.publishYear
        ) {
            
            return res.status(400).send({
                message: "Please fill all required fields",    
            });
        }
        const { id } = req.params;
        const result = await Book.findByIdAndUpdate(id, req.body);

        if (!result) {
            return res.status(404).send({ message: "Book not found" });
        }

        return res.status(200).send({ message: "Book updated successfully" });
    } catch (error) {
            console.log(error.message);
            res.status(500).send({ message: error.message});
        }
});
```

This is a route handler for a PUT request in an Express.js application. It's designed to update a book record in a database. Here's a step-by-step explanation:

1. `app.put('/books/:id', async (req, res) => {...}`: This line sets up a route for PUT requests to '/books/:id'. The ':id' is a route parameter that will be replaced with the ID of the book to update.

2. Inside the route handler, it first checks if the required fields (`title`, `author`, `publishYear`) are provided in the request body. If not, it sends a 400 status code (Bad Request) with a message.

3. `const { id } = req.params;`: This line extracts the 'id' from the request parameters.

4. `const result = await Book.findByIdAndUpdate(id, req.body);`: This line uses the `findByIdAndUpdate` method of the `Book` model to update the book with the given ID. It uses the data from the request body to update the book.

5. If the `findByIdAndUpdate` method does not find a book with the given ID, it returns `null`. The code checks for this and, if the book is not found, sends a 404 status code (Not Found) with a message.

6. If the book is found and updated, it sends a 200 status code (OK) with a success message.

7. If any error occurs during this process, it's caught in the `catch` block, logged to the console, and a 500 status code (Internal Server Error) is sent with the error message.

Similar to the previous modules, the endpoints are to be tested using Postman. But instead of using the `post` method, we will use the `put` method.

Use the following postman settings
- Method: `put`
- URL: `http://localhost:3000/books/<bookid>`
- Body: 
    ```json
    {
        "title": "new title",
        "author": "new author",
        "publishYear": 2023
    }
    ```
The final output (from postman) should look like this:

```json
{
    "message": "Book updated successfully"
}
```

This can be verified by using the `get` method and the url must be `http://localhost:5000/books/<bookid>`. The final output (from postman) should look like this:

```json
{
    "_id": "65ef564e810c88d123eea864",
    "title": "newname",
    "author": "newauthname",
    "publishYear": 2023,
    "createdAt": "2024-03-11T19:06:55.000Z",
    "updatedAt": "2024-03-14T06:46:16.522Z",
    "__v": 0
}
```

## 09-Deleting books from the database

In the previous modules, we have used the `post` method to add books to the database, the `get` method to retrieve books from the database, and the `put` method to update books in the database. In this module, we will use the `delete` method to remove books from the database.

This is the following route to handle the `delete` method:

```javascript
app.delete('/books/:id', async (req, res) => {
    try {
        const { id } = req.params;
        const result = await Book.findByIdAndDelete(id);
        if (!result) {
            return res.status(404).send({ message: "Book not found" });
        }
        return res.status(200).send({ message: "Book deleted successfully" });
    } catch (error) {
        console.log(error.message);
        res.status(500).send({ message: error.message});
    }
});
```

The code is self-explanatory. It first checks if the book with the given ID exists in the database. If it does, it deletes the book and sends a 200 status code (OK) with a success message. If the book is not found, it sends a 404 status code (Not Found) with a message. If any error occurs during this process, it's caught in the `catch` block, logged to the console, and a 500 status code (Internal Server Error) is sent with the error message.

Similar to the previous modules, the endpoints are to be tested using Postman. But instead of using the `post` method, we will use the `delete` method.

First we shall add a new book to the database using the `post` method. Then we will use the `get` method to retrieve the book's id. Finally, we will use the `delete` method to remove the book from the database.

**Adding a new book**
- Method: `post`
- URL: `http://localhost:5000/books`
- Body: 
    ```json
    {
        "title": "deletethisbook",
        "author": "deletethisauthor",
        "publishYear": 2008
    }
    ```

**Retrieving the book's id**
- Method: `get`
- URL: `http://localhost:5000/books`
- The final output (from postman) should look like this:
    ```json
    {
        "count": 2,
        "data": [
            {
                "_id": "65ef564e810c88d123eea864",
                "title": "newname",
                "author": "newauthname",
                "publishYear": 2023,
                "createdAt": "2024-03-11T19:06:55.000Z",
                "updatedAt": "2024-03-14T06:46:16.522Z",
                "__v": 0
            },
            {
                "_id": "65f2a166b3f07128b54a362f",
                "title": "deletethisbook",
                "author": "deletethisauthor",
                "publishYear": 2008,
                "createdAt": "2024-03-14T07:04:06.831Z",
                "updatedAt": "2024-03-14T07:04:06.831Z",
                "__v": 0
            }
        ]
    }
    ```
    Here the second book has the id `65f2a166b3f07128b54a362f` and this is the id we will use to delete the book.

**Deleting the book**
- Method: `delete`
- URL: `http://localhost:5000/books/65f2a166b3f07128b54a362f`
- The final output (from postman) should look like this:
    ```json
    {
        "message": "Book deleted successfully"
    }
    ```

This can be verified by using the `get` method and the url must be `http://localhost:5000/books`. The final output (from postman) should look like this:
```json
{
    "count": 1,
    "data": [
        {
            "_id": "65ef564e810c88d123eea864",
            "title": "newname",
            "author": "newauthname",
            "publishYear": 2023,
            "createdAt": "2024-03-11T19:06:55.000Z",
            "updatedAt": "2024-03-14T06:46:16.522Z",
            "__v": 0
        }
    ]
}
```

## 10-Express router

Having all the routes in the same file can be a bit messy, it makes the code readability harder and debugging a bit more difficult. To solve this problem, Express provides a way to separate the routes into different files using the `express.Router` class.

In order to do this we can create a new file called `/routes/bookRoutes.js` and move the routes from `app.js` to this new file.

```javascript
import express from 'express';
import { Book } from '../models/bookModel.js';

const router = express.Router();

router.post('/', async (req, res) => {
    try {
        if (
            !req.body.title ||
            !req.body.author ||
            !req.body.publishYear
        ) {
            return res.status(400).send({
                message: 'Please fill all required fields'
            });
        }
        const newBook = {
            title: req.body.title,
            author: req.body.author,
            publishYear: req.body.publishYear,
        };
        const book = await Book.create(newBook);
        // Send a response back to the client
        return res.status(201).send(book);
    } catch (error) {
        console.log(error.message);
        res.status(500).send({ message: error.message});
    }
});

router.get('/', async (req, res) => {
    try {
        const books = await Book.find({});
        return res.status(200).json({ 
            count: books.length,
            data: books
        });
    } catch (error) {
        console.log(error.message);
        res.status(500).send({ message: error.message});
    }
});

router.get('/:id', async (req, res) => {
    try {
        const { id } = req.params;
        const book = await Book.findById(id);
        return res.status(200).json(book);
    } catch (error) {
        console.log(error.message);
        res.status(500).send({ message: error.message});
    }
});

router.put('/:id', async (req, res) => {
    try {
        if (
            !req.body.title ||
            !req.body.author ||
            !req.body.publishYear
        ) {
            
            return res.status(400).send({
                message: "Please fill all required fields",    
            });
        }
        const { id } = req.params;
        const result = await Book.findByIdAndUpdate(id, req.body);

        if (!result) {
            return res.status(404).send({ message: "Book not found" });
        }

        return res.status(200).send({ message: "Book updated successfully" });
    } catch (error) {
            console.log(error.message);
            res.status(500).send({ message: error.message});
        }
});

router.delete('/:id', async (req, res) => {
    try {
        const { id } = req.params;
        const result = await Book.findByIdAndDelete(id);
        if (!result) {
            return res.status(404).send({ message: "Book not found" });
        }
        return res.status(200).send({ message: "Book deleted successfully" });
    } catch (error) {
        console.log(error.message);
        res.status(500).send({ message: error.message});
    }
});

export default router;
```

**For reference** the structure of the `index.js` file should look like this **BEFORE** the refactoring:

```javascript
import express, { response } from "express";
import { PORT, mongoDBURL } from "./config.js";
import mongoose from "mongoose";
import { Book } from "./models/bookModel.js";

const app = express();
app.use(express.json());

app.get('/', (req, res) => {
    console.log(req);
    return res.status(234).send('Hello from server');
});

app.post('/books', async (req, res) => {
    try {
        if (
            !req.body.title ||
            !req.body.author ||
            !req.body.publishYear
        ) {
            return res.status(400).send({
                message: 'Please fill all required fields'
            });
        }
        const newBook = {
            title: req.body.title,
            author: req.body.author,
            publishYear: req.body.publishYear,
        };
        const book = await Book.create(newBook);
        // Send a response back to the client
        return res.status(201).send(book);
    } catch (error) {
        console.log(error.message);
        res.status(500).send({ message: error.message});
    }
});

app.get('/books', async (req, res) => {
    try {
        const books = await Book.find({});
        return res.status(200).json({ 
            count: books.length,
            data: books
        });
    } catch (error) {
        console.log(error.message);
        res.status(500).send({ message: error.message});
    }
});

app.get('/books/:id', async (req, res) => {
    try {
        const { id } = req.params;
        const book = await Book.findById(id);
        return res.status(200).json(book);
    } catch (error) {
        console.log(error.message);
        res.status(500).send({ message: error.message});
    }
});

app.put('/books/:id', async (req, res) => {
    try {
        if (
            !req.body.title ||
            !req.body.author ||
            !req.body.publishYear
        ) {
            
            return res.status(400).send({
                message: "Please fill all required fields",    
            });
        }
        const { id } = req.params;
        const result = await Book.findByIdAndUpdate(id, req.body);

        if (!result) {
            return res.status(404).send({ message: "Book not found" });
        }

        return res.status(200).send({ message: "Book updated successfully" });
    } catch (error) {
            console.log(error.message);
            res.status(500).send({ message: error.message});
        }
});

app.delete('/books/:id', async (req, res) => {
    try {
        const { id } = req.params;
        const result = await Book.findByIdAndDelete(id);
        if (!result) {
            return res.status(404).send({ message: "Book not found" });
        }
        return res.status(200).send({ message: "Book deleted successfully" });
    } catch (error) {
        console.log(error.message);
        res.status(500).send({ message: error.message});
    }
});

mongoose.connect(mongoDBURL).then(() => {
    console.log('Connected to MongoDB');
    app.listen(PORT, () => {
        console.log(`Server is running on port ${PORT}`);
    });
}).catch((err) => {
    console.log('Failed to connect to MongoDB', err);
});
```

And here is the code after refactoring:

```javascript
import express, { response } from "express";
import { PORT, mongoDBURL } from "./config.js";
import mongoose from "mongoose";
import booksRouter from "./routes/bookRoutes.js";

const app = express();
app.use(express.json());

app.get('/', (req, res) => {
    console.log(req);
    return res.status(234).send('Hello from server');
});

app.use('/books', booksRouter);

mongoose.connect(mongoDBURL).then(() => {
    console.log('Connected to MongoDB');
    app.listen(PORT, () => {
        console.log(`Server is running on port ${PORT}`);
    });
}).catch((err) => {
    console.log('Failed to connect to MongoDB', err);
});
```

Note the changes we have done to the `index.js` file: \
We have removed all the `/books` routes from the `index.js` file and replaced them with `app.use('/books', booksRouter);`. This line tells Express to use the `booksRouter` for all the routes that start with `/books`.

And the `bookRoutes.js` file is a new file that we have created to hold all the `/books` routes. We have moved all the `/books` routes from the `index.js` file to this new file. We have renamed the `app` object to `router` and we have exported it at the end of the file and refactored the routes to start with `/` instead of `/books`. This is because we have included this line `app.use('/books', booksRouter);` in the `index.js` file, so all the routes in the `bookRoutes.js` file will be prefixed with `/books`.

## 11-CORS policy

### What is CORS?
CORS stands for Cross-Origin Resource Sharing. It is a security feature implemented in web browsers to prevent unauthorized access to resources on a different origin. An origin is defined as the combination of protocol, domain, and port. For example, the origin of `https://example.com:8080` is `https://example.com:8080`. It is a safety measure to prevent unauthorized access to resources on a different origin. However, there are times when you want to allow access to resources from a different origin. This is where CORS comes in.

### Including CORS in your Express app
To use CORS in your Express app, you need to install the `cors` package. You can do this by running the following command in your terminal:

```bash
npm i cors
```

After installing the `cors` package, you can include it in your Express app by adding the following line of code to your `index.js` file:

```javascript
import cors from "cors";
```

Then, you can use the `cors` middleware in your app by adding the following line of code to your `index.js` file. This can be done in 2 ways:
- Allow all origins
- Allow specific origins

```javascript
// Allow all origins
app.use(cors());
// Allow specific origins
app.use(cors({
    origin: 'http://localhost:5000',
    methods: 'GET, POST, PUT, DELETE',
    allowedHeaders: 'Content-Type'
}));
```

Note that only one of the above lines should be used in your `index.js` file. The first line allows all origins, while the second line allows only the specified origin. You can also specify the methods and headers that are allowed.

## 12-React setup

### What is React?
React is a JavaScript library for building user interfaces. It is maintained by Facebook and a community of individual developers and companies. React can be used as a base in the development of single-page or mobile applications.

### How to install React
There are two (main) ways to install React:
- Using `create-react-app`: **Advantages**: It is the easiest way to get started with React. **Disadvantages**: It is not as flexible as setting up React from scratch.
- Using `vite`: **Advantages**: It is faster than `create-react-app`. **Disadvantages**: It is not as beginner-friendly as `create-react-app`.

We shall use vite to set up our React app. To create a vite app, run the following command in the **root directory** of your terminal:


```bash
npm create vite@latest
```
If vite is not installed, a prompt will appear asking you to install it. Press `y` and hit `Enter` to install vite. After installing vite, you will be prompted to enter the name of your project. Enter the name of your project and hit `Enter`. Vite will now ask the framework you want to use. Select `react` and hit `Enter`. It will now ask if you want to use TypeScript or JavaScript. We shall use JavaScript, so hit `Enter`. Vite will now create a new directory with the name of your project and set up a new React app for you.

Now go into the directory of your project by running the following command in your terminal:

```bash
cd <project-name>
npm i
```

### Using Tailwind
Tailwind CSS is a utility-first CSS framework for rapidly building custom designs. It is a low-level framework that provides you with all the building blocks you need to build your own designs. To use Tailwind in your React app, you need to install the `tailwindcss` package. You can do this by running the following command in your terminal. But first visit the [Tailwind website](https://tailwindcss.com/) or dirctly visit the [quickstart guide for vite](https://tailwindcss.com/docs/guides/vite).

Installation
```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

After installing the `tailwindcss` package, you can replace it in your React app by adding the following line of code to your `tailwind.config.js` file:

```css
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

Now you can replace the code of `index.css` with the following code:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Delete `App.css` for now

In the `App.jsx` file, replace the code with the following:

```jsx
import React from 'react'

const App = () => {
  return (
    <div className='bg-red-400 text-white'>
      App
    </div>
  )
}

export default App
```
To make development easier, you use the ES7 React/Redux/GraphQL/React-Native snippets extension in VSCode. This extension provides you with a lot of snippets that you can use to write your code faster. Using `rafce` snippet will create a functional component with an export statement.

To run this code in your browser, run the following command in your terminal:

```bash
npm run dev
```
Unlike the modules before you have to run the command in the `frontend` directory. This will start a development server and open your app in your default browser. The output will look like this:
![basic react app](https://github.com/AumPauskar/MERN-trial/blob/main/docs/assets/react-basic.png)

## 13-React router dom

The react router dom is a package that allows you to use the routing in your react application. It is a collection of navigational components that compose declaratively with your application.

### Installation
```bash
npm i react-router-dom
```

### Usage

Go to the `main.jsx` file and import the `BrowserRouter` and `Route` components from the `react-router-dom` package.

```jsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.jsx'
import './index.css'
import { BrowserRouter } from 'react-router-dom'

ReactDOM.createRoot(document.getElementById('root')).render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
)
```

You have to create a new folder within the `src` folder called `page`. This folder will contain the components that will be used in the routes. Create 5 different files within the `page` folder.
- `Home.jsx`
    ```jsx
    import React from 'react'

    function Home() {
    return (
        <div>
        
        </div>
    )
    }

    export default Home
    ```
- `ShowBook.jsx`
    ```jsx
    import React from 'react'

    function ShowBook() {
    return (
        <div>
        
        </div>
    )
    }

    export default ShowBook
    ```
- `EditBook.jsx`
    ```jsx
    import React from 'react'

    function EditBook() {
    return (
        <div>
        
        </div>
    )
    }

    export default EditBook
    ```
- `CreateBook.jsx`
    ```jsx
    import React from 'react'

    function CreateBook() {
    return (
        <div>
        
        </div>
    )
    }

    export default CreateBook
    ```
- `DeleteBook.jsx`
    ```jsx
    import React from 'react'

    function DeleteBook() {
    return (
        <div>
        
        </div>
    )
    }

    export default DeleteBook
    ```


Now you have to modify the `App.jsx` file to use the `Route` component.

```jsx
import React from 'react'
import { Routes, Route } from 'react-router-dom'
import Home from './page/Home'
import ShowBook from './page/ShowBook'
import EditBook from './page/EditBook'
import NewBook from './page/NewBook'
import CreateBook from './page/CreateBook'
import DeleteBook from './page/DeleteBook'

const App = () => {
  return (
    <Routes>
      <Route path='/' element={ <Home /> } />
      <Route path='/books/create' element={ <CreateBook /> } />
      <Route path='/books/details/:id' element={ <ShowBook /> } />
      <Route path='/books/edit/:id' element={ <EditBook /> } />
      <Route path='/books/delete/:id' element={ <DeleteBook /> } />
    </Routes>
  )
}

export default App
```

## 14-Showing books in react

In this part we need both the frontend and the backend of the project and we will be using the backend from the previous part.

### Packages needed

First cd into the frontend folder and run the following command to install the packages needed.

```bash
cd frontend
npm install axios react-icons
```
Axios is a promise based HTTP client for the browser and node.js and react-icons is a library that provides popular icons for your react project.

### Tweaking the backend
Open the `/backend/index.js` and do the following changes.

```javascript
app.use(cors());
// app.use(cors({
//     origin: 'http://localhost:5000',
//     methods: 'GET, POST, PUT, DELETE',
//     allowedHeaders: 'Content-Type'
// }));
```
We are commenting out the cors options because we are not going to use it in this part.

### Creating react components for loading state
Create a folder in `frontend/src` called `components` and create a file called `Spinner.jsx` and add the following code.

```jsx
import React from 'react'

function Spinner() {
  return (
    <div className='animate-ping w-16 h-16 m-8 rounded-full bg-sky-600'></div>
  )
}

export default Spinner
```

This is a simple spinner component that we will use to show the user that the books are being loaded.

### Now we have to create a component to show the books

Modifying `frontend/src/page/Home.jsx` to show the books.

```jsx
import React from 'react'
import { useState, useEffect } from 'react'
import axios from 'axios'
import Spinner from '../components/Spinner'
import { AiOutlineEdit } from 'react-icons/ai'
import { BsInfoCircle } from 'react-icons/bs'
import { MdOutlineAddBox, MdOutlineDelete } from 'react-icons/md'
import { Link } from 'react-router-dom';

function Home() {
  const [books, setBooks] = useState([]);
  const [loading, setLoading] = useState(false);
  useEffect(() => {
    setLoading(true);
    axios.get('http://localhost:5000/books').then((response) => {
      setBooks(response.data.data);
      setLoading(false);
  }).catch((error) => {
      console.log(error);
      setLoading(false);
  });
  }, []);
  return (
    <div className='p-4'>
      <div className='flex justify-between items-center'>
        <h1 className='text-3xl my-8'>Book list</h1>
        <Link to ='/books/create'>
          <MdOutlineAddBox className='text-sky-800 text-4xl' />
        </Link>
      </div>
      {loading ? (
      <Spinner />
      ) : (
        <table className='w-full border-separate border-spacing-2' >
          <thead>
            <tr>
              <th className='border border-slate-600 rounded-md'>No</th>
              <th className='border border-slate-600 rounded-md'>Title</th>
              <th className='border border-slate-600 rounded-md max-md:hidden'>Author</th>
              <th className='border border-slate-600 rounded-md'>Publish Year</th>
              <th className='border border-slate-600 rounded-md max-md:hidden'>Operations</th>
            </tr>
          </thead>
          <tbody>
            {books.map((book, index) => (
              <tr key={book._id} className='h-8'>
                <td className='border border-slate-700 rounded-md text-center'>
                  {index + 1}
                </td>
                <td className='border border-slate-700 rounded-md text-center'>
                  {book.title}
                </td>
                <td className='border border-slate-700 rounded-md text-center'>
                  {book.author}
                </td>
                <td className='border border-slate-700 rounded-md text-center'>
                  {book.publishYear}
                </td>
                <td className='border border-slate-700 rounded-md text-center'>
                  <div className='flex justify-center gap-x-4'>
                    <Link to={`/books/details/${book._id}`}>
                      <BsInfoCircle className='text-sky-800 text-2xl' />
                    </Link>
                    <Link to={`/books/edit/${book._id}`}>
                      <AiOutlineEdit className='text-sky-800 text-2xl' />
                    </Link>
                    <Link to={`/books/delete/${book._id}`}>
                      <MdOutlineDelete className='text-sky-800 text-2xl' />
                    </Link>
                  </div>
                </td>
              </tr>
              ))}
          </tbody>
        </table>
      )}
    </div>
  )
}

export default Home
```

Explanation of the code:
This is a React component named `Home` that fetches and displays a list of books from a backend server. Here's a breakdown of what each part of the code does:

1. **Imports**: The necessary modules and components are imported. This includes React itself, the `useState` and `useEffect` hooks from React, the `axios` library for making HTTP requests, a `Spinner` component (presumably a loading spinner), several icons from `react-icons`, and the `Link` component from `react-router-dom`.

2. **State Variables**: Two state variables are declared using the `useState` hook: `books` (an array to store the list of books) and `loading` (a boolean to track whether the data is currently being fetched).

3. **Data Fetching**: The `useEffect` hook is used to fetch the list of books from the backend server when the component is first rendered. The `axios.get` function is used to make a GET request to the server. If the request is successful, the response data is stored in the `books` state variable and `loading` is set to `false`. If an error occurs, it's logged to the console and `loading` is also set to `false`.

4. **Rendering**: The component returns a JSX element that displays a list of books. If the data is still being fetched (`loading` is `true`), a `Spinner` component is displayed. Otherwise, a table is displayed with each book's details. Each book has links to its detail, edit, and delete pages, which are created using the `Link` component from `react-router-dom`.

5. **Export**: Finally, the `Home` component is exported for use in other parts of the application.

Modifying `frontend/src/App.js` to show the `Home` component.

```jsx
import React from 'react'
import { Routes, Route } from 'react-router-dom'
import Home from './page/Home'
import ShowBook from './page/ShowBook'
import EditBook from './page/EditBook'
// import NewBook from './page/NewBook'
import CreateBook from './page/CreateBook'
import DeleteBook from './page/DeleteBook'

const App = () => {
  return (
    <Routes>
      <Route path='/' element={ <Home /> } />
      <Route path='/books/create' element={ <CreateBook /> } />
      <Route path='/books/details/:id' element={ <ShowBook /> } />
      <Route path='/books/edit/:id' element={ <EditBook /> } />
      <Route path='/books/delete/:id' element={ <DeleteBook /> } />
    </Routes>
  )
}

export default App
```

### Running the code
To run this code two instances of the terminal must be made. One for the backend and the other for the frontend. In the backend terminal run the following command.

```bash
cd backend/
npm run dev
```

In the frontend terminal run the following command.

```bash
cd frontend/
npm run dev
```

Open the link provided by the frontend page and you will see the books being displayed.

**Preview of the page:**
![React book list](https://github.com/AumPauskar/MERN-trial/blob/main/docs/assets/react-book-list.png)

## References
- [freecodecamp.org](https://youtu.be/-42K44A1oMA?si=E38KksJu-mndwl-m)
- [My github repo](https://github.com/AumPauskar/MERN-trial) derived from the above link
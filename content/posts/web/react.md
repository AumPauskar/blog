+++
title = 'Building websites with React'
date = 2023-12-15T09:20:47+05:30
draft = false
tags = ["react", "web", "javascript", "frontend", "webdev", "programming", "html", "css", "node", "npm"]
author = "Aum Pauskar"
description = "A comprehensive guide to building websites with React"
+++

# React tutorial

## About the tutorial
This short note is based and created assuming you are using a Linux (debian/ubuntu) system, most of the commands will run on other systems like Windows and Mac as well but may require some changes. In case you need to follow along and using a Windows system, you can use the [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10) to run the commands.

## Installing react
In order to install react, node and npm are required. To install node and npm, run the following command:
```bash
sudo apt update
sudo apt install nodejs npm -y
```

**Note:** The above command may install a deprecated version of node and npm. To install the latest version of node and npm, run the following commands:
```bash
sudo apt update
sudo apt install curl
# replace .../setup_14.x with the latest version
# for example, if the latest version is 16.x, replace .../setup_20.x with .../setup_20.x
curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
sudo apt update
sudo apt install nodejs -y
```

To verify the installation run the following commands
```bash
node --version
npm --version
```
If installed sucessfully you should see the version of node and npm installed.
```
$ node -v
v20.5.1
$ npm -v
9.8.0
```
In order to install react, run the following command:
```bash
sudo npm -g install create-react-app
```
To verify the installation run the following command
```bash
create-react-app --version
```

## Creating and running a react app
To create a react app, run the following command:
```bash
npx create-react-app my-react-app
```
This will create a react app named `my-react-app` in the current directory. To run the app, run the following commands:
```bash
cd my-react-app
npm start
```

This will start the react app and open it in the default browser. If it doesn't open automatically, you can just click on the terminal link to open it in the browser.

## File structure
Since we are using create-react-app, the file structure is already created for us.
```bash
README.md  node_modules/  package-lock.json  package.json  public/  src/
```
`node_modules/` conttains all the dependencies of the project. `package.json` contains the information about the project and the dependencies. `src/` contains the source code of the project. `public` contains the static files of the project. \
If we just `cd` into the `src/` directory, we can see the following files:
```bash
App.css  App.js  App.test.js  index.css  index.js  logo.svg  reportWebVitals.js  setupTests.js
```

## Why to use react?
React is a JavaScript library for building user interfaces. With the standard HTML, CSS and JavaScript the browser engine creates a DOM (Document Object Model), which is a tree of objects. However with the complezity of applications increasing, the DOM becomes more and more complex. Here react comes into play, wherein all are arranged into components and it also creates something called as a virtual DOM, which is a copy of the actual DOM. 


## Standard practices in react
- Components should be named with PascalCase
- All the react components must be in the `components/` directory. **Source:** `/src/components`

### More about components
- A component can be created using a function or a class. However using a function is more common. A component can be created using the following syntax:
  ```js
  function MyComponent() {
    return (
      <div>
        <h1>My component</h1>
      </div>
    );
  }
  ```
- A component can be dynamically rendered using the following syntax:
  ```js
  function MyComponent() {
    const myVar = true;
    return (
      <div>
        {myVar && <h1>My component</h1>}
      </div>
    );
  }
  ```
- A jsx or tsx function can **only return one component**. If more are required, they must be wrapped in a div or a fragment. A fragment can be created using the following syntax:
  ```js
  function MyComponent() {
    return ( 
      <div>
          <h1>My component</h1>
          <h2>My component</h2>
      </div>
      // here div acts as a wrapper  
    );
  }
  ```


## Creating a basic hello world app
Create a file named `Message.js` in the `src/` directory and add the following code:
```js
function Message() {
  return <h1>Hello world</h1>;
}

export default Message;
```
Now in the `App.js` file, add the following code:
```js
import Message from "./Message";

function App() {
  return (
    <div>
      <Message></Message>
    </div>
  );
}

export default App;
```
Now to run the app use
```bash
npm start
```

**About react and JSX:** React uses JSX, which is a syntax extension to JavaScript. Both JSX and TypeScript can be used in React but using JSX is more common. 

- Dynamic content
  `Message.js` can be updated to the following to display dynamic content:
  ```js
  function Message() {
    const myMessage = 'Bruh world';
    return <h1>Hello world {myMessage}</h1>;
  }

  export default Message;
  ```

- Adding a button to the app
```js
import Message from "./Message";

function MyButton() {
  return (
    <button>
      I'm a button
    </button>
  );
}

function App() {
  return (
    <div>
      <Message></Message>
      <MyButton />
    </div>
    
  );
}

export default App;
```

## Using bootstrap
Bootstrap is a CSS framework that makes it easy to create responsive websites. To install bootstrap, run the following command

```bash
npm i bootstrap@version
```
example
```bash
npm i bootstrap@5.2.3
```

After installing bootstrap npm will automatically include it in the `package.json` file. To use bootstrap, add the following line to the `App.js` file.

contents of `App.js`
```js
import Message from "./Message";
import ListGroup from "./ListGroup";

function MyButton() {
  return (
    <button>
      I'm a button
    </button>
  );
}

function App() {
  return (
    <div>
      <Message></Message>
      <MyButton />
      <ListGroup />
    </div>
    

  );
}

export default App;
```
since we are using react its better to make a seperate file for each component. So create a file named `ListGroup.js` in the `src/` directory and add the following code:
```js
function ListGroup() {
	return 	<ul className="list-group">
	<li className="list-group-item">An item</li>
	<li className="list-group-item">A second item</li>
	<li className="list-group-item">A third item</li>
	<li className="list-group-item">A fourth item</li>
	<li className="list-group-item">And a fifth one</li>
	</ul>;
}

export default ListGroup;
```
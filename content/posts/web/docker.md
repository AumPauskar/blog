+++
title = 'Docker'
date = 2024-03-31T21:32:54+05:30
tags = ["docker", "os", "web", "devops", "kubernates", "linux", "container", "nodejs", "expressjs", "mern", "fullstack"]
author = "Aum Pauskar"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "A brief introduction to docker and its installation."
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

# Docker

## What is docker
Docker is a platform for developers and sysadmins to develop, deploy, and run applications with containers. The use of Linux containers to deploy applications is called containerization. Containers are not new, but their use for easily deploying applications is.

## Why docker
- **Consistency**: Docker provides a consistent environment for your application from development all the way through production.
- **Isolation**: Docker containers are completely isolated. This means that your application will run the same way no matter where it is deployed.
- **Portability**: Docker containers can run on your local development machine, on the cloud, or on-premises.
- **Resource Efficiency**: Docker containers share the same OS kernel and are lighter weight than VMs.
- **Productivity**: Docker makes it easy to install and run software without worrying about setup or dependencies.

## Installation of docker
I'll be using Windows 11 for the installation of docker. You can find the installation steps for other operating systems [here](https://docs.docker.com/get-docker/).

- Download [Docker Desktop](https://www.docker.com/products/docker-desktop/) for Windows.
- Double-click on the installer and follow the installation steps.
- Once the installation is complete, you can find the Docker Desktop icon in the system tray.
- Restart your system to ensure it is working alongside windows terminal.

## Docker commands
- `docker --version`: Check the version of docker installed.
- `docker run hello-world`: Run a simple hello-world container.
- `docker ps`: List all running containers.
- `docker ps -a`: List all containers.
- `docker images`: List all images.
- `docker pull <image-name>`: Pull an image from the docker hub.
- `docker build -t <image-name> .`: Build an image from a Dockerfile.
- `docker exec -it <container-id> bash`: Run a bash shell inside a container.
- `docker stop <container-id>`: Stop a running container.
- `docker rm <container-id>`: Remove a container.
- `docker rmi <image-id>`: Remove an image.
- `docker-compose up`: Start the services defined in a docker-compose file.
- `docker-compose down`: Stop the services defined in a docker-compose file.
- `dokcer run -p <host-port>:<container-port> <image-name>`: Run a container and map the host port to the container port.

## Dockerfile
A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image. Using `docker build` users can create an automated build that executes several command-line instructions in succession. To ensure all the dependencies are running open the docker desktop or ensure that the docker service is running.


## Code that I am using to demonstrate docker

### Flask Application

- Directory Structure
```
└───flask-app
    │   app.py
    │   Dockerfile
    │
    └───__pycache__
            app.cpython-312.pyc
```

- app.py
```python
import flask
import fcntl

app = flask.Flask(__name__)

@app.route('/')
def index():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run(debug=True)
```

- Dockerfile
```Dockerfile
FROM ubuntu:22.04

# Install necessary dependencies
RUN apt-get update && apt-get install -y python3 python3-pip

# Set the working directory
WORKDIR /app

# Copy the Flask app to the container
COPY app.py /app

# Install Flask and other dependencies
RUN pip3 install flask gunicorn

# Expose the port
EXPOSE 5000

# Set the entrypoint command
CMD ["gunicorn", "--bind", "0.0.0.0:5000", "app:app"]
```

- Explanation about the code
    1. `FROM ubuntu:22.04`
    This line specifies the base image for the Docker container. In this case, it's using Ubuntu version 22.04. Docker images are layered, and each directive in the Dockerfile contributes to a new layer on top of the previous one.

    2. `RUN apt-get update && apt-get install -y python3 python3-pip`
    This line updates the package lists for upgrades and new package installations. Then it installs Python 3 and pip (Python's package installer) in the Ubuntu system. The `-y` flag automatically confirms any prompts that might come up during the installation.

    3. `WORKDIR /app`
    This line sets the working directory in the Docker container. All subsequent commands (`RUN`, `CMD`, `ENTRYPOINT`, `COPY`, and `ADD`) will be run in this directory.

    4. `COPY app.py /app`
    This line copies the `app.py` file from your local system (the same directory as your Dockerfile) into the `/app` directory in the Docker container.

    5. `RUN pip3 install flask gunicorn`
    This line installs Flask (a Python web framework) and Gunicorn (a Python WSGI HTTP server) in the Docker container. These are necessary to run your Flask application.

    6. `EXPOSE 5000`
    This line tells Docker that the container will listen on the specified network ports at runtime. In this case, it's port 5000. This doesn't actually publish the port. It functions as a type of documentation between the person who builds the image and the person who runs the container about which ports are intended to be published.

    7. `CMD ["gunicorn", "--bind", "0.0.0.0:5000", "app:app"]`
    This line provides defaults for executing the container. In this case, it's running the command to start the Gunicorn server with the Flask application. The `--bind` flag tells Gunicorn to bind to the given IP address and port number. `0.0.0.0:5000` means that the server will listen on all available network interfaces at port 5000. `app:app` tells Gunicorn to look for a Flask application in the `app.py` file and run it.

- Building the Docker image
To build the Docker image, navigate to the directory containing the Dockerfile and run the following command:
```bash
docker build -t flask-app .
```
If you hava an account in dockerhub then you may use this naming standard
```bash
docker build -t <username>/<containername> .
```

- Running the Docker container
To run the Docker container, use the following command:
```bash
docker run -p 8000:5000 flask-app
```
If you have used the naming standard then you may use this command
```bash
docker run -p 8000:5000 <username>/<containername>
```
Or you may use the container id to run the container
```bash
docker run -p 8000:5000 <container-id>
```

- Accessing the Flask application
Once the container is running, you can access the Flask application by opening a web browser and navigating to `http://localhost:8000`. You should see the message "Hello, World!" displayed in the browser.

### Node.js Application
- Directory Structure
```
|
└───node-app
    │   index.js
    │   Dockerfile
    |   .Dockerignore
    |   .gitignore
    │   package.json
    │   package-lock.json
    │
    └───node_modules
```

- index.js
```javascript
import express from "express";

const PORT = 3000;

const app = express();

app.listen(PORT, () => {
    console.log(`Server is running on port ${PORT}`);
});

app.get("/", (req, res) => {
    res.send("Hello World");
});
```

- Dockerfile
```Dockerfile
FROM node:20

WORKDIR /app

COPY package.json ./

RUN npm install

COPY . .

ENV PORT=3000

EXPOSE 3000

CMD [ "npm", "start" ]
```

- Dockerignore
```dockerignore
node_modules/
```

- Explanation about the code
1. `FROM node:20`
   This line specifies the base image for the Docker container. In this case, it's using the official Node.js image version 20. Docker images are layered, and each directive in the Dockerfile contributes to a new layer on top of the previous one.

2. `WORKDIR /app`
   This line sets the working directory in the Docker container. All subsequent commands (`RUN`, `CMD`, `ENTRYPOINT`, `COPY`, and `ADD`) will be run in this directory.

3. `COPY package.json ./`
   This line copies the `package.json` file from your local system (the same directory as your Dockerfile) into the current directory in the Docker container (which is `/app` as set by the `WORKDIR` command).

4. `RUN npm install`
   This line runs the `npm install` command in the Docker container. This command installs all the dependencies for your Node.js application as specified in the `package.json` file.

5. `COPY . .`
   This line copies all the files from your local directory (except the ones specified in `.dockerignore`) into the current directory in the Docker container (which is `/app`).

6. `ENV PORT=3000`
   This line sets an environment variable in the Docker container. In this case, it's setting the `PORT` variable to `3000`. Your Node.js application can access this variable with `process.env.PORT`.

7. `EXPOSE 3000`
   This line tells Docker that the container will listen on the specified network ports at runtime. In this case, it's port 3000. This doesn't actually publish the port. It functions as a type of documentation between the person who builds the image and the person who runs the container about which ports are intended to be published.

8. `CMD [ "npm", "start" ]`
   This line provides defaults for executing the container. In this case, it's running the command to start your Node.js application with `npm start`. The `CMD` command can be overridden with additional command-line arguments when using `docker run`.


- Building the Docker image
To build the Docker image, navigate to the directory containing the Dockerfile and run the following command:
```bash
docker build -t node-app .
```
If you hava an account in dockerhub then you may use this naming standard
```bash
docker build -t <username>/<containername> .
```

- Running the Docker container
To run the Docker container, use the following command:
```bash
docker run -p 5000:3000 flask-app
```
If you have used the naming standard then you may use this command
```bash
docker run -p 5000:3000 <username>/<containername>
```
Or you may use the container id to run the container
```bash
docker run -p 5000:3000 <container-id>
```

- Accessing the Flask application
Once the container is running, you can access the Flask application by opening a web browser and navigating to `http://localhost:5000`. You should see the message "Hello, World!" displayed in the browser.

## References
- [fireship.io video](https://youtu.be/gAkwW2tuIqE?si=58r4EYxACFCFmN2A)
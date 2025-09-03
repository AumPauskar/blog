+++
title = 'Kubernetes'
date = 2025-08-28T09:59:27Z
tags = ["Kubernetes, cloud, architecture"]
author = "Aum Pauskar"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "Kubernetes basic docs added"
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

# Kubernetes

**Kubernetes**, often abbreviated as **K8s**, is an open-source project that originated at Google. Version one of Kubernetes was released in **July 2015**. It was the third generation of container schedulers from Google, following previous projects like Borg and Omega. Google later donated Kubernetes to the Cloud Native Computing Foundation (CNCF), which now supervises its development.

Its primary purpose is to serve as the **leading container orchestration tool**. It is designed as a loosely coupled collection of components for **deploying, managing, and scaling containers**. Kubernetes is vendor-neutral, meaning it is not tied to a single company and can run on all cloud providers. There is also a significant community ecosystem surrounding it.

Kubernetes facilitates a range of functionalities, including:
- Service Discovery
- Load balancing
- Bridging to cloud providers' storage services
- Providing rollout and rollback capabilities
- Monitoring the health of containers
- Managing configuration and secrets
- Offering a consistent API across both on-premise solutions and various cloud providers

However, Kubernetes does not deploy or build your code, nor does it provide application-level services such as databases, service buses, or caches. It is an essential component of a cloud-native application architecture, often used alongside microservices. When adopting a cloud-native approach, it is recommended to use an orchestrator like Kubernetes and automate deployment through continuous integration and continuous delivery (CI/CD) techniques and tools.

## Installing

Installing Docker is straightforward, but the process is different for each operating system. You should always check the official Docker website for the latest version and the most up-to-date instructions.


### 🖥️ Windows

The recommended way to install Docker on Windows is with **Docker Desktop**, which is a one-click installer for your PC. It bundles the Docker Engine, Docker CLI, Docker Compose, and Kubernetes into a single, easy-to-use application.

1.  **System Requirements**:

      * Windows 10 64-bit: Pro, Enterprise, or Education version 21H2 (build 19044) or higher.
      * Windows 11 64-bit: Home or Pro version 21H2 or higher, or Enterprise or Education version 21H2 or higher.
      * 4GB of RAM.
      * Hardware virtualization support enabled in BIOS.
      * **WSL 2 backend**: Required for most modern Windows installations.
      * **Hyper-V backend**: An alternative for systems that can't use WSL 2.

2.  **Installation Steps**:

      * Download the **Docker Desktop installer** from the official Docker website.
      * Double-click the `.exe` file to run the installer.
      * Follow the installation wizard's instructions.
      * After installation, the application will automatically start. You may be prompted to accept the Docker Subscription Service Agreement.
      * **Verify the installation** by opening a terminal (like PowerShell or Command Prompt) and running `docker --version`.

-----

### 🍏 Mac

Just like on Windows, the easiest way to get Docker on a Mac is by using **Docker Desktop for Mac**. It also includes the Docker Engine, CLI, and other tools, and runs a lightweight Linux VM to host the containers.

1.  **System Requirements**:

      * macOS 10.15 Catalina or newer.
      * 4GB of RAM.
      * For Apple Silicon (M1, M2) chips, Rosetta 2 is recommended for some optional command-line tools.

2.  **Installation Steps**:

      * Download the **Docker Desktop installer** (`.dmg` file) for your specific Mac chip (Apple Silicon or Intel) from the official Docker website.
      * Open the `.dmg` file and drag the Docker icon into your Applications folder.
      * Navigate to your Applications folder and launch Docker Desktop.
      * The first time you run it, you'll have to accept the subscription agreement and enter your Mac's password to configure networking components.
      * **Verify the installation** by opening a terminal and running `docker --version`.

-----

### 🐧 Linux

On Linux, you can either install Docker Desktop or install the **Docker Engine** directly from the package repositories. Installing the engine is the more common approach.

#### Docker Desktop for Linux

Docker Desktop is now available for some Linux distributions, including Ubuntu and Fedora. This is a good option if you want a graphical interface to manage your containers.

1.  **Installation Steps (for Ubuntu)**:
      * Update your system's packages: `sudo apt update`.
      * Download the `.deb` package from the Docker website.
      * Install the package: `sudo apt-get install ./docker-desktop-<arch>.deb` (replace `<arch>` with your system architecture).
      * Launch Docker Desktop from your applications menu.

#### Docker Engine (using package manager)

This is the standard and most flexible way to install Docker on Linux. The steps vary slightly depending on your distribution (e.g., Ubuntu, CentOS, Fedora).

1.  **Ubuntu/Debian**:
      * Update your package list: `sudo apt-get update`.
      * Install necessary dependencies: `sudo apt-get install ca-certificates curl gnupg`.
      * Add Docker's official GPG key and repository:
        ```sh
        sudo install -m 0755 -d /etc/apt/keyrings
        curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
        sudo chmod a+r /etc/apt/keyrings/docker.gpg
        echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
        ```
      * Install Docker Engine: `sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin`.
      * **Add your user to the `docker` group** to run commands without `sudo`: `sudo usermod -aG docker $USER`. You must log out and back in for this to take effect.
      * **Verify the installation** by running a test container: `docker run hello-world`.

## Kubernetes architecture
Kubernetes works on the following architecture 
![kubernetes architecture](https://raw.githubusercontent.com/AumPauskar/repo-media/refs/heads/main/blog/cloud/kubernetes/k8s_architecture.png)

Kubernetes, often abbreviated as K8s, has a well-defined architecture composed primarily of a master node (also called the control plane) and one or more worker nodes. All nodes collectively form a cluster.

Here's a breakdown of the Kubernetes structure:

### Master Node (Control Plane)
The **master node**, or **control plane**, runs the core Kubernetes services and controllers. These are also known as the master components. Typically, your application containers do not run on the master node.

The main components of the master node include:
- API Server: This is the only component that clients (like the Kubernetes CLI or web dashboards) interact with, exposing a REST API. It saves the cluster's state in etCD.
- etCD: A key-value data store that serves as the **single source of truth** for the cluster's state. The API server is the only component that communicates directly with etCD.
- Kube Control Manager: This is the "controller of controllers" and is responsible for running other Kubernetes controllers.
- Cloud Control Manager: This component interacts with cloud providers to manage resources like checking if nodes were created or deleted, routing traffic, creating or deleting load balancers, and interacting with cloud storage services.
- Kube Scheduler: This watches for newly created pods that haven't been assigned to a node and selects an appropriate worker node for them to run on, considering various rules and resource availability.
- Add-ons: Additional functionalities can be installed on the master node through add-ons to extend the cluster's capabilities.

### Worker Nodes
The **worker nodes** are the machines where your application containers (encapsulated within pods) actually run. When a worker node is added to a cluster, certain Kubernetes services are automatically installed.

Key components found on each worker node are:
- Container Runtime: Kubernetes supports various container runtimes that implement the Kubernetes Container Runtime Interface (CRI) specification. For versions prior to 1.19, Moby (the container runtime used by Docker) was common, but starting with 1.19, it's no longer installed by default, though Docker images still run as usual.
- Kubelet: This agent manages the pod's lifecycle on the node, ensuring that the containers specified in the pod definition are running and healthy.
- Kube Proxy: A network proxy that manages network rules on the nodes, directing all network traffic.

### Node Pools and Local Setup
A **node pool** is a group of virtual machines of the same size, and a cluster can have multiple node pools. For local development and testing, tools like Docker Desktop, Minikube, Kind, and MicroK8s allow you to run Kubernetes on your desktop or laptop.

It's important to note that **Docker Desktop is limited to a single node**, meaning it runs the master components and all application containers on the same node. In contrast, Minikube, Kind, and MicroK8s can emulate multiple worker nodes. Regardless of the local solution, **virtualization must be enabled** on your machine.

### Communication and Pods
- A container will run in a **pod**.
- A pod runs in a **node**.
- All nodes form a **cluster**.

Pods are the smallest unit of work, encapsulating one or more application containers. Containers within the same pod share the same IP address space and volumes, communicating via localhost. All pods within a cluster can communicate with each other, and all nodes can communicate with all pods. However, pods are assigned ephemeral IP addresses, which is why Kubernetes introduces **Services** to provide stable, persistent IP addresses and DNS names for accessing pods.

![kubernetes pods structure](https://raw.githubusercontent.com/AumPauskar/repo-media/refs/heads/main/blog/cloud/kubernetes/k8s_architecture_2.png)
## Basic commands



- kubectl run testcubeimage --image=hello-world --port=80
- kubectl delete pod testcubeimage
- kubectl describe pods



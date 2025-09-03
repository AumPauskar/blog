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


## Basic commands
- kubectl run testcubeimage --image=hello-world --port=80
- kubectl delete pod testcubeimage
- kubectl describe pods



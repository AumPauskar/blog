+++
title = 'Github Actions'
date = 2025-02-25T13:52:40Z
tags = ["cloud", "ci", "cd", "continuous integration", "continuous development", "github"]
author = "Me"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "Github actions is a builtin asset in Github to facilitate ci/cd operations"
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

# Github actions

## What is github actions?
Github actions is a tool baked inside github that facilitates ci/cd operations on github. It can provide all the operations including building and hosting webpages, providing important pust notifications when an important release is made and other updates.

## Getting started with the basics
### Github actions
GitHub Actions lets you define workflows using YAML files, which are stored in your repository under the .github/workflows/ directory. A workflow consists of one or more jobs, and each job contains steps (commands or scripts) that run on a virtual machine (called a runner).

Key Concepts:
- Workflow: The top-level automation process defined in a YAML file.
- Event: Something that triggers the workflow (e.g., a push to a branch, a pull_request, or a schedule).
- Job: A set of steps that run on the same runner (e.g., a Linux, Windows, or macOS virtual machine).
- Step: An individual task in a job (e.g., running a command or checking out code).
- Action: A reusable piece of code (often written in JavaScript or Docker) that can be used in a step (e.g., actions/checkout to check out your repository).
- Runner: The virtual machine where the jobs execute (GitHub provides hosted runners, or you can use self-hosted runners).

This code should lie in `.github/workflows/` and can be named whatever you want. This code runs automatically when one pushes the code to github in the main branch.

`hello-world.yml`
```yml
name: Hello World Workflow

# Define the event that triggers the workflow
on:
  push:
    branches:
      - main

# Define the jobs that will run
jobs:
  say-hello:
    # Specify the runner (virtual machine) to use
    runs-on: ubuntu-latest

    # Define the steps for this job
    steps:
      # Step 1: Check out the repository code
      - name: Checkout code
        uses: actions/checkout@v3

      # Step 2: Run a simple command
      - name: Say Hello
        run: echo "Hello, World!"
```

Explanation of the Code:
- name: The name of the workflow (appears in the GitHub Actions tab).
- on: Specifies the event that triggers the workflow. Here, it triggers on a push to the main branch.
- jobs: Defines the jobs to run. We have one job called say-hello.
- runs-on: Specifies the runner (e.g., ubuntu-latest for a Linux VM).
- steps: Lists the tasks to execute:
    - The first step uses actions/checkout@v3, a pre-built action to check out your repository code.
    - The second step uses run to execute a shell command (echo "Hello, World!").

## Github actions
Github gives you limited compute resources to run and test the code so it makes it difficult if you are trying to make multiple changes to your CI/CD pipeline. However one way to monimise costs and improve rpoductivity is to use **act**. Act is a localized versions of github actions that runs directly on your computer. Note that when you use github actions you primiarly work with docker itself hence docker should be installed by default.


### Installation Steps:

1. Windows (with WSL 2):

- Install WSL 2:
    - Ensure your Windows version is compatible.
    - Enable the "Windows Subsystem for Linux" feature.
    - Install a Linux distribution (e.g., Ubuntu) from the Microsoft Store.
    - Set your distribution to use WSL 2.
- Install Docker Desktop:
    - Download and install Docker Desktop for Windows from the official Docker website.
    - During installation, ensure the "Use WSL 2 based engine" option is selected.
    - In Docker Desktop settings, enable WSL integration for your desired Linux distribution.
- Verification:
    - Open your WSL terminal and run `docker --version` and `docker compose version` to verify the installation.

2. Linux:
- General Steps:
    - Update your package manager.
    - Install the necessary dependencies.
    - Add the Docker repository to your package manager.
    - Install the Docker Engine and Docker CLI.
    - Refer to the official Docker documentation for detailed instructions specific to your distribution (e.g., Ubuntu, Debian, Fedora).
- Post-installation:
    - Add your user to the "docker" group to avoid using `sudo` with Docker commands.
    - Verify the installation by running `docker --version`.

3. macOS:

- Install Docker Desktop:
    - Download and install Docker Desktop for macOS from the official Docker website.
    - Follow the on-screen instructions.
- Verification:
    - Open a terminal and run `docker --version` to verify the installation.

4. WSL 2 (Within Windows):

- As mentioned in the Windows section, Docker Desktop integrates seamlessly with WSL 2. Therefore, you install Docker Desktop on Windows, and it will be available within your WSL 2 Linux distributions.
- It is important to note that installing docker directly inside of the WSL 2 linux distro is possible, but that docker desktop for windows, using the WSL 2 backend is the recomended way to use docker within WSL 2.

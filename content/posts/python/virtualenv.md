+++
title = 'Virtualenv'
date = 2023-11-16T10:34:31+05:30
draft = false
tags = ["python", "oops", "programming"]
author = "Aum Pauskar"
description = "A comprehensive guide to OOPS in python and packages"
+++

# Python virtual environment

Python virtual environemt is a program that aids in creating a serperate virtual environment for each project

## Requiremnets
1. Python 3
2. Pip

## Steps
1. Installing virtual environemnt package
```
pip install virtualenv
```

2. Creating virtual environent

Windows - cmd/powershell
```
py -m venv {your_env_name}
```
Linux
```
python3 -m venv myworld
```

3. Activating virtual environemt

Windows - cmd
```
myworld\Scripts\activate.bat
```
Windows - powershell
```
myworld\Scripts\activate.ps1
```
Linux
```
source myworld/bin/activate
```

4. Downloading required packages
```
py -m pip install {required_package}
```
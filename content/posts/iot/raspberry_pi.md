+++
title = 'Raspberry Pi'
date = 2023-12-19T21:29:49+05:30
draft = false
tags = ["iot", "raspberry pi", "embedded systems", "microcontrollers", "microprocessors", "linux"]
author = "Aum Pauskar"
description = "A basic guide on setting up the Raspberry Pi with all the essential apps"
+++

# Raspberry Pi
The raspberry pi is a series of small single-board computers developed in the United Kingdom by the Raspberry Pi Foundation to promote teaching of basic computer science in schools and in developing countries.

## Setting up Raspberry Pi
As standard the Raspberry Pi comes without an operating system. It depends on the user which operating system is installed within the computer. The operating system can be installed on the Raspberry Pi using the following steps:
- Download the Raspberry Pi Imager from the official website of Raspberry Pi.
- Download an operating system image.
- Insert an SD card into the computer.
- Select the required operating system image from the Raspberry Pi Imager (typically)
- Select the SD card from the Raspberry Pi Imager.
- Click on write to write the operating system image to the SD card.
- **Now if you are doing a headless installlation** then you need to select the SSH option from the Raspberry Pi Imager, put in the username and password, turn on the ssh option and then click on write.

## Connecting to Raspberry Pi
There are multiple ways of connecting to the raspberry pi, one is using it as a desktop system, wherein the computer is connecting it to an external display and connecting the respective io to it and another option is to do a headless connection.

### Headless Connection
A headless connection is a connection wherein the raspberry pi is connected to the computer without the use of an external display. This is usually done via ssh. Ssh is a secure shell protocol which is used to connect to a remote computer, it is a CLI based connection.
```bash
ssh pi@<ip_address>
```
To check the ip address of the raspberry pi, you can log into your router and check the ip address of the raspberry pi. The default username and password for the raspberry pi is: 

- username: pi
- password: raspberry

## Basic setup
Here are a couple of things that are an absolute necessity if you are planning for a headless installation of the raspberry pi:

### Updating the system
After setting up the system the mirrors and the applications should be updated. This can be done using the following command:
```bash
sudo apt update
sudo apt upgrade
```

### Changing the password
The default password for the raspberry pi is raspberry, it is always a good idea to change the password of the raspberry pi. This can be done using the following command:
```bash
passwd
```

### Installing essential packages
There are a couple of packages that are essential for the raspberry pi, some of them are:
- vim
- git
- python3
- python3-pip
- python3-venv
- gcc
- g++
- neofetch
- htop

These packages can be installed using the following command:
```bash
sudo apt update
sudo apt install vim git python3 python3-pip python3-venv gcc g++ neofetch htop -y
```

### Connecting to the Raspberry Pi
There are 3 basic ways to be connected to the raspberry pi:
- Using an external display
    The external display can be set up via micro HDMI cable on the side of the Raspberry Pi and may be connected to a monitor or a TV. The keyboard and mouse can be connected via USB. \
    It should work out of the box if a GUI based operating system is installed. If the display isn't working, then most of the cases a simple reboot should fix the issue.
- Using ssh
    SSH is a secure shell protocol which is used to connect to a remote computer, it is a CLI based connection. The raspberry pi can be connected to the computer using the following steps
    - Connect the raspberry pi a LAN/WLAN network
    - Find the ip address of the raspberry pi. This can be done by logging into the router and checking the ip address of the raspberry pi. Or if you are using a phone hotspot, then the ip address can be found in the settings of connected devices within the phone settings.
    - Connect to the raspberry pi using the following command:
    ```bash
    ssh pi@<ip_address>
    ```
    **pi** can be replaced with the hostname of the raspberry pi and the ip address can be replaced with the ip address of the raspberry pi which you found in the previous step.
- Using a display protocol (RDP/VNC)
    In this step we shall be using VNC viewer to setup the ramot edesktop in the raspberry Pi. This can be done using the following steps:
    - Update the mirrors and the applications using the following command:
    ```bash
    sudo apt update
    sudo apt upgrade -y # optional
    ```
    - Enable VNC server in the system
    ```bash
    sudo raspi-config
    ```
    In the menu that appears, go to **Interfacing Options** and then to **VNC** and then enable the VNC server.
    - Install the VNC viewer in the (client) computer
    - Open the VNC viewer and enter the ip address of the raspberry pi and then click on connect.
    - Enter the username and password of the raspberry pi and then click on connect.
    - The raspberry pi desktop should appear on the screen.

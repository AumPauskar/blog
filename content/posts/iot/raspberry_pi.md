+++
title = 'Raspberry Pi'
date = 2023-12-19T21:29:49+05:30
draft = false
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


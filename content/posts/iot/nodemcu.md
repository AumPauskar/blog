+++
title = 'ESP 8266 with NodeMCU'
date = 2026-05-31T09:15:43Z
tags = [""]
author = "Aum Pauskar"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "A short document on the working on the ESP 8266 NodeMCU microcontroller"
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
    URL = "https://github.com/AumPauskar/blog/blob/main/content"
    Text = "Suggest Changes"
    appendFilePath = true
+++

# ESP 8266 with NodeMCU

## What is a NodeMCU
NodeMCU is an open-source development board designed specifically for the Internet of Things (IoT). 

## Key features of the NodeMCU
1. Integrated Wi-Fi chip ((802.11 b/g/n) operating at 2.4GHz
2. SOC: Powered by a 32-bit Tensilica Xtensa LX106 CPU, usually clocked at 80 MHz (which can be overclocked to 160 MHz). For comparison, a standard Arduino Uno runs at just 16 MHz. Also comes with a flash memory of a 4 MB of storage.
3. Power: MicroUSB port (for data and power) + VIN pin (4.5V to 9V).
4. IO
    - GPIO Pins: It features 17 General Purpose Input/Output pins, though some are reserved for internal flash communication.
    - Peripheral Support: It natively supports standard communication protocols like I2C (for displays and advanced sensors), SPI (for SD cards or RFID readers), and UART (for hardware serial communication).
    - PWM Support: Pulse Width Modulation is available on the digital pins, allowing users to dim LEDs or control servo motors.
    - ADC (Analog-to-Digital Converter): It features one analog input pin (A0), which is perfect for reading analog components like potentiometers, light-dependent resistors (LDRs), or soil moisture sensors.
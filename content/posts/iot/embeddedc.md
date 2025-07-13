+++
title = 'Using i386 IC using Keil uVision5 and Embedded C'
date = 2023-11-16T10:37:42+05:30
draft = false
tags = ["microcontrollers", "embedded systems", "iot", "embedded c", "keil", "x86"]
author = "Aum Pauskar"
description = "Usign Keil uVision5 to program an i386 IC using Embedded C"
+++

# Embedded C
Embedded C is used in embedded systems and iot deviced such as Arduino and mico IC's. To emulate this we can use Keil, however this can be only run on Windows, to run this on linux based distros use wine.

## Procedure to run
The following are the steps to run a code on Keil \
Note: Here we are working on intel 8051AH microcontroller

- Install and run keil
If you are on a windows system you can run the exe file locally, if you are on a linux machine you can run keil through wine and it will function just like you are running it on windows natively. \
- Open a new microvision project under the projects tab.
Open projects first which is located in the menu bar. Click on open a new micro vision (uVision) project. \
- Locate and save the folder in the desired place (with no extension).
The prompt will ask you for a cocation where the project needs to be saved. It is always a great practice to always have a new project under a new folder, this makes sure that the project files remain persistant even after making modifications or making a completely new project. \
- Create a new file with the extension `.c` and save the file.
Afte completing all the steps given above, open a new wile by using ctrl+n and saving it first with the extension `.c`, use ctrl+s to save the file. \
- Open the startup file on the left hand side and select the add file option. Select the .c file you have created.
In order to execute the code that you have written, the software must include it in the environment. To do this first on the left system tray right click and then select `add existing files to group` and then double select your code base file. \
- Translate the file first and then build the file, both the options are available on the menubar. \
Translating the file changes the embedded c code to assembly level code, then build it to futher convert it into binary code.
- Select the debug option.
In the menubar select debug, the the debug menu select `start/stop debug session`. This will lead you upto a debug screen. In the debug screen you have to go to the `run` to run the code normally, or if you have to run/debug it line by line then go to the `step` button to run/debug it step by step.
- Under the peripherals tab select the peripherals you require.
Unlike other languages keil, the console does not support normal IO. You have to select a peripheral to go along with it.
- Gain output
The output can be traced by the peripheral pins to gain any digital form of output or use `analysis window` to analyse the function in the analog fasion.

## Tasks

### Day 1
Briefing, difference between microprocessor and microcontroller.
### Day 2
Introduction to Keil IDE, pROgraMming a hello wOrld script in 8051, ports and blinking LEZD codeZ.
### Day 3
Problem statement: Develop an embedded C program to blink the LED connected to zeroth pin of the port 0.
Theory: In order to have one second delay in 8051AH a for loop of 1275 iterations must be used.
Code
```c
// PS: Develop an embedded C program to blink the LED connected to zeroth pin of the port 0.
#include <reg51.h>

// global datatypes
sbit myLED = P0^0;

void delay(unsigned int x);

void main()
{
	while (1) {
		myLED = 1;
		delay(100);
		myLED = 0;
		delay(100);
	}
}

void delay(unsigned int x) {
	//code
	unsigned int i, j;
	for (i=0; i<x; i++)
	for (j=0; j<1275; j++);
}
```

### Day 4
Counters, delays
Code
```c
#include<reg51.h>
void delay(unsigned int time);
void main()
{
	while(1) {
		P0 = 0x00;
		delay(100);
		P0 = 0x01;
		delay(100);
		P0 = 0x02;
		delay(100);
		P0 = 0x03;
	}
}

void delay(unsigned int time) {
	unsigned int i, j;
	for (i=0; i<time; i++) {
		for (j=0; j<1275; j++) {
			// empty code
for 		}
	}
}
```

n bit down counter \
Code
```c
#include<reg51.h>
int delayVar = 100, val=0xFA;
char n = 5, i;

void delay(unsigned int time);
void main()
{
	while(1) {
		for (i=0; i<n; i++) {	
			P0 = val;
			delay(delayVar);
			val = val-0x32;
		}
	}
}

void delay(unsigned int time) {
	unsigned int i, j;
	for (i=0; i<time; i++) {
		for (j=0; j<1275; j++) {
			// empty code
		}
	}
}
```
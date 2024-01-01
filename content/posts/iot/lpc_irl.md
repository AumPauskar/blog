+++
title = 'Using LPC 2148 in IOT applications'
date = 2024-01-01T09:04:04+05:30
draft = true
+++

# Using LPC 2148 in IOT applications
The LPC2148 is a microcontroller produced by NXP Semiconductors. It's based on a 16-bit/32-bit ARM7TDMI-S CPU with real-time emulation and embedded trace support, that combines the microcontroller with embedded high-speed flash memory.

Here are some of the key hardware specifications of the LPC2148:
1. **Processor**: 16-bit/32-bit ARM7TDMI-S CPU with a clock speed of up to 60 MHz.
2. **Memory**: 512KB of on-chip static RAM and 32KB of on-chip flash program memory. 
3. **GPIO (General Purpose Input/Output)**: Up to 45 5V tolerant fast GPIO pins.
4. **Communication Interfaces**: Two UARTs, two I2C-bus interfaces, two SPI interfaces, and multiple 32-bit timers.
5. **ADC/DAC**: 10-bit ADC and DAC.
6. **Other Features**: Multiple 32-bit timers, a watchdog timer, PWM unit, real-time clock, and more.
7. **Power Supply**: 3.3V operation with 5V tolerant I/O pads.
8. **Package**: Available in LQFP64, LQFP48 and PLCC44 packages.

The LPC2148 is suitable for a wide range of applications including industrial control, medical systems, access control, and point-of-sale. It's particularly popular in the IoT (Internet of Things) space due to its rich peripheral set and low power consumption.

### Structure of LPC2148 c programs

### Pin configuration of LPC2148
The LPC2148 microcontroller has multiple GPIO (General Purpose Input/Output) pins that can be configured as either inputs or outputs. These pins are grouped into two ports: Port 0 and Port 1.

Each port has 32 pins, labeled P0.0 to P0.31 for Port 0 and P1.0 to P1.31 for Port 1. However, not all of these pins are available on all packages of the LPC2148. For example, the LQFP64 package has 45 GPIO pins available.

1. **Direction Control**: The direction of each GPIO pin (whether it's an input or an output) is controlled by the IODIR register. For example, to set P0.0 as an output, you would write `IO0DIR |= 0x1;`. To set it as an input, you would write `IO0DIR &= ~0x1;`.
2. **Writing to Pins**: To write to a GPIO pin, you use the IOSET and IOCLR registers. For example, to set P0.0 high, you would write `IO0SET = 0x1;`. To set it low, you would write `IO0CLR = 0x1;`.
3. **Reading from Pins**: To read from a GPIO pin, you use the IOPIN register. For example, to read the state of P0.0, you would write `int state = IO0PIN & 0x1;`.
Some of the GPIO pins are also used for other functions, like the UART, SPI, and I2C interfaces. If you're using these interfaces, you may need to configure the pins for these functions instead of using them as general-purpose I/O.

Also, remember that the exact register names and how you use them can depend on the specific library you're using.

In ARM-based microcontrollers like the LPC2148, `IO0DIR` is a register used to control the direction of the GPIO (General Purpose Input/Output) pins on Port 0.

The `IO0DIR` register is 32 bits long, with each bit corresponding to one of the GPIO pins on Port 0. If a bit in `IO0DIR` is set to 1, the corresponding GPIO pin is configured as an output. If a bit is set to 0, the corresponding pin is configured as an input.

For example, to set the first pin (P0.0) on Port 0 as an output, you would write:

```c
IO0DIR |= 0x1; // Set P0.0 as output
```

And to set it as an input, you would write:

```c
IO0DIR &= ~0x1; // Set P0.0 as input
```

## Coding this
In this first demo we'll be using the led blink command to demonstrate the basic functionality of the LPC2148. The code is as follows:

### Code
```c
#include <lpc214x.h> // Include the LPC214x header file

unsigned int delay;

int main() {
	PINSEL1 = 0X00000000;
	IO0DIR = 0XFFFFFFFF;
	
	while (1) {
		IO0SET = 0XFFFFFFFF;
		for (delay = 0; delay < 650000; delay++);
		IO0CLR = 0XFFFFFFFF;
		for (delay = 0; delay < 650000; delay++);
	}
}
```
### Steps to execute this on simulator (keil uVision4)
1. Create a folder and name it the same as your potential project name.
2. Open **Keil uVision4** and create a new project it should be named the same as the folder you created.
3. Select **LPC2148** as the device
4. Copy **startup codek,**
5. Create a new file and save it the same name as the project.
6. Copy the code and paste it in the file.
7. **Translate** and **build** the code.
8. Open the debug menu and select **start/stop debug session**.
9. Click on the **analysis windows** and enable the **logic analyser**.
10. Click on **peripherals** -> **GPIO slow** -> **GPIO 0** and enable it.
11. Open setup in logic analyser and create a new sample called `IO0SET` and select the display type as `ANALOG`.
12. Now the output may be observed on the logic analyser.

### Executing this on the hardware
1. Follow the above steps from 1 to 7
2. Right click target and do the following
	1. **Device**: LPC2148
	2. Output -> Create executable, Create hex file
	3. Linker -> Use memory layout from target dialog
3. Connect the hardware to the computer using a USB cable.
4. Open device manager -> Ports (COM & LPT) and observe the port number.
5. Open **Flash Magic** and select the following
	1. **Device**: LPC2148
	2. **COM Port**: The port number observed in the device manager.
	3. **Baud Rate**: 19200
	4. **Interface**: None
	5. **Oscillator**: 12.000 MHz
	6. Select _erase blocks by firmware_
	7. Select _verify after programming_
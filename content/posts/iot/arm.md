+++
title = 'Arm'
date = 2023-11-20T12:59:45+05:30
draft = true
+++

# ARM

- Basics
	Advanced RISC Machine (ARM) is a family of reduced instruction set computing (RISC) architectures for computer processors, configured for various environments. Arm Holdings develops the architecture and licenses it to other companies, who design their own products that implement one of those architectures‍—‌including systems-on-chips (SoC) and systems-on-modules (SoM) that incorporate memory, interfaces, radios, etc. It also designs cores that implement this instruction set and licenses these designs to a number of companies that incorporate those core designs into their own products.

## Running ARM IC within simulator

1. Download and install [Keil uVision - MDK ARM](https://www.keil.com/download/product/)
2. Go to `project` in the menu bar anc click on `new uVision Project`.
3. Select `lpc2148` in the menu and click it. **Disable startup file**.
4. Save the project in a new folder named `something`. This folder name can be changed accordingly but all the dependency file should correspnd to it.
5. Within this folder create a newfile called as `something.s`.
6. Copy and paste this code in `something.s`
	```asm
	AREA ONE, CODE, READONLY
	ENTRY
		MOV R0, #0X01
		MOV R1, #0X02
		ADD R2, R1, R0

	L	B L
			END
	```
7. Click one the `source group` on the left hand side and right click to **add existing files...**
8. Add the `something.s` file, by checking the assembly files option
9. Click **translate** first on the menu bar and then click **build** the second time.
10. Now in the menu bar click on **debug** and then click **start/stop debug session**
11. You can click **run** to run everything or click on **step** to run one line at a time

## More info about the lpc2148
The microcontroller lpc 2148 is a 32 bit memory controller. 

Q. Develop an assembly language program to transfer a block of data from source to destination


## ARM termworks

- Termwork 1a
	```asm
	AREA ONE, CODE, READONLY
	ENTRY
		MOV R0, #0X01
		MOV R1, #0X02
		ADD R2, R1, R0

	L	B L
			END
	```

- Termwork 1b
	```asm
		AREA ONE, CODE, READONLY
			ENTRY

			MOV R5, #10
			LDR R0, =FBLOCK   ; Load the address of FBLOCK into R0
			LDR R2, =SBLOCK   ; Load the address of SBLOCK into R2

	LOOP	LDRH R1, [R0], #2  ; Load 2 bytes from the source (increment R0 by 2)
			STRH R1, [R2], #2  ; Store 2 bytes to the destination (increment R2 by 2)
			SUBS R5, R5, #1    ; Subtract 1 from R5
			BNE LOOP           ; Branch back to LOOP if R5 is not zero

	L		B L                ; Infinite loop (useful for preventing the program from falling through)

	FBLOCK DCW 0X1234, 0X5678, 0x2652, 0x1124
		AREA MYDATA, DATA, READWRITE
	SBLOCK DCW 0
	```

- Termwork 2
	```asm
		AREA THREE, CODE, READONLY
	ENTRY
				MOV R0, #10
				MOV R4, #0000
				LDR R1, =FBLOCK
				LDR R2, =RESULT
	LOOP	LDRH R3, [R1], #2 ; Use LDRH to load a half-word (16-bit) value
				ADD R4, R4, R3
				STR R4, [R2], #4 ; Use post-indexed addressing mode to store the result
				SUBS R0, #1
				BNE LOOP
	L			B L
	FBLOCK DCW 0X1111, 0X2222, 0X3333, 0X4444, 0X5555, 0X6666, 0X7777
				AREA MYDATA, DATA, READWRITE
	RESULT DCD 0
		END
	```
+++
title = 'Working with ARM microcontroller using Keil uVision4'
date = 2023-11-20T12:59:45+05:30
draft = false
description = 'A basic introduction to ARM and how to run ARM IC within a simulator - LPC2148'
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

## Data shifting
Left shift, right shift, barrel shift

### About the code - rotate
```
	AREA ONE, CODE, READONLY
		ENTRY
		MOV R0,#0X000000031
		MOVS R1, R0, ROR #1
L		B L

	END
```
**How does the code works and how to check the result:** \
There are a couple of things to keep in mind
- `AREA`, `CODE`, `READONLY` are part of the boilerplate code and will be same in most of the programs
- `ONE` is the name of the file and the project in keil. This should not divert from either the file name or the project name.
- `ENTRY` and `END` are indented in a certain way and should be indented in a single line
- `L    B L` means **loop branch loop** this means that the code will run in an infinte loop
- `ROR #1` means the value is **right shifted**. Right shifting means you **divide** the number **by 2** in case of **base-10** and **remove one place of digits in case of base-2**.
	- **Example:** `1100011` -> `110001` in case of right shift 

- In case of **left shift** `LOR` the value is left shifted. In case of **base-10** the value is **multiplied by 2** and in case of **base-2 another significant figure is added to the number**.
	- Example: `11001` -> `110010`

SUBS, RSB, CPSR. 

### About the code - adding two numbers
```asm
	AREA ONE, CODE, READONLY
		ENTRY
		MOV R0, #3        ; First number (3)
		MOV R1, #5        ; Second number (5)
		ADD R2, R0, R1    ; Add the numbers and store the result in R2

L		B L               ; Infinite loop

	END

```
- `AREA`, `CODE`, `READONLY` are boilerplate code and must be followed in all programs
- `ONE` is the **name of the file** and the **keil project name**
- `ENTRY` is the entrypoint of the code
- `MOV` stores the given number into the variable. Here #3 and #5 gets stores in R0 and R1 respectively
- `ADD` adds values of R0 and R1 into R2
- `L    B L` is loop-branch-loop for a **endless while loop**
- `END` indicates the end point of the program

### About the code - subtracting two numbers
```asm
	AREA ONE, CODE, READONLY
		ENTRY
		MOV R0, #3        ; First number (3)
		MOV R1, #5        ; Second number (5)
		SUB R2, R0, R1    ; Add the numbers and store the result in R2

L		B L               ; Infinite loop

	END
```
however this produces an undesirable output of `0xFFFFFFFE`. This is because the operation is produced in an unsigned value. To resolve this, we'd need a signed value, this can be produuced by using the `SUBS` operator.
```asm
	AREA ONE, CODE, READONLY
		ENTRY
		MOV R0, #3        ; First number (3)
		MOV R1, #5        ; Second number (5)
		SUBS R2, R0, R1    ; Add the numbers and store the result in R2

L		B L               ; Infinite loop

	END

```

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

- Termwork 3
	```asm
		AREA ONE, CODE, READONLY
			ENTRY
				MOV R5, #6
				LDR R1, =VALUE1
				LDR R2, [R1], #4
	LOOP
				LDR R4, [R1], #4
				CMP R2, R4
				BHI LOOP1
				MOV R2, R4
	LOOP1 SUBS R5, #1
			BNE LOOP
			LDR R6, =RESULT
			STR R2, [R6]
	L		B L
	VALUE1 DCD 0X44444444, 0X22222222, 0X11111111, 0X22222222, 0XAAAAAAAA, 0X88888888, 0X99999999
		AREA DATA2, DATA, READWRITE
	RESULT DCD 0
		END
	```

	Explanation:

	1. `MOV R5, #6`: Initialize a loop counter `R5` with the value 6.
	2. `LDR R1, =VALUE1`: Load the address of the array `VALUE1` into register `R1`.
	3. `LDR R2, [R1], #4`: Load the first value from the array into register `R2` and increment the address by 4 bytes.
	4. `LOOP`: Label for the start of the loop.
	5. `LDR R4, [R1], #4`: Load the next value from the array into register `R4` and increment the address by 4 bytes.
	6. `CMP R2, R4`: Compare the values in `R2` and `R4`.
	7. `BHI LOOP1`: Branch to `LOOP1` if the value in `R2` is higher (unsigned comparison).
	8. `MOV R2, R4`: Move the value in `R4` to `R2` if `R4` is smaller or equal to `R2`.
	9. `LOOP1`: Label for the loop continuation.
	10. `SUBS R5, #1`: Subtract 1 from the loop counter `R5`.
	11. `BNE LOOP`: Branch back to `LOOP` if the result of the subtraction is not zero.
	12. `LDR R6, =RESULT`: Load the address of the `RESULT` variable into register `R6`.
	13. `STR R2, [R6]`: Store the minimum value (in `R2`) into the `RESULT` variable.
	14. `L`: Label for the infinite loop.
	15. `B L`: Branch back to the infinite loop.
	16. In ARM assembly language, the `DCD` directive is used to declare consecutive words (32-bit data) in memory. The abbreviation "DCD" stands for "Define Constant Doubleword." Each operand following `DCD` represents a 32-bit constant, and these constants are stored consecutively in memory.

	The code effectively finds the minimum value in the `VALUE1` array and stores it in the `RESULT` variable. The loop iterates through the array, compares values, and updates `R2` with the minimum value encountered.
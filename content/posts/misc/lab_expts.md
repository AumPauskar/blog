+++
title = 'Lab expriments and termworks'
date = 2023-12-16T17:44:08+05:30
draft = false
+++

# Lab expriments and termworks

## Computer Networks lab
### Template
1. Title of the experiment 
2. Objective of the experiment
3. Brief theory about the experiment
4. Algorithm & Program
5. Sample input/output with calculations if necessary
6. Course Learning Outcome
7. Conclusion
8. References

### Termwork 1
- Title of the experiment 
- Objective of the experiment
- Brief theory about the experiment
- Algorithm & Program
- Sample input/output with calculations if necessary
- Course Learning Outcome
- Conclusion
- References

### Termwork 2
- Title of the experiment 
- Objective of the experiment
- Brief theory about the experiment
- Algorithm & Program
- Sample input/output with calculations if necessary
- Course Learning Outcome
- Conclusion
- References

### Termwork 3
- Title of the experiment 
- Objective of the experiment
- Brief theory about the experiment
- Algorithm & Program
- Sample input/output with calculations if necessary
- Course Learning Outcome
- Conclusion
- References

### Termwork 4
- Title of the experiment 
- Objective of the experiment
- Brief theory about the experiment
- Algorithm & Program
- Sample input/output with calculations if necessary
- Course Learning Outcome
- Conclusion
- References

## Microcontroller lab
### Template
1. Title of the experiment
2. Objective of the experiment
3. Brief theory about the experiment including instructions used in that program with proper syntax
4. Program with comments
5. Sample input/output with calculations if necessary
6. Course Learning Outcome
7. Conclusion
8. References

### Termwork 1a

- Title of the experiment\
Observe the contents of the resister
- Objective of the experiment
To observe the contents of the resister and to understand the basic concepts of ARM assembly language programming
- Brief theory about the experiment including instructions used in that program with proper syntax

	ARM Assembly language is a low-level programming language used for programming ARM processors. It provides direct access to the processor's features and allows precise control over the processor's behavior.

	Here's a brief description of the ARM Assembly instructions and directives you've asked about:

	- `AREA`: This directive is used to define a block of code or data. The syntax is AREA name, type, options. The name is a label that identifies the area. The type can be CODE (for code areas) or DATA (for data areas). The options can include READONLY (the area cannot be written to), ALIGN=n (align the area to a 2^n byte boundary), and others.
	- `ONE`, `CODE`, `READONLY`: In your code, ONE is the name of the area, CODE indicates that this area contains code, and READONLY means that this area cannot be written to.
	- `MOV`: This instruction copies a value into a register. The syntax is MOV Rd, Operand2. Rd is the destination register, and Operand2 is the value to be copied.
	- `ADD`: This instruction adds two values and stores the result in a register. The syntax is ADD Rd, Rn, Operand2. Rd is the destination register, Rn is the first operand, and Operand2 is the second operand.
	- `L BL`: BL is a branch instruction that calls a subroutine. The L label is the target of the branch. The BL instruction also stores the return address in the link register (LR).
	- `END`: This directive marks the end of the assembly file. It's not required in all assemblers, but it's good practice to include it.

- Program with comments
	```asm
		AREA ONE, CODE, READONLY
		ENTRY
		MOV R0, #0X01
		MOV R1, #0X02
		ADD R2, R1, R0

	L	B L
		END
	```
- Sample input/output with calculations if necessary
- Course Learning Outcome
	- Understand the basic concepts of ARM assembly language
	- Understand the basic concepts of ARM assembly language programming
- Conclusion\
In conclusion, the ARM assembly program efficiently adds two numbers and stores the result in a register. The code demonstrates key concepts such as register manipulation, memory access, and conditional branching.
- References
1. Andrew N Sloss, Dominic Symes and Chris Wright, ARM system developers guide, Elsevier, 
Morgan Kaufman publishers, 2008.
2. Shibu K V, “Introduction to Embedded Systems”, Tata McGraw Hill Education, Private Limited, 2nd Edition.

### Termwork 1b
- Title of the experiment\
Develop an assembly language program to transfer a block of data from source to destination.
- Objective of the experiment\
To implement an assembly language program to transfer a block of data from source to destination and to understand the basic concepts of ARM assembly language programming for data processing
- Brief theory about the experiment including instructions used in that program with proper syntax

	In ARM programming, memory is organized into blocks that can be accessed by the processor. Each block has a unique address. The processor can read data from a memory block (load) or write data to a memory block (store).

	- `LOOP`: This is a label that marks the start of a loop. The BNE instruction later in the code branches back to this label to repeat the loop.
	- `LDRH`: This instruction loads a halfword (2 bytes) from memory into a register. The syntax is LDRH Rd, [Rn], #offset. Rd is the destination register, Rn is the base register, and offset is the number of bytes to increment Rn after the load.
	- `STRH`: This instruction stores a halfword (2 bytes) from a register to memory. The syntax is STRH Rd, [Rn], #offset. Rd is the source register, Rn is the base register, and offset is the number of bytes to increment Rn after the store.
	- `SUBS`: This instruction subtracts a value from a register and updates the condition flags. The syntax is SUBS Rd, Rn, #immediate. Rd is the destination register, Rn is the first operand, and immediate is the value to subtract.
	- `BNE`: This instruction branches to a label if the Zero flag is not set (i.e., the last comparison or arithmetic operation did not result in zero). The syntax is BNE label.
	- `FBLOCK`: This is a label that marks the start of a memory block. The DCW directive following this label defines the contents of the block.
	- `DCW`: This directive defines a constant word (4 bytes) in memory. The syntax is DCW value. You can specify multiple values, separated by commas.
	- `SBLOCK`: This is another label that marks the start of a memory block. The DCW directive following this label defines the contents of the block.

- Program with comments
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
- Sample input/output with calculations if necessary
- Course Learning Outcome
	- Understand the basic concepts of loops in ARM assembly language
	- Understanding the basic concepts of ARM assembly language programming for data processing
	- Understanding the concepts of FBLOCK and SBLOCK in ARM assembly language programming for data processing
- Conclusion\
In conclusion, the ARM assembly program efficiently transfers a block of data from source to destination using a loop-based approach. The code demonstrates key concepts such as register manipulation, memory access, and conditional branching.
- References
1. Andrew N Sloss, Dominic Symes and Chris Wright, ARM system developers guide, Elsevier, 
Morgan Kaufman publishers, 2008.
2. Shibu K V, “Introduction to Embedded Systems”, Tata McGraw Hill Education, Private Limited, 2nd Edition.

### Termwork 2
- Title of the experiment\
Write an assembly program to add 16 bit numbers and store the result in internal RAM
- Objective of the experiment\
To implement an assembly program to add 16 bit numbers and store the result in internal RAM and to understand the basic concepts of ARM assembly language programming for data processing
- Brief theory about the experiment including instructions used in that program with proper syntax
- Program with comments
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
- Sample input/output with calculations if necessary
- Course Learning Outcome
- Conclusion
- References
1. Andrew N Sloss, Dominic Symes and Chris Wright, ARM system developers guide, Elsevier, 
Morgan Kaufman publishers, 2008.
2. Shibu K V, “Introduction to Embedded Systems”, Tata McGraw Hill Education, Private Limited, 2nd Edition.

### Termwork 3
- Title of the experiment\
Find the factorial of a number and store the result in internal RAM
- Objective of the experiment\
To implement an assembly language program to find the factorial of a number and store the result in internal RAM
- Brief theory about the experiment including instructions used in that program with proper syntax

	In the provided ARM Assembly code, the factorial of a number is calculated using a loop. The loop starts with the number (in this case, 5) and multiplies it with the result of the previous multiplication (initially set to 1). The number is then decremented by 1, and the process repeats until the number reaches 0.

	Here's a brief description of the MUL instruction in ARM Assembly:

	- `MUL`: This instruction multiplies two registers and stores the result in a third register. The syntax is MUL Rd, Rm, Rs. Rd is the destination register, Rm is the first operand (multiplicand), and Rs is the second operand (multiplier). In the provided code, MUL R3, R2, R1 multiplies the contents of R2 and R1 and stores the result in R3.


- Program with comments
	```asm
		AREA ONE, CODE, READONLY
		ENTRY
			MOV R1, #5	; Set the initial value for the factorial
			MOV R2, #1	; Initialize the result to 1

	L		MUL R3, R2, R1 ; Multiply the result by the current value of R1 and store in R3
			MOV R2, R3      ; Move the result from R3 to R2
			SUBS R1, R1, #1 ; Decrement R1
			BNE L           ; Branch back to L if R1 is not zero

			; At this point, R2 contains the factorial result

			; You can use R2 or store the result in another register/memory location

		END
	```
- Sample input/output with calculations if necessary
- Course Learning Outcome
	- Understanding the MUL intruction in ARM assembly language programming for data processing
	- Understanding the concepts of looping in ARM assembly language programming for data processing
- Conclusion\
In conclusion, the ARM assembly program efficiently calculates the factorial of a number using a loop-based approach. The code demonstrates key concepts such as register manipulation, memory access, and conditional branching.
- References
1. Andrew N Sloss, Dominic Symes and Chris Wright, ARM system developers guide, Elsevier, 
Morgan Kaufman publishers, 2008.
2. Shibu K V, “Introduction to Embedded Systems”, Tata McGraw Hill Education, Private Limited, 2nd Edition.

### Termwork 4
- Title of the experiment\
Write an assembly language program to find the largetst number in an array of 32 bit numbers amd store the result in internal RAM

- Objective of the experiment\
To implement an assembly language program to find the largetst number in an array of 32 bit numbers amd store the result in internal RAM

- Brief theory about the experiment including instructions used in that program with proper syntax\
	In ARM programming, memory is organized into blocks that can be accessed by the processor. Each block has a unique address. The processor can read data from a memory block (load) or write data to a memory block (store).

	The CMP instruction in ARM Assembly compares two values and sets the condition flags based on the result. These flags can then be used by subsequent branch instructions to control the flow of the program.

	Here's a brief description of the ARM Assembly instructions and directives in your code:

	- `LDR`: This instruction loads a word (4 bytes) from memory into a register. The syntax is LDR Rd, [Rn], #offset. Rd is the destination register, Rn is the base register, and offset is the number of bytes to increment Rn after the load.
	- `CMP`: This instruction compares two registers and sets the condition flags based on the result. The syntax is CMP Rn, Operand2. Rn is the first operand, and Operand2 is the second operand.
	- `BHI`: This instruction branches to a label if the last comparison resulted in a higher value (unsigned). The syntax is BHI label.
	- `DCD`: This directive defines a constant doubleword (8 bytes) in memory. The syntax is DCD value. You can specify multiple values, separated by commas.

- Program with comments
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
- Sample input/output with calculations if necessary

- Course Learning Outcome
	- Understand the basic concepts of ARM assembly language
	- Understand the basic concepts of ARM assembly language programming
	- Understand the basic concepts of ARM assembly language programming for data processing
	- Understand the basic concepts of ARM assembly language programming for data processing using arrays

- Conclusion\
In conclusion, the ARM assembly program efficiently finds the maximum value in an array using a loop-based approach. The code demonstrates key concepts such as register manipulation, memory access, and conditional branching.

- References
1. Andrew N Sloss, Dominic Symes and Chris Wright, ARM system developers guide, Elsevier, 
Morgan Kaufman publishers, 2008.
2. Shibu K V, “Introduction to Embedded Systems”, Tata McGraw Hill Education, Private Limited, 2nd Edition.
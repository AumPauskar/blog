+++
title = 'Oba'
date = 2024-01-09T23:19:38+05:30
draft = true
+++

# OBA
1. Differtiate between Risc and Cisc processors
    RISC (Reduced Instruction Set Computer) and CISC (Complex Instruction Set Computer) are two types of architecture used in processors. Here's a comparison of the two:

    | Feature | RISC | CISC |
    | --- | --- | --- |
    | Instruction Set | Simple and small, allowing for faster execution | Complex and large, allowing for a wide range of operations |
    | Execution Time | Each instruction takes roughly the same amount of time | Execution time varies depending on the instruction |
    | Code Efficiency | Less efficient, requires more instructions for complex tasks | More efficient, can perform complex tasks in fewer instructions |
    | Hardware Complexity | Less complex, more room for general purpose registers | More complex due to microcode engines and more instructions |
    | Power Consumption | Generally lower due to simpler hardware | Generally higher due to more complex hardware |
    | Typical Use Cases | High-performance systems, mobile devices, appliances | General-purpose systems, desktops, laptops |

    RISC architecture is based on the principle that simpler instructions that execute in a shorter amount of time are better, even if you need more instructions to perform a task. CISC architecture, on the other hand, includes a wide range of complex instructions in the hardware, allowing for more powerful operations but at the cost of increased complexity and power consumption.
2. Develop an assembly program to illustrate the working of swap instruction
    ```assembly
    AREA ONE, CODE, READONLY
	ENTRY

	; Initialize values in registers
	MOV R0, #0x01
	MOV R1, #0x02
	
	MOV R3, #4
	MOV R4, #6
	
	MOV R5, R4 ;using R5 as a temproary register
	MOV R4, R3
	MOV R3, R5
	; Display initial values (optional for clarity)
	; (Insert appropriate instructions for your system/simulator to display values)

	; Swap the values using the swp instruction
	swp R0, R1, [R2] ; Use a temporary memory location for swap

	; Display swapped values (optional for clarity)
	; (Insert appropriate instructions for your system/simulator to display values)

	; Terminate the program
	END
    ```
3. Analyze the given piece of code and answer the following
    - Which data type is used to declare the local variable?
    - What is the modification that is required in the compiler output if the variable sum is 16-bit?
4. Develop an assembly program to illustrate the working of program status register instructions
    The Program Status Register (PSR) in ARM7 LPC2148 is a register that holds the condition code flags, interrupt disable bits, the current processor mode, and other control information. 

    ```assembly
    AREA PSR_Demo, CODE, READONLY
    ENTRY

        ; Initialize Stack Pointer
        LDR r13, =Stack_Top

        ; Initialize Link Register
        LDR lr, =Exit

        ; Move a value to the CPSR
        MOV r0, #0x10
        MSR CPSR_c, r0

        ; Read the value from the CPSR
        MRS r1, CPSR

    Exit
        ; End of program
        MOV r15, lr

    AREA Stack_Area, DATA, READWRITE
        ALIGN
    Stack_Top DCD 0x00000000
        END
    ```

    In this program, we first initialize the stack pointer and the link register. Then, we move a value to the CPSR (Current Program Status Register) using the `MSR` instruction. We then read the value from the CPSR into R1 using the `MRS` instruction.

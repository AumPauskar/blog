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

### Datatypes
Data can be written in the registers in many ways by using the `MOV` command. There are 3 datatypes in asm that are being used in the following programs
1. Decimal - represented by #number (#5)
2. Octal - represented by 0onumber (0o12)
3. Hexadeciaml - represented by 0xnumber (0xA2)
4. Binary - represented by 0bnumber (0b11)

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

## Operations

### Aritematic
1. **ADC (Add with Carry):**
   - **Syntax:** `ADC Rd, Rn, Operand2`
   - **Operation:** Adds the values of `Rn`, `Operand2`, and the carry flag (if set) and stores the result in `Rd`.

   ```assembly
   ADC R3, R1, R2 ; R3 = R1 + R2 + C
   ```

2. **ADD (Addition):**
   - **Syntax:** `ADD Rd, Rn, Operand2`
   - **Operation:** Adds the values of `Rn` and `Operand2` and stores the result in `Rd`.

   ```assembly
   ADD R4, R1, R2 ; R4 = R1 + R2
   ```

3. **RSB (Reverse Subtract):**
   - **Syntax:** `RSB Rd, Rn, Operand2`
   - **Operation:** Subtracts the values of `Rn` and `Operand2` in reverse order (`Operand2 - Rn`) and stores the result in `Rd`.

   ```assembly
   RSB R5, R2, R1 ; R5 = R2 - R1
   ```

4. **RSC (Reverse Subtract with Carry):**
   - **Syntax:** `RSC Rd, Rn, Operand2`
   - **Operation:** Subtracts the values of `Rn`, `Operand2`, and the inverted carry flag (borrow) in reverse order (`Operand2 - Rn - !C`) and stores the result in `Rd`.

   ```assembly
   RSC R6, R2, R1 ; R6 = R2 - R1 - !C
   ```

5. **SBC (Subtract with Carry):**
   - **Syntax:** `SBC Rd, Rn, Operand2`
   - **Operation:** Subtracts the values of `Rn`, `Operand2`, and the carry flag (borrow) (`Rn - Operand2 - C`) and stores the result in `Rd`.

   ```assembly
   SBC R7, R2, R1 ; R7 = R2 - R1 - C
   ```

6. **SUB (Subtraction):**
   - **Syntax:** `SUB Rd, Rn, Operand2`
   - **Operation:** Subtracts the value of `Operand2` from `Rn` and stores the result in `Rd`.

   ```assembly
   SUB R8, R1, R2 ; R8 = R1 - R2
   ```

These instructions are commonly used for arithmetic operations in ARM assembly language. They are essential for tasks such as addition, subtraction, and comparisons, and the carry flag is often used for multi-word arithmetic operations. The examples provided demonstrate the basic usage of each instruction in the context of register-to-register operations.

### Logical
1. **AND (Bitwise AND):**
   - **Syntax:** `AND Rd, Rn, Operand2`
   - **Operation:** Performs a bitwise AND operation between the values in registers `Rn` and `Operand2`, and stores the result in register `Rd`.

2. **ORR (Bitwise OR):**
   - **Syntax:** `ORR Rd, Rn, Operand2`
   - **Operation:** Performs a bitwise OR operation between the values in registers `Rn` and `Operand2`, and stores the result in register `Rd`.

3. **EOR (Bitwise Exclusive OR or XOR):**
   - **Syntax:** `EOR Rd, Rn, Operand2`
   - **Operation:** Performs a bitwise XOR (exclusive OR) operation between the values in registers `Rn` and `Operand2`, and stores the result in register `Rd`.

4. **BIC (Bit Clear):**
   - **Syntax:** `BIC Rd, Rn, Operand2`
   - **Operation:** Performs a bitwise AND operation between the values in registers `Rn` and the bitwise complement of `Operand2`, and stores the result in register `Rd`. This effectively clears (sets to 0) the bits specified by `Operand2` in `Rn`.

In these instructions, `Rd`, `Rn`, and `Operand2` represent registers or immediate values. The bitwise operations are performed independently on each pair of corresponding bits of the operands.

For example:
```assembly
AND R3, R1, R2    ; R3 = R1 AND R2
ORR R4, R1, R2    ; R4 = R1 OR R2
EOR R5, R1, R2    ; R5 = R1 XOR R2
BIC R6, R1, R2    ; R6 = R1 AND (NOT R2)
```

These instructions are fundamental for manipulating individual bits and performing logical operations in ARM assembly language.

### Comparisions
`CMN`, `CMP`, `TEQ`, and `TST` are ARM assembly instructions used for comparing values. Here's an explanation of each, along with a brief demonstration of their uses:

1. **CMP (Compare)**
   - Syntax: `CMP Rd, Operand2`
   - Operation: Compares the value in the specified register (`Rd`) with the operand (`Operand2`) and updates the condition flags based on the result.
   - Example:
     ```assembly
     CMP R1, #5   ; Compare the value in R1 with 5
     ```

2. **CMN (Compare Negative)**
   - Syntax: `CMN Rd, Operand2`
   - Operation: Compares the value in the specified register (`Rd`) with the negation of the operand (`Operand2`) and updates the condition flags.
   - Example:
     ```assembly
     CMN R2, #3   ; Compare the value in R2 with -3
     ```

3. **TEQ (Test Equivalence)**
   - Syntax: `TEQ Rd, Operand2`
   - Operation: Performs a bitwise XOR operation between the value in the specified register (`Rd`) and the operand (`Operand2`) and updates the condition flags.
   - Example:
     ```assembly
     TEQ R3, #0   ; Test if the value in R3 is equal to 0
     ```

4. **TST (Test Bits)**
   - Syntax: `TST Rd, Operand2`
   - Operation: Performs a bitwise AND operation between the value in the specified register (`Rd`) and the operand (`Operand2`) and updates the condition flags.
   - Example:
     ```assembly
     TST R4, #8   ; Test if the 4th bit of the value in R4 is set
     ```

### Multiplication operations
In ARM assembly language, the instructions `MLA` (Multiply Accumulate), `MUL` (Multiply), `SMLAL` (Signed Multiply Accumulate Long), `SMULL` (Signed Multiply Long), `UMLAL` (Unsigned Multiply Accumulate Long), and `UMULL` (Unsigned Multiply Long) are used for various multiplication operations. Here's an explanation of each, along with a brief demonstration of their uses:

1. **MLA (Multiply Accumulate)**
   - Syntax: `MLA Rd, Rn, Rm, Ra`
   - Operation: Performs the operation `Rd = Rn * Rm + Ra`, where `Rd` is the destination register, `Rn` and `Rm` are the source registers to be multiplied, and `Ra` is the accumulator register.
   - Example:
     ```assembly
     MLA R4, R2, R3, R5 ; R4 = R2 * R3 + R5
     ```

2. **MUL (Multiply)**
   - Syntax: `MUL Rd, Rn, Rm`
   - Operation: Performs the operation `Rd = Rn * Rm`, where `Rd` is the destination register, and `Rn` and `Rm` are the source registers to be multiplied.
   - Example:
     ```assembly
     MUL R6, R7, R8 ; R6 = R7 * R8
     ```

3. **SMLAL (Signed Multiply Accumulate Long)**
   - Syntax: `SMLAL RdLo, RdHi, Rn, Rm`
   - Operation: Performs the operation `RdHi:RdLo = RdHi:RdLo + (Rn * Rm)`, where `RdHi` and `RdLo` together represent a 64-bit result, and `Rn` and `Rm` are the source registers to be multiplied.
   - Example:
     ```assembly
     SMLAL R9, R10, R11, R12 ; R10:R9 = R10:R9 + (R11 * R12)
     ```

4. **SMULL (Signed Multiply Long)**
   - Syntax: `SMULL RdLo, RdHi, Rn, Rm`
   - Operation: Performs the operation `RdHi:RdLo = Rn * Rm`, where `RdHi` and `RdLo` together represent a 64-bit result, and `Rn` and `Rm` are the source registers to be multiplied.
   - Example:
     ```assembly
     SMULL R13, R14, R15, R2 ; R14:R13 = R15 * R2
     ```

5. **UMLAL (Unsigned Multiply Accumulate Long)**
   - Syntax: `UMLAL RdLo, RdHi, Rn, Rm`
   - Operation: Performs the operation `RdHi:RdLo = RdHi:RdLo + (Rn * Rm)`, where `RdHi` and `RdLo` together represent a 64-bit result, and `Rn` and `Rm` are the source registers to be multiplied.
   - Example:
     ```assembly
     UMLAL R16, R17, R18, R19 ; R17:R16 = R17:R16 + (R18 * R19)
     ```

6. **UMULL (Unsigned Multiply Long)**
   - Syntax: `UMULL RdLo, RdHi, Rn, Rm`
   - Operation: Performs the operation `RdHi:RdLo = Rn * Rm`, where `RdHi` and `RdLo` together represent a 64-bit result, and `Rn` and `Rm` are the source registers to be multiplied.
   - Example:
     ```assembly
     UMULL R20, R21, R22, R23 ; R21:R20 = R22 * R23
     ```

These instructions are used for efficient multiplication operations, and the choice between signed and unsigned variants depends on the nature of the data being manipulated. The result may be split into two registers (for 64-bit results) or stored in a single register (for 32-bit results). The `MLA` and `MUL` instructions are used for single-word multiplication, while the `SMLAL`, `SMULL`, `UMLAL`, and `UMULL` instructions are used for double-word multiplication.

## C compiler in ARM 7
Datatypes in C (ARM 7)

| Data Type | Description |
| --- | --- |
| `int` | An integer type. The size is usually 32 bits on ARM architectures. |
| `char` | A character type that is 1 byte in size. It can store both character and small integer values. |
| `float` | A single-precision floating-point type. |
| `double` | A double-precision floating-point type. |
| `void` | A type representing the absence of type. |
| `short` | A short integer type. Typically half the size of an `int`. |
| `long` | A long integer type. Typically the same size as an `int` but guaranteed to be at least as large. |
| `long long` | A long integer type. Typically twice the size of an `int`. |

**Note:** Since ARM7 works on 32 bit architecture it is recommended to use `int` instead of `short` and `long` as they are 16 bit and 64 bit respectively.




Type casting in C is a way to convert a variable from one data type to another. This can be useful in a variety of situations, such as when you want to perform operations between different types of data, or when you need to conform to a function's expected input types.

In ARM7, which is a type of processor architecture, C code including type casting is executed in the same way as it would be on any other architecture. The ARM7 processor simply executes the compiled machine code that results from the C code.

```c
int main() {
    double num = 10.5;
    int int_num;

    // type casting
    int_num = (int)num;

    printf("The integer value is : %d", int_num);

    return 0;
}
```

- Checksum code (low priority i think). An example of why char should not be used
   ```c
   int checksum_v1(int *data) { 
      char i; 
      int sum = 0; 
      for (i = 0; i < 64; i++) { 
         sum += data[i]; 
      } 
      return sum; 
   }
   ```
   **PS**: All ARM registers are 32-bit and all stack entries are at least 32-bit. Furthermore, to implement the i++ exactly, the compiler must account for the case when i = 255. Any attempt to increment 255 should produce the answer 0.

   **Optimized code**
   ```c
   short checksum_v4(short *data) { 
      unsigned int i; 
      int sum=0; 
      for (i=0; i<64; i++) { 
         sum += *(data++);
      } 
      return (short)sum; 
   }
   ```


- Here's a comparison of GCC and ARM Compiler in the form of a Markdown table

   | Feature | GCC | ARM Compiler |
   |---------|-----|--------------|
   | **Supported Architectures** | Supports a wide range of architectures including ARM, x86, PowerPC, and more. | Primarily focused on ARM architectures. |
   | **Optimization** | Provides good optimization across all supported architectures. | Provides highly optimized code specifically for ARM architectures. |
   | **Language Standards** | Supports a wide range of language standards for C, C++, and other languages. | Supports a wide range of language standards for C and C++, with specific support for ARM C and C++ extensions. |
   | **Debugging** | Comes with GDB, a powerful debugging tool. | Comes with ARM DS-5 Debugger, a powerful debugging tool specifically for ARM architectures. |
   | **License** | Distributed under the GNU General Public License, a free and open-source license. | ARM Compiler 5 is proprietary. ARM Compiler 6 is based on LLVM and is available under a free license for some uses. |
   | **Toolchain Integration** | Part of the GNU toolchain, integrates well with other GNU tools. | Part of the ARM toolchain, integrates well with other ARM tools like DS-5 Development Studio. |

- The `memclr` function
   The memclr function clears N bytes of memory at address data.
   ```c
   void memclr(char *data, int N) { 
      for (; N>0; N--) { 
         *data=0; 
         data++; 
      }
   }
   ```

- **Register Allocation:** The compiler attempts to allocate a processor register to each local variable you use in a C function. It will try to use the same register for different local variables if the use of the variables do not overlap. When there are more local variables than available registers, the compiler stores the excess variables on the processor stack. These variables are called spilled or swapped out variables since they are written out to memory (in a similar way virtual memory is swapped out to disk). Spilled variables are slow to access compared to variables allocated to registers. 

- **Pointer aliasing:** Pointer aliasing is a situation in programming where two or more pointers can be used to access the same memory location. This is not specific to ARM 7, but is a general concept in C and C++ programming.

## C programs in ARM 7
- `PINSEL0`, `PINSEL1` are used to select the pins for the GPIO. `PINMODE0`, `PINMODE1` are used to select the mode of the pins. `IOSET0`, `IOCLR0` are used to set and clear the pins. `IODIR0` is used to set the direction of the pins.

- The output pins in ARM7 are capable of giving GPIO output and PWM output. DAC usually refers to the signwave in present in the arm chip.

- Left shifting in c is done via `<<` and right shifting is done via `>>`. `~` is used to invert the bits. In case we need to compare two integers, one with 16 and other with 32 bits.

- Blink
   ```c
   #include <lpc214x.h>

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

## Arduino uno programs

- Buzzer
   ```c
   // RM17 - RM9 connected 
   int buzzer_pin = 9;     // Arduino pin #23/D9  or Board pin P38

   void setup() 
   {
   pinMode(buzzer_pin, OUTPUT);
   Serial.begin(9600);
   digitalWrite(buzzer_pin,HIGH);
   }

   void loop() {
   digitalWrite(buzzer_pin, LOW);
   delay(1000);
   digitalWrite(buzzer_pin, HIGH);
   delay(1000);
   }
   ```

- LDR
   ```c
   int light_pin = 5;     //Arduino board pin #19 / D5

   void setup() {
   pinMode(light_pin, INPUT);
   Serial.begin(9600);
   }

   void loop() {
   int light_data = digitalRead(light_pin);
   if(light_data)
      Serial.println("Light Not Detected!");
   else
      Serial.println("Light Detected!");
      
   delay(1000);
   }
   ```
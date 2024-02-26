+++
title = 'Procedural programming in C'
date = 2024-02-26T11:43:27+05:30
tags = ["programming", "c", "procedural programming", "c++", "cpp", "c#", "compiler"]
author = "Aum Pauskar"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "A brief introduction to procedural programming in C"
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
    URL = "https://github.com/AumPauskar/blog/content/posts/"
    Text = "Suggest Changes"
    appendFilePath = true
+++

# Procedural programming in C

## About the tutorial
This tutorial is about procedural programming in C. We are going to use gcc within a linux environment to compile and run our programs. If you don't want to install any compilers on the computer, you can use an online compiler like [repl.it](https://repl.it/), or [onlinegdb](https://www.onlinegdb.com/online_c_compiler).

## Understanding the basics

### What is C?
C is a general-purpose, procedural computer programming language supporting structured programming, lexical variable scope, and recursion, with a static type system. By design, C provides constructs that map efficiently to typical machine instructions. It has found lasting use in applications previously coded in assembly language. Such applications include operating systems and various application software for computer architectures that range from supercomputers to PLCs and embedded systems.

### What is a compiler?
A compiler is a special program that translates source code written in a high-level programming language (like C, C++, C#, etc.) into machine code. The machine code is a set of instructions that can be executed directly by the CPU. The compiler is a part of the toolchain that includes a linker, assembler, and debugger.

### What is a procedural programming language?
Procedural programming is a programming paradigm, derived from structured programming, based on the concept of the procedure call. Procedures, also known as routines, subroutines, or functions, simply contain a series of computational steps to be carried out. Any given procedure might be called at any point during a program's execution, including by other procedures or itself.

### Installing C 
To install C on your computer, you need to install a C compiler. The most popular C compiler is gcc. You can install gcc on a linux system using the following command. Open a terminal and run the following commands:
```bash
sudo apt update
sudo apt upgrade -y
sudo apt install gcc
```

### Runnig a Hello World script
A hello world script is the first program that every programmer writes. It is a simple program that prints "Hello, World!" to the console. Here is the code for the hello world program in C:

```c
#include <stdio.h>
int main() {
    printf("Hello, World!\n");
    return 0;
}
```
To run the program, save the code in a file called `hello.c`. Open a terminal and navigate to the directory where the file is saved. Run the following command to compile the program:
```bash
gcc hello.c -o hello
```
This will create an executable file called `hello`. Run the program using the following command:
```bash
./hello
```

**About the program**
- The `#include <stdio.h>` line is a preprocessor directive that tells the compiler to include the standard input-output library in the program. This library contains the `printf` function that is used to print text to the console.
- The `int main()` line is the main function of the program. The program starts executing from the main function.
- The `printf("Hello, World!\n");` line is a function call that prints "Hello, World!" to the console.
- The `return 0;` line is the return statement of the main function. It returns 0 to the operating system, indicating that the program executed successfully.

## Datatypes and decaring variables in C

### Datatypes
C is a relatively low level language and is harware dependent. It has a rich set of datatypes that can be used to store different types of data. Here are some of the most commonly used datatypes in C:
- `int`: Used to store integer values.
- `float`: Used to store floating point values.
- `double`: Used to store double precision floating point values.
- `char`: Used to store single characters.
- `void`: Used to indicate that a function does not return any value.

There are different advantagnes of using different data types. For example, `int` is used to store integer values, `float` is used to store floating point values, `double` is used to store double precision floating point values, `char` is used to store single characters, and `void` is used to indicate that a function does not return any value.

### Variables
A variable is a name given to a memory location. It is used to store data. The value of a variable can be changed during the execution of the program. In C, you need to declare a variable before using it. Here is the syntax to declare a variable in C:
```c
datatype variable_name;
```
Here is an example of declaring variables in C:
```c
int age;
float height
```
Variables may also be declared and assigned values at the same time. Here is the syntax to declare and assign a value to a variable in C:
```c
datatype variable_name = value;
```

## Control structures in C
### If-else statement
The if-else statement is used to execute a block of code if a condition is true. If the condition is false, the code inside the else block is executed. Here is the syntax of the if-else statement in C:
```c
if (condition) {
    // code to be executed if the condition is true
} else {
    // code to be executed if the condition is false
}
```
Here is an example of using the if-else statement in C:
```c
int age = 20;
if (age >= 18) {
    printf("You are an adult\n");
} else {
    printf("You are a child\n");
}
```
### Switch statement
The switch statement is used to execute a block of code based on the value of a variable. Here is the syntax of the switch statement in C:
```c
switch (variable) {
    case value1:
        // code to be executed if the value of the variable is value1
        break;
    case value2:
        // code to be executed if the value of the variable is value2
        break;
    default:
        // code to be executed if the value of the variable does not match any of the cases
}
```
Here is an example of using the switch statement in C:
```c
char grade = 'A';
switch (grade) {
    case 'A':
        printf("Excellent\n");
        break;
    case 'B':
        printf("Good\n");
        break;
    case 'C':
        printf("Average\n");
        break;
    default:
        printf("Fail\n");
}
```
## Loops in C
### For loop
The for loop is used to execute a block of code a specified number of times. Here is the syntax of the for loop in C:
```c
for (initialization; condition; increment/decrement) {
    // code to be executed
}
```
Here is an example of using the for loop in C:
```c
for (int i = 0; i < 5; i++) {
    printf("%d\n", i);
}
```
### While loop
The while loop is used to execute a block of code as long as a condition is true. Here is the syntax of the while loop in C:
```c
while (condition) {
    // code to be executed
}
```
Here is an example of using the while loop in C:
```c
int i = 0;
while (i < 5) {
    printf("%d\n", i);
    i++;
}
```
### Do-while loop
The do-while loop is similar to the while loop, but the condition is checked after the block of code is executed. This means that the block of code is executed at least once. Here is the syntax of the do-while loop in C:
```c
do {
    // code to be executed
} while (condition);
```
Here is an example of using the do-while loop in C:
```c
int i = 0;
do {
    printf("%d\n", i);
    i++;
} while (i < 5);
```

### Loop control statements
Loop control statements change the execution of the loop. There are three loop control statements in C:
- `break`: The break statement is used to terminate the loop.
    syntax:
    ```c
    for (int i = 0; i < 5; i++) {
        if (i == 3) {
            break;
        }
        printf("%d\n", i);
    }
    ```
- `continue`: The continue statement is used to skip the rest of the code inside the loop and start the next iteration.
    syntax:
    ```c
    for (int i = 0; i < 5; i++) {
        if (i == 3) {
            continue;
        }
        printf("%d\n", i);
    }
    ```
- `goto`: The goto statement is used to jump to a specific label within the code.
    syntax:
    ```c
    for (int i = 0; i < 5; i++) {
        if (i == 3) {
            goto end;
        }
        printf("%d\n", i);
    }
    end:
    ```
## Functions in C
A function is a block of code that performs a specific task. It is a self-contained unit of code that can be called by other parts of the program. Here is the syntax of a function in C:
```c
return_type function_name(parameters) {
    // code to be executed
}
```
Here is an example of a function in C:
```c
int add(int a, int b) {
    return a + b;
}
```
The `int` before the function name is the return type of the function. The `add` is the name of the function. The `int a, int b` are the parameters of the function. The `return a + b` is the code to be executed by the function. The `return` statement is used to return a value from the function. The `int a, int b` are the parameters of the function. The `return a + b` is the code to be executed by the function. The `return` statement is used to return a value from the function.

### Types of functions
There are four types of functions in C:
- Functions with no arguments and no return value
    ```c
    void function_name() {
        // code to be executed
    }
    ```
- Functions with arguments and no return value
    ```c
    void function_name(int a, int b) {
        // code to be executed
    }
    ```
- Functions with no arguments and a return value
    ```c
    int function_name() {
        // code to be executed
        return value;
    }
    ```
- Functions with arguments and a return value
    ```c
    int function_name(int a, int b) {
        // code to be executed
        return value;
    }
    ```
### Function prototypes
A function prototype is a declaration of a function that tells the compiler about the function name, return type, and parameters. It is used to inform the compiler about the existence of the function. Here is the syntax of a function prototype in C:
```c
return_type function_name(parameters);
```
Here is an example of a function prototype in C:
```c
int add(int a, int b);
```
Function prototype in action:
```c
#include <stdio.h>
int add(int a, int b);
int main() {
    int sum = add(3, 5);
    printf("%d\n", sum);
    return 0;
}
int add(int a, int b) {
    return a + b;
}
```

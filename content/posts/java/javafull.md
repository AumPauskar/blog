+++
title = 'Javafull'
date = 2023-11-16T10:35:36+05:30
draft = false
+++

# Java tutorial
Java is a cross platform compiled language that uses jvm (java virtual machine) that can be used in any machine no matter the hardware or software, provided the machine supports jvm
## FYI
1. The object class is the root of all classes
2. Data can be gatered with the scanner method in the java library but cannot cater charecter type data with the standard library. Those can be gathered by sc = next().charat(0)
## Hello world
Code
```java
public class HelloWorld {

	public static void main(String[] args) {
		System.out.println("Hello World");
	}
}
```
In java you need to classify the class, the method inside the class and the print function in order to print a hello world program. \
To compile a java program you an use pre built methods in the code editors/IDE's or use following code in the terminal. Note: This is made in Linux, useage on other OS may differ. \
Compile method
```
cd "location of the file"
javac "nameofthefile.java"
java "classname"
```
Output
```
Hello World
```
The second method is to use extensions; VSCode provides the apt extensions to work in Java as in working in an IDE. To download it just go to the extensopns

### Keywords in hello world
1. public - the given function is available throughout the program
2. static - the java method can be called without the need to instansiate a class
3. void - returns no output
4. main - main class
5. class - class _classname_
6. println - prints a line with a newline charecter given below

### How a Java program is executed
Java is a compile time program and it is cross platform, unlike C which uses its compiler to convert the .c file into machine code, the Java compiler converts the given code to a byte code that is executed within the Java runtime environment or JRE. The JRE is supported on various platforms from servers to microcomputers. \
Java code -> byte code -> program gets executed

### Print methods
AS in total there are two printmethods in Java; there is the println version and the print version. The println version gets an empty line after the print statement where as the standard print version does not. However escape sequences do work on both the given cases.
## Basic info about Java

### Datatypes
Like C/C++ java needs variables to be declared in the code before executing anycode. \
These are the available data types in Java
1. boolean data type
2. byte data type (8-bit int -128, 127)
3. char data type
4. short data type (16-bit int -32768, 32767)
5. int data type (32-bit int -2147483648, 2147483647)
6. long data type (64-bit int -9223372036854775808, 9223372036854775807)
7. float data type
8. double data type

Note: Whenever a floating point datatype is used java always interprets it as a double datatype.

### Variables
The following is the syntax of declaring a variable in Java
```java
public class test {

	public static void main(String[] args) {
		int var1 = 5;
		char var2 = 'B';
		boolean var3 = true;
		long var4 = 456_789_324_456L;
		float var5 = 5.7F;

		System.out.println(var1);
		System.out.println(var2);
		System.out.println(var3);
		System.out.println(var4);
		System.out.println(var5);
	}
}
```
Output
```
5
B
true
456789324456
5.7
```
Once the data is initalised the value can be changed further in the program. Multiple variable can also be declared in the same line. \
A string should be enclosed in double brackets while a charecter is always enclosed in single brackets. In Java the default datatype for integer is always int, for storing longer numbers `long` must be used, however since Java automatically recognises it as a int a suffix of `L` may be applied. Similar case for having float, the default datatype for java for storing floating point datatype is `double` so a suffix of `F` may be added at the end of the data provided in the variable. As shown above large numbers can also be formatted like numbers in real life, insted of commas, numbers can be formatted by underscores, the Java compiler interprets them as standard numbers. \
Java has two type of datatypes in broad classifiction.
1. Primative datatypes
2. Reference datatypes

Java has the following primative datatypes
| Datatype | Description |
| ---------- | ---------- |
| boolean | stores true/false value |
| byte | stores an 8 bit int |
| char | stores a charecter |
| double | stores a decimal datatype (high precision) |
| float | stores a decimal datatype (low precision) |
| int | stores a 32 bit int |
| long | stores a 64 bit int |
| short | stores a 32 bit int |
Primitive datatypes are shown above where are reference datatyped are based on either prebuilt or user generated classes, an example is given below
```java
import java.util.Date;
public class test {

	public static void main(String[] args) {
		Date now = new Date();
		System.out.println(now);
	}
}
```
Output
```
Tue Oct 25 18:32:31 IST 2022
```
Here the util. Date module is imported from the Java library to initiate the Date class. The new operator here dynamically allocates the memory and hence gives data to the variable.

### Type casting
In some scenarios the datatype of the variable is needed to be changes to another variable, this is called as type casting.
```java
public class test {

	public static void main(String[] args) {
		double a = 5, b = 3;
		
		// here a double value (a/b) is getting converted to a int value
		// which is again assing to the int output datatype
		int output = (int) (a/b); 
		System.out.println(output);
	}
}
```
Output
```
1
```
### Strings
Strings are the reference datatypes wherein it is an array of charecters. A string in Java is created by defining it by `String` before the name of the variable. \
Similar like python, Java supports string formating with the help of the addition operator. Like C, strings in Java have to be contained with double quotes where as charecters in Java have to be contained in single quotes. 

### Escape sequences
A simple print function has limitations of what it can and what it connot print, in some cases some charecters might not get printed since they are reserved in the programming syntax like the new line ASCII charecter. To overcome this escape sequences are used wherein the all the ASCII operations can be performed by the use of the given combinaion of symbols.

| Escape sequences | Description |
| ---------- | ---------- |
| \' | Single quote |
| \" | Double quote |
| \\ | Backslash |
| \r | Carriage return |
| \n | Newline |
| \f | Form feed |
| \t | Horizontal tab |
| \b | Backspace |
| \ddd | Octal constant (ddd) |
| \uxxxx | Hexadecimal constant (xxxx) |

### Taking input from the user
There are two major ways the program can take input from the user.
Method 1 - Use builtin function
```java
public class test {

	public static void main(String[] args)
		throws java.io.IOException {
		char val;
		System.out.print("Enter a charecter: ");
		val = (char) System.in.read();
		System.out.println("The given charecter is: " + val);
		
	}
}
```
Output
```
Enter a charecter: a
The given charecter is: a
```
Method 2 - Use scanner class
```java
import java.util.Scanner;
public class test {
	public static void main(String[] args) {
		// defining a object of scanner class
		Scanner scanObj = new Scanner(System.in);
		System.out.print("Enter num 1: ");
		// using the scanObj object to scan both numbers
		int num1 = scanObj.nextInt();
		System.out.print("Enter num 2: ");
		int num2 = scanObj.nextInt();
		System.out.println("The sum is: " + (num1+num2));
		// extra
		scanObj.close();
	}
}
```
Output
```
Enter num 1: 4
Enter num 2: 5
The sum is: 9
```
Its always a good practice to close the scanner object in this case it was `scanObj` using the scanObj.close() method.
### Comments

```java
// This is a line of comment

/*
where as
this is
a block
of comment
*/
```

## Logical control

### The if-else statement
The user can control the flow of the program with the help of if-else statements. \
Here is a code in action.
```java
class test {
	public static void main(String args[]) {
		int var1 = 5;
		if (var1%2 == 0) {
			System.out.println("The number is even");
		} else if (var1%2 == 1) {
			System.out.println("The number is odd");
		} else {
			System.out.println("Error");
		}
	}
}
```
Output
```
The number is odd
```

### Switch statements
A switch statement is a multiway Java logical operator. Succeding versions after Java 7 will also support strings as the condition. A break statement must be added after every case statement so that the program stops and does not executes all the sucessive statements. A default keyword can be added if the user wants to specify when and where the code must stop.
```java
import java.util.Scanner;;
public class test {

	public static void main(String[] args) {
		Scanner scanObj = new Scanner(System.in);
		System.out.print("Enter a number (1-7): ");
		byte option = scanObj.nextByte();
		switch (option) {
			case 1: System.out.println("Monday");
			break;
			case 2: System.out.println("Tuesday");
			break;
			case 3: System.out.println("Wednesday");
			break;
			case 4: System.out.println("Thrusday");
			break;
			case 5: System.out.println("Friday");
			break;
			case 6: System.out.println("Saturday");
			break;
			case 7: System.out.println("Sunday");
			break;
			default: System.out.println("Invalid statement");
		}

	}
}
```
Output 1
```
Enter a number (1-7): 2
Tuesday
```
Output 2
```
Enter a number (1-7): 22
Invalid statement
```
### Ternary operators

The following program can also be performed with the help of ternary operators.
```java
class test {
	public static void main(String[] args) {
		int var1 = 5;
		System.out.println((var1/2 == 0) ? ("The number is even") : ("The number is odd"));
	}
}
```
Output
```
The number is odd
```
### Strings as an exception
Two strings cannot be compared using the `==` operator as they are a derived data type. Here is how you compare two strings.
```
```
## Loops

There are three types of loops in Java and they are namely the
1. for loop
2. while loop
3. do-while loop \
The for loop and the while loop are entry-controlled loop where as the do-while loop is exit controlled loop.
### For loop
Syntax for for loop
```java
public class test {

	public static void main(String[] args) {
		for(int i=1; i<=10; i++) {
			System.out.println("5 x " + i + " = " + 5*i);
		}
	}
}
```
Output
```
5 x 1 = 5
5 x 2 = 10
5 x 3 = 15
5 x 4 = 20
5 x 5 = 25
5 x 6 = 30
5 x 7 = 35
5 x 8 = 40
5 x 9 = 45
5 x 10 = 50
```
A for loop can also be initialised in an infinite manner with the following template
```java
for (;;) {
	// infinite code
}
```
### While loop
Syntax for while loop
```java
public class test {

	public static void main(String[] args) {
		int i = 0;
		while (i<10) {
			i++;
			System.out.print(i + ",");
		}
	}
}
```
Output
```
1,2,3,4,5,6,7,8,9,10,%
```
### Do-while

Syntax for do-while loop
```java
public class test {

	public static void main(String[] args) {
		int i = 0;
		do {
			i++;
			System.out.print(i + ",");
		} while(i<10);
	}
}
```

```
Output
1,2,3,4,5,6,7,8,9,10,%
```

### For each loop
Now this is not a complety distinctive style of loop fowever its just an extension of a standard for loop. For each loop cycles through an array till the array gets completed.
```java
package test;

public class jarjar {

	public static void main(String[] args) {
		int[] arr = {1,2,3,4,5,6,7,8,9,0};
		for (int i : arr) {
			System.out.print(i);
		}
	}
}
```
Output
```
1234567890%
```
### Break statements
A break statement can also be initialised within a loop to exit a loop whenever a condition is met.
```
public class test {
	public static void main(String[] args) {
		int val = 0;
		while (true) {
			val++;
			if (val == 6) {
				break;
			} else {
				System.out.println(val);
			}
		}
	}
}
```
Output
```
1
2
3
4
5
```
### Continue statements
The continue statemtnt tells the loop in the code to execute again making the code within the loop below the continue statemtnt irrelavant if the condiiton is met
```java
public class test {
	public static void main(String[] args) {
		int val = 0;
		while (true) {
			val++;
			if (val % 2 == 0) {
				continue;
			}
			// the continue statemnt forces the program to redo the
			// loop if the condition is met
			System.out.println(val);


			// useage of break statement
			if (val >= 10) {
				break;
			}
		}
	}
}
```
Output
```
1
3
5
7
9
11
```

## Datatypes

### Arrays
A array is a one dimentional complex data type which can store one type of data inside it. In Java the arrays are stored as an object and should be used with object functions to interact.
Given below is a program of how to scan and print two arrays. Note that none of the packages are required to interact with the array, however these are requited to do system input and printing the array. The individual elements can be accessed with the array indexing starting from 0 to the last-1 element of the array.

```java
package test;
import java.util.Arrays;
import java.util.Scanner;

public class jarjar {

	public static void main(String[] args) {
		// declaring an array
		int[] arr = new int[10];
		// declaring and defining the array
		int[] arr2 = {1,2,3,4,5,6,7,8,9,10};
		System.out.println(Arrays.toString(arr2));
		Scanner in = new Scanner(System.in);
		for (int i = 0; i < 10; i++) {
			arr[i] = in.nextInt();
		}
		in.close();
		System.out.println(Arrays.toString(arr));

	}
}
```
Output
```
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
0 9 8 7 6 5 4 3 2 1 
[0, 9, 8, 7, 6, 5, 4, 3, 2, 1]
```

### Multidimentional array
Multidimentional array are similar to the linear array the only difference being its an array inside another array, since its just a compound array all the features of the regalar array functions are applicable here also.
```java
package test;
import java.util.Arrays;
import java.util.Scanner;

public class jarjar {

	public static void main(String[] args) {
		int i;
		int[][] arr2D = new int[3][3];
		Scanner in = new Scanner(System.in);
		for (i=0; i<3; i++) {
			for (int j=0; j<3; j++) {
				System.out.print("Enter value ["+i+"]["+j+"] :");
				arr2D[i][j] = in.nextInt();
			}
		}
		in.close();
		for (i=0; i<3; i++) {
			System.out.println(Arrays.toString(arr2D[i]));
		}
	}
}
```
Output
```
Enter value [0][0] :1
Enter value [0][1] :2
Enter value [0][2] :3
Enter value [1][0] :4
Enter value [1][1] :5
Enter value [1][2] :6
Enter value [2][0] :7
Enter value [2][1] :8
Enter value [2][2] :9
[1, 2, 3]
[4, 5, 6]
[7, 8, 9]
```

### Misc functions in the array
1. length - the arrayName.length function returns an integer value of the array length whenever its called
## Error handling
If an error is occuring inside the program and the programmer wants the error to be handled gracefully error handling must be implementd. To do this a try-catch method is used. \
Here is the syntax on how to catch errors

// error catching to be written

## Garbage collection
Unlike the OG of high level programming language like C or C++ java is equipped with a much more advanced automated garbage collecion which removes unwanted java variables when not in use.

## String comparision
The string compare method can be used to compare two given strings, when both the strings are same the inbuilt function returns a 0 with a -ve or +ve number being returned if the two strings are not matching.


## Working with classes
Working with classes or as its commonly known as object oriented programming is a method of programming where the program is built with classes which are just charecterisation of a much more complex data type with the inclusion of functions.

Things to know before attempting OOPS in Java
1. Only the main function should contain th public attribute
2. The package must be defined for inclusion of more than one class (including the main)

What are we going to do? \
Here we have made a folder called `test` which contains a java file `jarjar.java`, hence in order to achive the output install Java 1.17 + make the same folder structure.

### Basics of class
```java
// a package of the foldername should be used
package test;

// child class should not have public attribute
class vehicle {
	// class members
	int cyl;
	String name;
	
}

// parent/main class must have the public attribute
public class jarjar {

	public static void main(String[] args) {
		// creating a new object
		vehicle car1 = new vehicle();
		// accessing class members
		car1.cyl = 5;
		car1.name = "Kuruma";
		System.out.println(car1.cyl);
		System.out.println(car1.name);
	}
}
```
### Constructors
```java
package test;

class Vehicle {
	int cyl;
	double bore;
	double stroke;
	int power;
	String engineType;

	// an example of a paramatrised constructor
	// this can be used to direct the variable
	Vehicle (int var) {
		this.power = var;
	}
	double giveDisplacement() {
		return cyl*bore*stroke;
	}
	
}

public class jarjar {

	public static void main(String[] args) {
		// creating a new object
		Vehicle car1 = new Vehicle(420);
		// accessing class members
		car1.cyl = 5;
		car1.engineType = "V6";
		System.out.println(car1.cyl);
		System.out.println(car1.power);
		System.out.println(car1.engineType);
	}
}
```
Output
```
4005.0
37
```
Note: The `this` keyword can be used to direct the variable in the current class scope and not be declared globally.

### Passing objects as parameters
The following code demonstrated how passing of objects as parameters works, the code also shows how method overloading/function overloading/constructor overloading. 
```java
package test;


/**
 * v8
 */
class v8 {
	String engine = "v8";
	int cyl = 8;
	int power = 400;
	double volume = 5.0;

	v8(int power, float volume) {
		this.power = power;
		this.volume = volume;
		System.out.println(power + "" + volume);
	}

	v8() {
		this.power = 400;
		this.volume = 5.0;
		System.out.println(power + "" + volume);
	}

	// recieved said argument 
	void powerPerCyl(int power, v8 object) {
		int output = power / object.cyl;
		System.out.println(output);
	}
	
}
public class jarjar {
	public static void main(String[] args) {
		v8 engine1 = new v8();
		// passed argemnt as an object
		engine1.powerPerCyl(300, engine1);
	}
}
```

### Static methods
Static methods are called independent of the object and make a standalone function. 
```java
package test;

class v8 {
	String engine = "v8";
	int cyl = 8;
	int power = 400;
	double volume = 5.0;


	// recieved said argument 
	static double powerPerCyl(int power, int cyl) {
		double output = power / cyl;
		return output;
	}
	
}
public class jarjar {
	public static void main(String[] args) {
		System.out.println(v8.powerPerCyl(420, 8));
	}
}
```
Output
```
52.0
```

### Inheritance
Inheritance in programming languages refers to getting all the properties of the parent function plus some more extras.
Note: Multiple inheritance in not supported in Java, however is supported using interfaces.
```java
package test;

class v8 {
	String engine = "v8";
	int cyl = 8;
	int power = 400;
	double volume = 5.0;

	double powerPerCyl(int power, int cyl) {
		double output = power / cyl;
		return output;
	}	
}

// F1 engine	-> v8
// child class	-> parent class
class F1Engine extends v8 {
	int rpm = 18000;
	int angle = 90;

	void printVol() {
		System.out.println(rpm + " " + angle + " " + power);
	}
}
public class jarjar {
	public static void main(String[] args) {
		v8 eng1 = new v8();
		F1Engine eng2 = new F1Engine();

		System.out.println(eng1.power);
		eng2.printVol();
	}
}
```
Output
```
400
18000 90 400
```

### Super builtin function
The super function calls the parent class constructor from the child class. The super function must always lie before any other statements in the child class constructor.

- Super to access constructor
```java
package test;

class v8 {
	String engine = "v8";
	int cyl = 8;
	int power = 400;
	double volume = 5.0;

	v8() {
		System.out.println(engine + " " + cyl + " " + power + " " + volume);
	}

	double powerPerCyl(int power, int cyl) {
		double output = power / cyl;
		return output;
	}	
}

class F1Engine extends v8 {
	int rpm = 18000;
	int angle = 90;

	void printVol() {
		System.out.println(rpm + " " + angle + " " + power);
	}

	F1Engine() {
		// super must always be the first statement
		super();
		System.out.println(rpm + " " + angle);
		// calling the super class
	}
}
public class jarjar {
	public static void main(String[] args) {
		v8 eng1 = new v8();
		F1Engine eng2 = new F1Engine();

		System.out.println(eng1.power);
		eng2.printVol();
	}
}
```
Output
```
v8 8 400 5.0
v8 8 400 5.0
18000 90
400
18000 90 400
```

- Super in acessing values of parent class
```java
package test;

class v8 {
	String engine = "v8";
	int cyl = 8;
	int power = 400;
	double volume = 5.0;

	double powerPerCyl(int power, int cyl) {
		double output = power / cyl;
		return output;
	}	
}

class F1Engine extends v8 {
	int rpm = 18000;
	int angle = 90;
	int power = 750;

	F1Engine() {
		System.out.println("Power in regular v8: " + super.power);
		System.out.println("Power in F1 v8: " + power);
	}
}
public class jarjar {
	public static void main(String[] args) {
		F1Engine eng2 = new F1Engine();

	}
}
```
Output
```
Power in regular v8: 400
Power in F1 v8: 750
```
### Abstract classes
Abstract classes are those chasses which contain abstract methods

1. An abstract class must be declared with an abstract keyword.
2. It can have abstract and non-abstract methods.
3. It cannot be instantiated.
4. It can have constructors and static methods also.
5. It can have final methods which will force the subclass not to change the body of the method. \
An abstract class is a subset of normal classes where only the bare minimum is implemented.

```java
package test;

abstract class v8 {
	String engine;
	int cyl;
	int power;
	double volume;
	double powerPerCyl(int power, int cyl) {
		double output = power / cyl;
		return output;
	}	
}

class F1Engine extends v8 {
	int rpm = 18000;
	int angle = 90;
	int power = 750;

	F1Engine() {
		System.out.println("Power in regular v8: " + super.power);
		System.out.println("Power in F1 v8: " + power);
	}
}
public class jarjar {
	public static void main(String[] args) {
		F1Engine eng2 = new F1Engine();

	}
}
```
Output
```
Power in regular v8: 0
Power in F1 v8: 750
```

#### Abstract methods
Abstract methods are those methods housed inside the classes which dont have any implementation or we can say "A method declared using the abstract keyword within an abstract class and does not have a definition".

The syntax for abstract methods is as follows:
```
abstract return_type method_name( [ argument-list ] );  
```
### Interfaces
Within an abstract class we can still have normal non-abstract methods, with the use of interfaces we can completely remove the need of solid methods

### Exception handling
Managing execptions or code errors in java can be handled in a more customizable way with the use of exception handling

- Components of try catch
1. try - asks the code to execute and argument and hope it doesn't spit out an error
2. catch - handles the error in a user defined way
3. finally - the final block in the code which gets executed no matter what

- Throw
The try catch is a system defined error handling snippet, with the throw keyword the user can customize the exception handling without an external library. \
The throw exception works with tandem with the try, catch, finally.

An example of try catch can be found below
```java
package test;
import java.util.Scanner;
public class jarjar {

	public static void main(String[] args) {
		Scanner scanInput = new Scanner(System.in);
		double a, b, ans;
		try {
			System.out.print("Enter divident: ");
			a = scanInput.nextInt();
			System.out.print("Enter divisor: ");
			b = scanInput.nextInt();
			scanInput.close();
			ans = a/b;
			System.out.println("Answer: " + ans);
		} catch (Exception e) {
			System.out.println("Invalid input");
		}
	}
}
```

This can be further be changed into a custom error with the use of `throw` keyword. The syntax can be simplified into being as `throw new error` as seen in termwork 8.

packages
In Java, a package is a way to organize and structure code. A package is a collection of related classes, interfaces, and other resources that are bundled together. Packages are used to group similar classes and interfaces, and to provide a unique namespace for them. This helps to prevent naming conflicts and makes it easier to maintain and reuse code.

Packages in Java are created using the package keyword, followed by the package name. For example:
```
package com.example.mypackage;
```
This creates a package named mypackage in the com.example namespace.

To use a class or interface from a package, you must import it using the import keyword. For example:
```
import java.util.List;
```
This imports the List interface from the java.util package.

It's also possible to use the * wildcard to import all the classes and interfaces from a package. For example:
```
import java.util.*;
```
This imports all the classes and interfaces from the java.util package.

Java has a set of built-in packages, known as the Java API, which provide a wide range of functionality for common tasks such as working with strings, lists, and dates. Additionally, developers can create their own custom packages.

It's a good practice to group related classes and interfaces in packages, and to use appropriate package names that reflect the functionality of the classes and interfaces. This makes it easy to understand the purpose of the package and how to use the classes and interfaces it contains.
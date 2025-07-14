+++
title = 'C# Basics'
date = 2025-07-12T12:40:13+07:00
tags = ["c#", "programming", "oops"]
author = "Aum Pauskar"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "A brief overview of C# basics, including syntax, data types, and object-oriented programming concepts."
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

# C# Basics

C# is a versatile programming language developed by Microsoft, widely used for building a variety of applications, from web to desktop and mobile. This post covers the basics of C#, including syntax, data types, and object-oriented programming concepts. Dotnet is a framework that supports C# and provides a rich set of libraries and tools for developers.

## Console commands
C# can be extended a lot by using the dotnet CLI here are some examples of the .net CLI commands.

The .NET CLI (Command-Line Interface) is a powerful tool for developing, building, running, and managing .NET applications. Here’s a concise overview of some commonly used .NET CLI commands:

- Basic commands

    1. **`dotnet new`**: Creates a new project or solution based on a specified template.
        - Example: `dotnet new console` (creates a new console application)

    2. **`dotnet build`**: Builds the project and its dependencies.
        - Example: `dotnet build` (builds the current project)

    3. **`dotnet run`**: Runs the application.
        - Example: `dotnet run` (runs the current project)

    4. **`dotnet restore`**: Restores the dependencies and tools of a project.
        - Example: `dotnet restore` (restores packages for the current project)

    5. **`dotnet publish`**: Packs the application and its dependencies into a folder for deployment.
        - Example: `dotnet publish -c Release` (publishes the project in Release configuration)

- Project Management

    6. **`dotnet add package`**: Adds a NuGet package to the project.
        - Example: `dotnet add package Newtonsoft.Json` (adds the Newtonsoft.Json package)

    7. **`dotnet remove package`**: Removes a NuGet package from the project.
        - Example: `dotnet remove package Newtonsoft.Json` (removes the Newtonsoft.Json package)

    8. **`dotnet list package`**: Lists the packages referenced by the project.
        - Example: `dotnet list package` (lists all packages in the current project)

- Solution Management

    9. **`dotnet sln`**: Manages solutions.
        - Example: `dotnet sln add MyProject.csproj` (adds a project to the solution)

    10. **`dotnet sln remove`**: Removes a project from the solution.
        - Example: `dotnet sln remove MyProject.csproj` (removes a project from the solution)

- Testing

    11. **`dotnet test`**: Runs unit tests in the project.
        - Example: `dotnet test` (runs tests in the current project)

- Global Tools

    12. **`dotnet tool install`**: Installs a .NET global tool.
        - Example: `dotnet tool install -g dotnet-ef` (installs the Entity Framework Core CLI tool globally)

    13. **`dotnet tool update`**: Updates a .NET global tool.
        - Example: `dotnet tool update -g dotnet-ef` (updates the Entity Framework Core CLI tool)

    14. **`dotnet tool list`**: Lists installed global tools.
        - Example: `dotnet tool list -g` (lists all globally installed tools)

- Help and Information

    15. **`dotnet --info`**: Displays information about the .NET SDK and runtime installed on the machine.
        - Example: `dotnet --info`

    16. **`dotnet help`**: Displays help information for the .NET CLI.
        - Example: `dotnet help` or `dotnet <command> --help` (provides help for a specific command)

## Syntax
C# syntax is similar to other C-style languages like Java and C++. Here are some basic elements:
- **Variables**: Declared with a type followed by the variable name.
    ```csharp
    int age = 30;
    string name = "Aum";
    ```
- **Data Types**: C# has several built-in data types, including:
    - `int`: Represents integer values.
    - `double`: Represents floating-point numbers.
    - `bool`: Represents boolean values (`true` or `false`).
    - `string`: Represents a sequence of characters.
- **Control Structures**: C# supports various control structures, such as:
    - **If statements**: Used for conditional execution.
    - **For loops**: Used for iterating over a range of values.
    - **Switch statements**: Used for selecting one of many code blocks to execute.

- **Functions**: Defined using the `void` keyword for functions that do not return a value, or with a specific return type.
    ```csharp
    void Greet(string name) {
        Console.WriteLine($"Hello, {name}!");
    }
    ```

- **Classes and Objects**: C# is an object-oriented language, allowing you to define classes and create objects.
    ```csharp

    class Person {
        public string Name { get; set; }
        public int Age { get; set; }

        public void Introduce() {
            Console.WriteLine($"My name is {Name} and I am {Age} years old.");
        }
    }

    Person person = new Person();
    person.Name = "Aum";
    person.Age = 30;
    person.Introduce();
    ```

## Preprocessor Directives
C# supports preprocessor directives, which are commands that are processed before the compilation of the code
- **Using Directives**: Used to include namespaces in your code.
    ```csharp
    using System;
    ```
- **Conditional Compilation**: Allows you to include or exclude code based on certain conditions.
    ```csharp
    #if DEBUG
    Console.WriteLine("Debug mode is enabled.");
    #endif
    ```

## Basic IO statements
C# provides several methods for input and output operations:
- **Console Input/Output**: The `Console` class provides methods for reading from and
writing to the console.
    ```csharp
    Console.WriteLine("Enter your name:");
    string name = Console.ReadLine();
    Console.WriteLine($"Hello, {name}!");
    ```

    - **Taking in a number**: You can read a number from the console and convert it to an integer.
    ```csharp
    Console.WriteLine("Enter your age:");
    string input = Console.ReadLine();
    int age;
    if (int.TryParse(input, out age)) {
        Console.WriteLine($"You are {age} years old.");
    } else {
        Console.WriteLine("Invalid input. Please enter a valid number.");
    }
    ```

## Datatypes

C# is a statically typed language, which means that the type of a variable is known at compile time. C# provides a rich set of built-in data types, which can be categorized into two main groups: **Value Types** and **Reference Types**. Below is a detailed look at these data types.

- 1. Integral Types
    - a. `int`
        - **Definition and Range**: Represents a 32-bit signed integer. Range: -2,147,483,648 to 2,147,483,647.
        - **Snippet**:
        ```csharp
        int myInt = 42;
        ```

    - b. `long`
        - **Definition and Range**: Represents a 64-bit signed integer. Range: -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807.
        - **Snippet**:
        ```csharp
        long myLong = 12345678901234L;
        ```

    - c. `short`
        - **Definition and Range**: Represents a 16-bit signed integer. Range: -32,768 to 32,767.
        - **Snippet**:
        ```csharp
        short myShort = 32000;
        ```

    - d. `byte`
        - **Definition and Range**: Represents an 8-bit unsigned integer. Range: 0 to 255.
        - **Snippet**:
        ```csharp
        byte myByte = 255;
        ```

    - e. `sbyte`
        - **Definition and Range**: Represents an 8-bit signed integer. Range: -128 to 127.
        - **Snippet**:
        ```csharp
        sbyte mySByte = -128;
        ```

    - f. `uint`
        - **Definition and Range**: Represents a 32-bit unsigned integer. Range: 0 to 4,294,967,295.
        - **Snippet**:
        ```csharp
        uint myUInt = 4000000000U;
        ```

    - g. `ulong`
        - **Definition and Range**: Represents a 64-bit unsigned integer. Range: 0 to 18,446,744,073,709,551,615.
        - **Snippet**:
        ```csharp
        ulong myULong = 8000000000000000000UL;
        ```

    - h. `ushort`
        - **Definition and Range**: Represents a 16-bit unsigned integer. Range: 0 to 65,535.
        - **Snippet**:
        ```csharp
        ushort myUShort = 65000;
        ```

- 2. Floating-Point Types

    - a. `float`
        - **Definition and Range**: Represents a single-precision (32-bit) floating-point number. Range: ±1.5 × 10^−45 to ±3.4 × 10^38.
        - **Snippet**:
        ```csharp
        float myFloat = 3.14f;
        ```

    - b. `double`
        - **Definition and Range**: Represents a double-precision (64-bit) floating-point number. Range: ±5.0 × 10^−324 to ±1.7 × 10^308.
        - **Snippet**:
        ```csharp
        double myDouble = 3.14159265358979;
        ```

    - c. `decimal`
        - **Definition and Range**: Represents a 128-bit precise decimal value with 28-29 significant digits. Range: ±1.0 × 10^−28 to ±7.9 × 10^28.
        - **Snippet**:
        ```csharp
        decimal myDecimal = 19.99m;
        ```

- 3. Other Value Types

    - a. `char`
        - **Definition and Range**: Represents a single 16-bit Unicode character. Range: U+0000 to U+FFFF.
        - **Snippet**:
        ```csharp
        char myChar = 'A';
        ```

    - b. `bool`
        - **Definition and Range**: Represents a Boolean value (true or false).
        - **Snippet**:
        ```csharp
        bool myBool = true;
        ```

- 4. Reference Types

    - a. `string`
        - **Definition**: Represents a sequence of characters. Strings are immutable.
        - **Snippet**:
        ```csharp
        string myString = "Hello, World!";
        ```
    - b. Array
        - **Definition**: A collection of items of the same type. Can be single-dimensional or multi-dimensional.
        - **Snippet**:
        ```csharp
        int[] myArray = new int[5] { 1, 2, 3, 4, 5 };
        ```

    - c. Class
        - **Definition**: A user-defined reference type that can contain data members (fields) and function members (methods).
        - **Snippet**:
        ```csharp
        class Person {
            public string Name;
            public int Age;
        }
        ```

    - d. Interface
        - **Definition**: A contract that defines a set of methods and properties that implementing classes must provide.
        - **Snippet**:
        ```csharp
        interface IAnimal {
            void Speak();
        }
        ```

    - e. Delegate
        - **Definition**: A type that represents references to methods with a specific parameter list and return type.
        - **Snippet**:
        ```csharp
        public delegate void Notify();
        ```

    - f. `object`
        - **Definition**: The base type from which all other types derive. Can hold any data type.
        - **Snippet**:
        ```csharp
        object myObject = "This is an object";
        ```

- 5. Nullable Types

    - a. `int?`
        - **Definition**: A nullable integer that can represent all the values of its underlying type plus an additional `null` value.
        - **Snippet**:
        ```csharp
        int? myNullableInt = null;
        ```

- 6. Enumerations

    - a. `enum`
        - **Definition**: A special "class" that represents a group of constants (named values).
        - **Snippet**:
        ```csharp
        enum Days { Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday }
        ```

## Logical statements

Logical statements or conditions help the flow of the code that is running within the program. Here are the examples of some logical statements that are in C#

- 1. Logical Operators

    - a. `&&` (Logical AND)
        - **Definition**: Returns `true` if both operands are true; otherwise, it returns `false`.
        - **Snippet**:
        ```csharp
        bool a = true;
        bool b = false;
        bool result = a && b; // result is false
        ```

    - b. `||` (Logical OR)
        - **Definition**: Returns `true` if at least one of the operands is true; returns `false` if both are false.
        - **Snippet**:
        ```csharp
        bool a = true;
        bool b = false;
        bool result = a || b; // result is true
        ```

    - c. `!` (Logical NOT)
        - **Definition**: Reverses the logical state of its operand. If the condition is true, it becomes false, and vice versa.
        - **Snippet**:
        ```csharp
        bool a = true;
        bool result = !a; // result is false
        ```

- 2. Conditional Statements

    - a. `if` Statement
        - **Definition**: Executes a block of code if the specified condition is true.
        - **Snippet**:
        ```csharp
        int number = 10;
        if (number > 0) {
            Console.WriteLine("Number is positive.");
        }
        ```

    - b. `else` Statement
        - **Definition**: Executes a block of code if the condition in the `if` statement is false.
        - **Snippet**:
        ```csharp
        int number = -5;
        if (number > 0) {
            Console.WriteLine("Number is positive.");
        } else {
            Console.WriteLine("Number is not positive.");
        }
        ```

    - c. `else if` Statement
        - **Definition**: Specifies a new condition to test if the first condition is false.
        - **Snippet**:
        ```csharp
        int number = 0;
        if (number > 0) {
            Console.WriteLine("Number is positive.");
        } else if (number < 0) {
            Console.WriteLine("Number is negative.");
        } else {
            Console.WriteLine("Number is zero.");
        }
        ```

- 3. Switch Statement

    - a. `switch`
        - **Definition**: Selects one of many code blocks to execute based on the value of a variable or expression.
        - **Snippet**:
        ```csharp
        int day = 3;
        switch (day) {
            case 1:
                Console.WriteLine("Monday");
                break;
            case 2:
                Console.WriteLine("Tuesday");
                break;
            case 3:
                Console.WriteLine("Wednesday");
                break;
            default:
                Console.WriteLine("Invalid day");
                break;
        }
        ```

- 4. Ternary Operator

    - a. `?:` (Ternary Conditional Operator)
        - **Definition**: A shorthand for `if-else` statements that returns one of two values based on a condition.
        - **Snippet**:
        ```csharp
        int number = 10;
        string result = (number > 0) ? "Positive" : "Non-positive"; // result is "Positive"
        ```

## Data structures in C#

- 1. Arrays

    - **Definition**: A collection of items of the same type, stored in contiguous memory locations. Arrays can be single-dimensional or multi-dimensional.
    - **Snippet**:
    ```csharp
    int[] myArray = new int[5] { 1, 2, 3, 4, 5 }; // Single-dimensional array
    ```

- 2. Lists

    - **Definition**: A dynamic array that can grow and shrink in size. It is part of the `System.Collections.Generic` namespace and provides methods for adding, removing, and searching for elements.
    - **Snippet**:
    ```csharp
    using System.Collections.Generic;

    List<int> myList = new List<int>();
    myList.Add(1);
    myList.Add(2);
    myList.Add(3);
    ```

- 3. Dictionaries

    - **Definition**: A collection of key-value pairs, where each key is unique. It allows for fast lookups based on keys. It is also part of the `System.Collections.Generic` namespace.
    - **Snippet**:
    ```csharp
    using System.Collections.Generic;

    Dictionary<string, int> myDictionary = new Dictionary<string, int>();
    myDictionary.Add("Alice", 30);
    myDictionary.Add("Bob", 25);
    ```

- 4. HashSet

    - **Definition**: A collection of unique elements that provides high-performance set operations. It does not allow duplicate values and is part of the `System.Collections.Generic` namespace.
    - **Snippet**:
    ```csharp
    using System.Collections.Generic;

    HashSet<int> myHashSet = new HashSet<int>();
    myHashSet.Add(1);
    myHashSet.Add(2);
    myHashSet.Add(2); // Duplicate, will not be added
    ```

- 5. Queue

    - **Definition**: A first-in, first-out (FIFO) collection of objects. It is part of the `System.Collections.Generic` namespace and provides methods for adding and removing elements.
    - **Snippet**:
    ```csharp
    using System.Collections.Generic;

    Queue<string> myQueue = new Queue<string>();
    myQueue.Enqueue("First");
    myQueue.Enqueue("Second");
    string first = myQueue.Dequeue(); // Removes "First"
    ```

- 6. Stack

    - **Definition**: A last-in, first-out (LIFO) collection of objects. It allows adding and removing elements from the top of the stack.
    - **Snippet**:
    ```csharp
    using System.Collections.Generic;

    Stack<string> myStack = new Stack<string>();
    myStack.Push("First");
    myStack.Push("Second");
    string last = myStack.Pop(); // Removes "Second"
    ```

- 7. LinkedList

    - **Definition**: A doubly linked list that allows for efficient insertions and deletions. It is part of the `System.Collections.Generic` namespace.
    - **Snippet**:
    ```csharp
    using System.Collections.Generic;

    LinkedList<string> myLinkedList = new LinkedList<string>();
    myLinkedList.AddLast("First");
    myLinkedList.AddLast("Second");
    myLinkedList.AddFirst("Zero"); // Adds "Zero" at the beginning
    ```

- 8. Tuple

    - **Definition**: A data structure that can hold a fixed number of items of different types. It is useful for returning multiple values from a method.
    - **Snippet**:
    ```csharp
    var myTuple = Tuple.Create(1, "Alice", 30); // Tuple with an int, string, and int
    ```

- 9. ArrayList

    - **Definition**: A non-generic collection that can hold items of any type. It is part of the `System.Collections` namespace and is less type-safe than generic collections.
    - **Snippet**:
    ```csharp
    using System.Collections;

    ArrayList myArrayList = new ArrayList();
    myArrayList.Add(1);
    myArrayList.Add("Hello");
    ```

## String functions in C#

The following are some of the string functions in C#. 
- 1. `Length`
    - **Definition**: Gets the number of characters in the string.
    - **Snippet**:
    ```csharp
    string myString = "Hello, World!";
    int length = myString.Length; // length is 13
    ```

- 2. `Substring`
    - **Definition**: Returns a substring from the string, starting at a specified index and optionally for a specified length.
    - **Snippet**:
    ```csharp
    string myString = "Hello, World!";
    string sub = myString.Substring(7, 5); // sub is "World"
    ```

- 3. `IndexOf`
    - **Definition**: Returns the zero-based index of the first occurrence of a specified substring. Returns -1 if not found.
    - **Snippet**:
    ```csharp
    string myString = "Hello, World!";
    int index = myString.IndexOf("World"); // index is 7
    ```

- 4. `LastIndexOf`
    - **Definition**: Returns the zero-based index of the last occurrence of a specified substring. Returns -1 if not found.
    - **Snippet**:
    ```csharp
    string myString = "Hello, World! Hello!";
    int lastIndex = myString.LastIndexOf("Hello"); // lastIndex is 14
    ```

- 5. `Replace`
    - **Definition**: Replaces all occurrences of a specified substring with another substring.
    - **Snippet**:
    ```csharp
    string myString = "Hello, World!";
    string replaced = myString.Replace("World", "C#"); // replaced is "Hello, C#!"
    ```

- 6. `ToUpper`
    - **Definition**: Converts the string to uppercase.
    - **Snippet**:
    ```csharp
    string myString = "Hello, World!";
    string upper = myString.ToUpper(); // upper is "HELLO, WORLD!"
    ```

- 7. `ToLower`
    - **Definition**: Converts the string to lowercase.
    - **Snippet**:
    ```csharp
    string myString = "Hello, World!";
    string lower = myString.ToLower(); // lower is "hello, world!"
    ```

- 8. `Trim`
    - **Definition**: Removes all leading and trailing whitespace characters from the string.
    - **Snippet**:
    ```csharp
    string myString = "   Hello, World!   ";
    string trimmed = myString.Trim(); // trimmed is "Hello, World!"
    ```

- 9. `Split`
    - **Definition**: Splits the string into an array of substrings based on specified delimiters.
    - **Snippet**:
    ```csharp
    string myString = "apple,banana,cherry";
    string[] fruits = myString.Split(','); // fruits is ["apple", "banana", "cherry"]
    ```

- 10. `Join`
    - **Definition**: Concatenates the elements of a string array, using a specified separator between each element.
    - **Snippet**:
    ```csharp
    string[] fruits = { "apple", "banana", "cherry" };
    string joined = string.Join(", ", fruits); // joined is "apple, banana, cherry"
    ```

- 11. `Contains`
    - **Definition**: Determines whether the string contains a specified substring.
    - **Snippet**:
    ```csharp
    string myString = "Hello, World!";
    bool contains = myString.Contains("World"); // contains is true
    ```

- 12. `StartsWith`
    - **Definition**: Determines whether the string starts with a specified substring.
    - **Snippet**:
    ```csharp
    string myString = "Hello, World!";
    bool startsWith = myString.StartsWith("Hello"); // startsWith is true
    ```

- 13. `EndsWith`
    - **Definition**: Determines whether the string ends with a specified substring.
    - **Snippet**:
    ```csharp
    string myString = "Hello, World!";
    bool endsWith = myString.EndsWith("World!"); // endsWith is true
    ```

- 14. `Format`
    - **Definition**: Formats the specified string by replacing the format items with the string representation of the corresponding objects.
    - **Snippet**:
    ```csharp
    string name = "Alice";
    int age = 30;
    string formatted = string.Format("{0} is {1} years old.", name, age); // formatted is "Alice is 30 years old."
    ```

- 15. `Equals`
    - **Definition**: Determines whether two string instances have the same value.
    - **Snippet**:
    ```csharp
    string str1 = "Hello";
    string str2 = "Hello";
    bool areEqual = str1.Equals(str2); // areEqual is true
    ```

- 16. `IsNullOrEmpty`
    - **Definition**: Determines whether a specified string is `null` or an empty string.
    - **Snippet**:
    ```csharp
    string myString = "";
    bool isNullOrEmpty = string.IsNullOrEmpty(myString); // isNullOrEmpty is true
    ```

- 17. `IsNullOrWhiteSpace`
    - **Definition**: Determines whether a specified string is `null`, empty, or consists only of white-space characters.
    - **Snippet**:
    ```csharp
    string myString = "   ";
    bool isNullOrWhiteSpace = string.IsNullOrWhiteSpace(myString); // isNullOrWhiteSpace is true
    ```

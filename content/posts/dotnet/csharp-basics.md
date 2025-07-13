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

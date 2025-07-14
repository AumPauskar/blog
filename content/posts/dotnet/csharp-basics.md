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

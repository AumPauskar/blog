+++
title = 'WebApis Using DDD'
date = 2025-12-30T11:02:38Z
tags = ["dotnet", "c#", "oops"]
author = "Aum Pauskar"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = ""
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

# WebApis Using DDD

The DDD architecture separates your core business logic (the "Domain") from technical details like databases (the "Infrastructure") or web frameworks (the "API").

Unlike using a flat architecture using a DDD architecture requires your code to have a central entry point which will be your `API` this will be your base project and with contain the `Program.cs`. This project will be of the type `webapi`. We will have other projects which will be of the type `classlib`. These will complement your base code with their respective functions.

## Creating your solution

Let's assume your solution is named **`Project1`** so this will how you shall create the various projects within your solution. Best practices is to capitalize the solution name and the projectname.

Here is how you can do it using the dotnet CLI

- Creating your base solution
    ```bash
    dotnet new sln -n Project1
    ```
- Creating your base project
    ```bash
    dotnet new webapi -n Project1.Api
    ```
- Creating the complementing solutions
    ```bash
    dotnet new classlib -n Project1.Domain
    dotnet new classlib -n Project1.Application
    dotnet new classlib -n Project1.Infrastructure
    dotnet new classlib -n Project1.Client
    ```
- Adding your various projects to the solution
    - Doing it manually
        ```bash
        dotnet sln add MyProject.Domain/MyProject.Domain.csproj
        dotnet sln add MyProject.Application/MyProject.Application.csproj
        dotnet sln add MyProject.Infrastructure/MyProject.Infrastructure.csproj
        dotnet sln add MyProject.Api/MyProject.Api.csproj
        dotnet sln add MyProject.Client/MyProject.Client.csproj
        ```
    - Recursively adding the files in linux based systems
        ```bash
        dotnet sln add **/*.csproj
        ```
    - Recursively adding the files in windows based systems (powershell)
        ```bash
        Get-ChildItem -Recurse *.csproj | ForEach-Object { dotnet sln add $_.FullName }
        ```

You can also do it via an IDE if doing from a GUI seems better.
+++
title = 'PHP'
date = 2025-03-21T20:47:43+07:00
tags = [""]
author = "Aum Pauskar"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "A simple php tutorial"
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

# PHP

## What is php?
PHP (Hypertext Preprocessor) is a widely-used open-source scripting language that is especially suited for web development and can be embedded into HTML. Here's a breakdown:

- Server-Side Scripting: PHP code is executed on the server, and the results are sent to the user's web browser as HTML. This contrasts with client-side scripting languages like JavaScript, which are executed in the browser.
- Dynamic Web Pages: PHP allows you to create dynamic web pages that can change content based on user input, database information, or other factors.
- Database Interaction: PHP can connect to various databases (like MySQL, PostgreSQL, and Oracle) to store and retrieve data. This is essential for building web applications that require data management.
- Open Source: PHP is open-source, meaning it's free to use and distribute. This has contributed to its widespread adoption.
- Cross-Platform: PHP runs on various operating systems, including Windows, Linux, and macOS.
- Uses:
    - Building websites and web applications
    - Developing e-commerce platforms
    - Creating content management systems (CMS) like WordPress, Drupal, and Joomla
    - Handling form data
    - Generating dynamic page content.

## Basics

### IO
- Print statement
    ```php
    <?php
        echo "Hello, World!"; // Outputs text to the screen
    ?>
    ```

### Comments and variables
- Comments
    ```php
    // This is a comment
    ```

    ```php
    /*
    This is a 
    multi-line comment
    */
    ```

- Variables
    ```php
    <?php
        $name = "John";
        $age = 25;
        echo $name; // Outputs: John
    ?>
    ```

### Control statement
- If-else statements
    ```php
    <?php
        $age = 18;

        if ($age >= 18) {
            echo "You are an adult.";
        } else {
            echo "You are a minor.";
        }
    ?>
    ```

- Switch statements
    ```php
    <?php
        $day = 2;

        switch ($day) {
            case 1:
                echo "Monday";
                break;
            case 2:
                echo "Tuesday";
                break;
            default:
                echo "Other day";
        }
    ?>
    ```
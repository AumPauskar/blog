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

1.  PHP Start and End Tags: These tags (`<?php` and `?>`) are essential for embedding PHP code within HTML or other text-based files. The PHP interpreter only processes the code located between these tags.

2.  Statements and Semicolons: PHP code is made up of individual instructions called statements. Each complete statement in PHP must end with a semicolon (`;`) to tell the interpreter where one instruction ends and the next begins.

3.  Variables: In PHP, variables are used to store data. They are represented by a dollar sign (`$`) followed by the variable name (e.g., `$myVariable`). PHP is dynamically typed, meaning you don't need to explicitly declare the data type of a variable before assigning a value to it.

### IO
- Print statement
    ```php
    <?php
    $message = "This is a message.";
    echo $message;
    echo "<br>";

    print "Another message.";
    echo "<br>";

    $data = array("apple", "banana", "cherry");
    var_dump($data);
    echo "<br>";

    print_r($data);
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

- Loops
    ```php
    <?php
    echo "\nFor loop...";

    for ($i = 0; $i < 5; $i++) {
        echo "The number is: " . $i . "<br>";
    }

    echo "\nWhile loop...";
    $count = 0;
    while ($count < 3) {
        echo "Count is: " . $count . "<br>";
        $count++;
    }

    echo "\nDo while loop...";
    $num = 5;
    do {
        echo "Number is: " . $num . "<br>";
        $num++;
    } while ($num < 8);

    echo "\nFor each loop...";
    $colors = array("red", "green", "blue");
    foreach ($colors as $color) {
        echo "Color: " . $color . "<br>";
    }

    $person = array("name" => "Alice", "age" => 28);
    foreach ($person as $key => $value) {
        echo $key . ": " . $value . "<br>";
    }

    ?>
    ```

## Functions
Functions: In PHP, a **function** is a block of reusable code that performs a specific task. Functions help organize your code, make it more readable, and avoid code duplication.

**Basic Structure of a Function:**

```php
<?php
function functionName($parameter1, $parameter2, ...) {
    // Code to be executed
    return $returnValue; // Optional
}
?>
```

Key Components:

- `function` keyword: This keyword signifies the start of a function definition.
- `functionName`: This is the identifier you'll use to call or invoke the function. Function names should be descriptive and follow PHP naming conventions (usually start with a letter or underscore, followed by letters, numbers, or underscores).
- `($parameter1, $parameter2, ...)`: These are optional **parameters** (or arguments) that the function can accept as input. You can have zero or more parameters. When you call the function, you'll provide the values for these parameters (called arguments).
- `{ ... }`:** The curly braces enclose the **function body**, which contains the actual PHP code that the function will execute.
- `return $returnValue;` (Optional): The `return` statement is used to send a value back from the function to the code that called it. A function can return any data type (scalar, array, object, etc.) or nothing at all (in which case it implicitly returns `null`).

**Example Function:**

```php
<?php
function greet($name) {
    echo "Hello, " . $name . "!\n";
}

// Calling the function
greet("Alice"); // Output: Hello, Alice!
greet("Bob");   // Output: Hello, Bob!
?>
```

- Function Scope: Variables declared inside a function have **local scope**, meaning they are only accessible within that function. Variables declared outside functions have **global scope** and are generally not directly accessible inside functions (unless you use the `global` keyword, which is often discouraged).

## Network based applications

### Making HTTP Requests (GET/POST):

PHP provides several ways to make HTTP requests to interact with external APIs or web services. Here are two common methods:

- Using `file_get_contents()` (for simple GET requests):\
    This function can be used to fetch the content of a URL. It's straightforward for simple GET requests where you don't need much control over headers or request bodies.

    ```php
    <?php
    $url = 'https://api.example.com/data'; // Replace with the actual API endpoint

    // Make a GET request
    $response = @file_get_contents($url);

    if ($response !== false) {
        // Process the response (usually JSON)
        $data = json_decode($response, true); // Decode JSON into an associative array
        if ($data) {
            print_r($data);
        } else {
            echo "Failed to decode JSON response.\n";
        }
    } else {
        echo "Failed to fetch data from the API.\n";
    }
    ?>
    ```

    * `@file_get_contents($url)`: Attempts to retrieve the content from the specified URL. The `@` symbol is used for error suppression (handle errors with proper checks instead in production).
    * `json_decode($response, true)`: If the API returns JSON, this function decodes it into a PHP associative array (the `true` parameter).

- Using `curl` (more powerful and versatile): \
    The `curl` extension provides a more flexible and powerful way to make various types of HTTP requests (GET, POST, PUT, DELETE, etc.) and allows you to control headers, request bodies, timeouts, and more.

    ```php
    <?php
    $url = 'https://api.example.com/data'; // Replace with the actual API endpoint

    // Initialize cURL session
    $ch = curl_init($url);

    // Set cURL options (for GET request, these are often defaults)
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true); // Return the response as a string

    // Execute the request
    $response = curl_exec($ch);

    // Check for errors
    if (curl_errno($ch)) {
        echo 'cURL error: ' . curl_error($ch) . "\n";
    } else {
        // Process the response
        $data = json_decode($response, true);
        if ($data) {
            print_r($data);
        } else {
            echo "Failed to decode JSON response.\n";
        }
    }

    // Close cURL resource
    curl_close($ch);

    // Example of a POST request using cURL:
    $postUrl = 'https://api.example.com/submit';
    $postData = array('name' => 'John Doe', 'email' => 'john.doe@example.com');

    $chPost = curl_init($postUrl);
    curl_setopt($chPost, CURLOPT_RETURNTRANSFER, true);
    curl_setopt($chPost, CURLOPT_POST, true); // Set as POST request
    curl_setopt($chPost, CURLOPT_POSTFIELDS, http_build_query($postData)); // Encode data for POST

    $postResponse = curl_exec($chPost);

    if (!curl_errno($chPost)) {
        $postResult = json_decode($postResponse, true);
        // Process $postResult
        print_r($postResult);
    } else {
        echo 'cURL POST error: ' . curl_error($chPost) . "\n";
    }

    curl_close($chPost);
    ?>
    ```

    * `curl_init($url)`: Initializes a new cURL session for the given URL.
    * `curl_setopt()`: Sets various options for the cURL session, such as:
        * `CURLOPT_RETURNTRANSFER`: To return the transfer as a string instead of outputting it directly.
        * `CURLOPT_POST`: To specify that it's a POST request (set to `true`).
        * `CURLOPT_POSTFIELDS`: To provide the data to be sent in the POST request (often as an array which `http_build_query()` encodes).
    * `curl_exec($ch)`: Executes the cURL session.
    * `curl_errno($ch)` and `curl_error($ch)`: Used to check for errors during the request.
    * `curl_close($ch)`: Closes the cURL session and releases resources.

### Creating a Basic API in PHP:

Building an API with PHP involves creating endpoints (URLs) that respond to specific HTTP methods (GET, POST, etc.) and return data (often in JSON format).

Basic Structure

1.  Receive the Request: Determine the requested URL and the HTTP method used (e.g., using `$_SERVER['REQUEST_URI']` and `$_SERVER['REQUEST_METHOD']`).
2.  Process the Request: Based on the URL and method, perform the necessary actions (e.g., fetch data from a database, process user input).
3.  Format the Response: Prepare the data to be sent back to the client (usually as a JSON string).
4.  Send the Response: Set the appropriate HTTP headers (e.g., `Content-Type: application/json`) and output the formatted data.

- Simple API Example (handling GET requests):\
    Let's say you want to create an API endpoint `/api/users` that returns a list of users.

    ```php
    <?php
    // Simulate fetching users from a database
    $users = [
        ['id' => 1, 'name' => 'Alice', 'email' => 'alice@example.com'],
        ['id' => 2, 'name' => 'Bob', 'email' => 'bob@example.com'],
    ];

    // Set the content type header to JSON
    header('Content-Type: application/json');

    // Encode the PHP array as a JSON string and output it
    echo json_encode($users);
    ?>
    ```

    If you access this PHP file (e.g., `yourdomain.com/api/users.php`) with a GET request, it will output:

    ```json
    [
        {"id":1,"name":"Alice","email":"alice@example.com"},
        {"id":2,"name":"Bob","email":"bob@example.com"}
    ]
    ```

- Handling Different HTTP Methods and URL Parameters: \
    To create more sophisticated APIs, you'll need to handle different HTTP methods and potentially extract parameters from the URL.

    ```php
    <?php
    // Set content type to JSON
    header('Content-Type: application/json');

    $requestMethod = $_SERVER['REQUEST_METHOD'];
    $requestUri = $_SERVER['REQUEST_URI'];

    // Basic routing (you'd typically use a more robust router in a real application)
    if ($requestUri === '/api/users') {
        if ($requestMethod === 'GET') {
            // Simulate fetching all users
            $users = [/* ... */];
            echo json_encode($users);
        } elseif ($requestMethod === 'POST') {
            // Handle creating a new user (read data from request body)
            $postData = json_decode(file_get_contents('php://input'), true);
            // Process $postData and potentially save to database
            $newUser = ['id' => 3, 'name' => $postData['name'] ?? '', 'email' => $postData['email'] ?? ''];
            echo json_encode($newUser);
        } else {
            http_response_code(405); // Method Not Allowed
            echo json_encode(['error' => 'Method not allowed']);
        }
    } elseif (preg_match('/\/api\/users\/(\d+)/', $requestUri, $matches)) {
        $userId = $matches[1];
        if ($requestMethod === 'GET') {
            // Simulate fetching a specific user by ID
            $user = /* ... fetch user with ID $userId ... */;
            if ($user) {
                echo json_encode($user);
            } else {
                http_response_code(404); // Not Found
                echo json_encode(['error' => 'User not found']);
            }
        } elseif ($requestMethod === 'PUT') {
            // Handle updating user with ID $userId (read data from request body)
            // ...
        } elseif ($requestMethod === 'DELETE') {
            // Handle deleting user with ID $userId
            // ...
        } else {
            http_response_code(405); // Method Not Allowed
            echo json_encode(['error' => 'Method not allowed']);
        }
    } else {
        http_response_code(404); // Not Found
        echo json_encode(['error' => 'Endpoint not found']);
    }
    ?>
    ```

    * `$_SERVER['REQUEST_METHOD']`: Gets the HTTP method used (GET, POST, PUT, DELETE, etc.).
    * `$_SERVER['REQUEST_URI']`: Gets the requested URI.
    * `file_get_contents('php://input')`: Reads the raw data from the request body (useful for POST/PUT requests with JSON data).
    * `http_response_code(405)` and `http_response_code(404)`: Set the appropriate HTTP status codes for the response.
    * Basic routing logic using `if/elseif` and regular expressions (`preg_match`) to handle different URL patterns.

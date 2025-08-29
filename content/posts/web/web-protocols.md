+++
title = 'Web Protocols'
date = 2025-08-29T06:00:34Z
tags = ["web", "protocols"]
author = "Aum Pauskar"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "A document containing different types of web protocols"
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

# Web Protocols

## HTTP

Hypertext Transfer Protocol (HTTP) is an application-layer protocol for transmitting hypermedia documents, like HTML, across the internet. It operates on a client-server model, where a client (e.g., a web browser) sends a request to a server, and the server returns a response. HTTP is the foundation of data exchange on the World Wide Web.


### HTTP Request-Response Model

HTTP is a **stateless protocol**, which means each request from a client is treated as an independent transaction; the server doesn't remember previous requests. This can be overcome with technologies like cookies. The communication is initiated by the client and follows a specific structure for both the request and the response.

- HTTP Request: A request message from a client to a server consists of:
    - Request Line: This includes the **HTTP method** (e.g., `GET`, `POST`), the **URI** of the requested resource (e.g., `/index.html`), and the **HTTP version** (e.g., `HTTP/1.1`).
    - Request Headers: Key-value pairs that provide metadata about the request, such as the `Host` (the domain name of the server), `User-Agent` (the client's browser), and `Accept` (the type of data the client can receive).
    - Empty Line: Separates the headers from the body.
    - Request Body (Optional): Contains the data being sent to the server, for example, form data in a `POST` request.


- HTTP Response: A response message from a server to a client consists of:
    - Status Line: This includes the **HTTP version**, a three-digit **status code** (e.g., `200`, `404`), and a short **status text** (e.g., `OK`, `Not Found`).
    - Response Headers: Key-value pairs providing metadata about the response, such as `Content-Type` (the format of the data in the body) and `Content-Length` (the size of the body).
    - Empty Line: Separates the headers from the body.
    - Response Body (Optional): Contains the requested resource, such as an HTML file, an image, or JSON data.


### Key HTTP Concepts

- HTTP Methods: Also called verbs, these indicate the desired action for a given resource. Common methods include:
    - `GET`: Retrieves data from the server. It's idempotent and safe (doesn't change the server's state).
    - `POST`: Submits data to the server to create a new resource.
    - `PUT`: Updates or replaces an existing resource.
    - `DELETE`: Removes a specified resource.
    - `HEAD`: Retrieves only the headers of a response, without the body.
    - `PATCH`: Applies partial modifications to a resource.

- **Status Codes:** Three-digit numbers that communicate the result of a request.
    - **1xx (Informational):** The request has been received and the process is continuing.
    - **2xx (Success):** The request was successfully received, understood, and accepted.
    - **3xx (Redirection):** Further action needs to be taken to complete the request.
    - **4xx (Client Error):** The request contains bad syntax or cannot be fulfilled. (e.g., **404 Not Found**)
    - **5xx (Server Error):** The server failed to fulfill an apparently valid request. (e.g., **500 Internal Server Error**)

-  **URLs and URIs:** Resources are identified on the network by a **Uniform Resource Identifier (URI)**. A **URL** (Uniform Resource Locator) is a type of URI that also provides the means of locating the resource, such as the protocol (`http://`), domain name, and path.


### HTTP Versions

HTTP has evolved to improve performance and add features:

* **HTTP/1.0:** The original version, which required a new TCP connection for every single request.
* **HTTP/1.1:** Introduced **persistent connections**, allowing multiple requests to be sent over a single TCP connection, significantly reducing latency. It also added more methods and caching mechanisms.
* **HTTP/2:** A major revision that introduced **multiplexing**, allowing multiple requests and responses to be sent simultaneously over a single connection, and **header compression**, which reduces overhead.
* **HTTP/3:** The newest version, which uses **QUIC** (Quick UDP Internet Connections) instead of TCP. This further reduces connection setup time and provides better handling of data loss, leading to a faster and more reliable experience, especially on mobile networks.

### HTTPS: The Secure Version

**HTTPS** (Hypertext Transfer Protocol Secure) is not a separate protocol but rather the use of HTTP over an encrypted **SSL/TLS (Secure Sockets Layer/Transport Layer Security)** connection. It encrypts the entire communication, including the headers and body, protecting data from eavesdropping and man-in-the-middle attacks. It uses port 443, whereas standard HTTP uses port 80.
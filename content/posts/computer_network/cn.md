+++
title = 'Computer networks'
date = 2023-11-23T12:50:11+05:30
draft = false
tags = ["computer networks", "networking", "internet", "communication", "protocols"]
author = "Aum Pauskar"
description = "Computer networks and the protocols used in them"
+++

# Computer networks

## Packets
In networking, a packet is a small segment of a larger message. Data sent over computer networks*, such as the Internet, is divided into packets. These packets are then recombined by the computer or device that receives them. The Internet is a "packet switching" network. Packet switching refers to the ability of networking equipment to process packets independently from each other. It also means that packets can take different network paths to the same destination, so long as they all arrive at the destination. Because of packet switching, packets from multiple computers can travel over the same wires in basically any order. This enables multiple connections to take place over the same networking equipment at the same time.
- Refernce: [Cloudflare](https://www.cloudflare.com/en-gb/learning/network-layer/what-is-a-packet/)
### MTU
MTU stands for Maximum Transmission Unit. It is a parameter that defines the maximum size of a data packet that can be transmitted in a network. The MTU is usually specified in bytes. When data is sent over a network, it is divided into packets, and the MTU determines the maximum size of these packets.

The effect of increasing or decreasing the MTU can have implications on network performance. Here are some key points:

1. **Increasing MTU:**
   - Larger MTU generally allows for more data to be sent in a single packet, which can lead to more efficient data transmission.
   - Larger packets mean fewer headers and less overhead per unit of data, resulting in a more efficient use of network resources.
   - However, increasing MTU may also lead to higher latency for small packets, as they need to wait for larger packets to be transmitted first.

2. **Decreasing MTU:**
   - Smaller MTU can be beneficial in situations where the network has a high error rate or where there are restrictions on the maximum packet size.
   - Smaller packets can be less prone to errors and can be retransmitted more quickly in case of errors.
   - However, using smaller MTU values can increase the overhead per unit of data due to the additional headers in each packet.

The MTU for popular network protocols can vary. Here are the typical MTU values for some common protocols:

- **Ethernet:** The standard MTU for Ethernet is 1500 bytes.
- **Internet Protocol (IP):** The default MTU for IP is often set to 1500 bytes.
- **IPv6:** IPv6 typically uses a larger MTU, often set to 1280 bytes as a minimum.
- **Point-to-Point Protocol (PPP):** The default MTU for PPP is 1500 bytes.

It's important to note that while these values are common, network administrators can configure MTU values based on specific requirements and considerations of the network infrastructure. It's also crucial to ensure that all devices on a network are configured with compatible MTU values to avoid fragmentation and performance issues.

### Nodal delay
Nodal delay, also known as node delay or network delay, is a concept in computer networking that refers to the time it takes for a packet of data to traverse from the source node to the destination node in a network. The nodal delay can be broken down into several components, each contributing to the total delay:

1. **Processing Delay (d_proc):** The time it takes for a router or switch to examine the incoming packet header and determine where to forward the packet. This can be optimized by using faster hardware or by implementing more efficient routing algorithms.

2. **Queuing Delay (d_queue):** The time the packet spends waiting in a queue before it can be processed by the router or switch. This can be minimized by using faster hardware or by implementing more efficient routing algorithms and by increasing memory cache. \
Formula: $LA \over R$ \
Where L is the length of the packet and R is the rate at which the packet is being transmitted and A is the average arrival rate of the packets.

3. **Transmission Delay (d_trans):** The time it takes to push the bits of the packet onto the link. This is influenced by the link's bandwidth.This can be minimized by using higher bandwidth links. \
Formula: $L \over R$ \
Where L is the length of the packet and R is the rate at which the packet is being transmitted.

4. **Propagation Delay (d_prop):** The time it takes for a bit to travel from the source to the destination. This is determined by the distance between the nodes and the speed of the medium (e.g., speed of light in fiber). This can be minimized by using shorter links or faster transmission media.

The formula for nodal delay (D) can be expressed as the sum of these individual components:

D = $d_{\text{proc}} + d_{\text{queue}} + d_{\text{trans}} + d_{\text{prop}}$

It's important to note that each of these components can vary based on factors such as network congestion, the processing capabilities of routers, and the characteristics of the transmission medium. Minimizing nodal delay is crucial for optimizing the overall performance of a network. Network designers and administrators often work to optimize each component of nodal delay to improve the efficiency of data transmission in a network.

## Circuit switching vs packet switching
### Circuit switching
Circuit switching works on the principle of a dedicated path for each communication link where in the comminication link is physically changed either physically by a person or by a machine
- Advantages of Circuit Switching:
	1. Guaranteed bandwidth: Circuit switching provides a dedicated path for communication, ensuring that bandwidth is guaranteed for the duration of the call.
	2. Low latency: Circuit switching provides low latency because the path is predetermined, and there is no need to establish a connection for each packet.
	3. Predictable performance: Circuit switching provides predictable performance because the bandwidth is reserved, and there is no competition for resources.
	4. Suitable for real-time communication: Circuit switching is suitable for real-time communication, such as voice and video, because it provides low latency and predictable performance.

- Disadvantages of Circuit Switching:
	1. Inefficient use of bandwidth: Circuit switching is inefficient because the bandwidth is reserved for the entire duration of the call, even when no data is being transmitted.
	2. Limited scalability: Circuit switching is limited in its scalability because the number of circuits that can be established is finite, which can limit the number of simultaneous calls that can be made.
	3. High cost: Circuit switching is expensive because it requires dedicated resources, such as hardware and bandwidth, for the duration of the call.

### Packet switching
Packet switching is a system where each packet has the source address and the destination address and every bit of data has a common link.
- Advantages of Packet Switching:
	1. Efficient use of bandwidth: Packet switching is efficient because bandwidth is shared among multiple users, and resources are allocated only when data needs to be transmitted.
	2. Flexible: Packet switching is flexible and can handle a wide range of data rates and packet sizes.
	3. Scalable: Packet switching is highly scalable and can handle large amounts of traffic on a network.
	4. Lower cost: Packet switching is less expensive than circuit switching because resources are shared among multiple users.

- Disadvantages of Packet Switching:
	1. Higher latency: Packet switching has higher latency than circuit switching because packets must be routed through multiple nodes, which can cause delay.
	2. Limited QoS: Packet switching provides limited QoS guarantees, meaning that different types of traffic may be treated equally.
	3. Packet loss: Packet switching can result in packet loss due to congestion on the network or errors in transmission.
	4. Unsuitable for real-time communication: Packet switching is not suitable for real-time communication, such as voice and video, because of the potential for latency and packet loss.

- Refence: [Geeks for Geeks](https://www.geeksforgeeks.org/difference-between-circuit-switching-and-packet-switching/)

## Bandwidth vs throughput
Bandwidth is the maximum amount of data that can be transmitted over a network in a given amount of time. It is typically measured in bits per second (bps), kilobits per second (kbps), or megabits per second (Mbps). Throughput is the actual amount of data that is transmitted over a network in a given amount of time. It is typically measured in bits per second (bps), kilobits per second (kbps), or megabits per second (Mbps). Bandwidth and throughput are often used interchangeably, but they are not the same thing. Bandwidth is the theoretical maximum amount of data that can be transmitted over a network, while throughput is the actual amount of data that is transmitted over a network. For example, a network may have a bandwidth of 100 Mbps, but the actual throughput may be only 50 Mbps. This is because the network may be congested or there may be other factors that limit the amount of data that can be transmitted. Bandwidth is a measure of capacity.

## Internet protocol stack
- Application: Ftp, http, smtp
- Transport: TCP, UDP
- Network: IP, routing protocols
- Link: Ethernet, 802.111, PPP
- Physical: Bits on the wire


### ISO/OSI model
- Application: This layer is responsible for providing services to the end-user applications. It includes protocols such as FTP (File Transfer Protocol), HTTP (Hypertext Transfer Protocol), and SMTP (Simple Mail Transfer Protocol). These protocols enable functions such as file transfer, web browsing, and email communication.

- Presentation: The presentation layer is responsible for data representation and encryption. It ensures that data from the application layer is properly formatted and encrypted for transmission. This layer also handles tasks such as data compression and decompression.

- Session: The session layer establishes, manages, and terminates communication sessions between applications. It provides synchronization and checkpointing mechanisms to ensure reliable communication. This layer helps in maintaining the continuity of communication between applications.

- Transport: The transport layer is responsible for end-to-end communication between hosts. It ensures reliable and efficient data transfer by providing services such as segmentation, reassembly, error recovery, and flow control. The two main protocols at this layer are TCP (Transmission Control Protocol) and UDP (User Datagram Protocol).

- Network: The network layer handles the routing and forwarding of data packets across different networks. It is responsible for addressing, routing, and packet delivery. The main protocol at this layer is IP (Internet Protocol), which enables the identification and addressing of devices on a network.

- Link: The link layer is responsible for the physical connection between nodes on a network. It handles tasks such as framing, error detection, and medium access control. Common protocols at this layer include Ethernet, 802.111 (Wi-Fi), and PPP (Point-to-Point Protocol).

- Physical: The physical layer deals with the transmission of raw bits over a physical medium. It defines the electrical, mechanical, and functional specifications for the physical connection. This layer includes components such as cables, connectors, and network interface cards (NICs).

### Encapsulation
In networking, encapsulation refers to the process of wrapping data with necessary protocol information before it is transmitted over the network. Each layer of the OSI model adds its own header (and sometimes a footer) to the data from the layer above it. This process allows data to be transmitted seamlessly across networks.

For example, when a message is sent from a device, it starts at the Application layer and moves down the OSI layers. Each layer adds its own specific information, such as addressing, error checking, and sequencing information. By the time the message reaches the Physical layer, it has been encapsulated with all the necessary information for transmission, reception, and interpretation at the destination.

In summary, encapsulation:

- Allows complex data communication processes to be broken down into smaller, simpler parts.
- Provides a way to integrate the protocols and services of each layer.
- Ensures that the systems on the sending and receiving ends have the necessary information to understand and process the data correctly.

## Application layer
The application layer is the highest layer in the OSI model and the TCP/IP model, which provides the interface and protocols for communication between applications and devices over a network. Some of the examples using P2P cimmunicatioins are
- HTTP
- FTP
- SMTP
- DNS
- DHCP

## Paradigms
The client-server model and peer-to-peer (P2P) model are two fundamental architectures used in computer networks to facilitate communication and resource sharing among devices. Let's explore each model in more detail:

1. **Client-Server Model:**

   - **Definition:**
     - In the client-server model, the system is divided into two main components: clients and servers.
     - Clients are end-user devices or applications that request services or resources from the server.
     - Servers are powerful computers or software applications that provide services or resources to clients.

   - **Communication Flow:**
     - Clients initiate requests for services or resources.
     - Servers respond to client requests by providing the requested services or resources.
     - Communication is typically one-way, with clients making requests and servers responding.

   - **Characteristics:**
     - Centralized: Services and resources are centralized on servers.
     - Scalability: Easier to scale as the server can handle multiple client requests.
     - Control: Servers control access to resources and manage security.

   - **Examples:**
     - Web servers (responding to browser requests).
     - File servers (providing file storage and retrieval).
     - Database servers (managing and providing access to databases).

   - **Advantages:**
     - Centralized management.
     - Controlled access to resources.
     - Easier maintenance and updates.

   - **Disadvantages:**
     - Single point of failure (if the server goes down, clients may lose access).
     - Scalability challenges as the number of clients increases.

2. **Peer-to-Peer (P2P) Model:**

   - **Definition:**
     - In the P2P model, all devices (peers) on the network have equal status and can act as both clients and servers.
     - Peers communicate directly with each other without the need for a centralized server.

   - **Communication Flow:**
     - Peers can both request and provide resources/services to each other.
     - There is no central server controlling communication.

   - **Characteristics:**
     - Decentralized: No central server; all peers have equal status.
     - Dynamic: Peers can join or leave the network at any time.
     - Resource Sharing: Peers share resources directly with each other.

   - **Examples:**
     - BitTorrent file sharing.
     - Skype for P2P communication.
     - Blockchain networks (like Bitcoin).

   - **Advantages:**
     - Decentralization reduces the risk of a single point of failure.
     - Scalability is inherent as each peer can contribute resources.

   - **Disadvantages:**
     - Lack of centralized control can make it challenging to manage and secure.
     - Initial setup and discovery of peers can be complex.

## Sockets
Sockets play a crucial role in networking, providing a programming interface for network communication. In the context of computer networks, a socket is a software endpoint that establishes communication between two processes over a network. Here are some key aspects and the importance of sockets in networking:

1. **Definition:**
   - A socket is a combination of an IP address and a port number that identifies a specific endpoint on a network.
   - It provides a mechanism for processes on different devices to communicate with each other.

2. **Communication Channels:**
   - Sockets enable processes running on different devices to establish communication channels, allowing data to be sent and received.

3. **Types of Sockets:**
   - There are two main types of sockets: TCP (Transmission Control Protocol) sockets and UDP (User Datagram Protocol) sockets.
     - **TCP Sockets:** Provide a reliable, connection-oriented communication. Data is sent in a stream, and there is acknowledgment of received data.
     - **UDP Sockets:** Offer a connectionless, unreliable communication. Data is sent in discrete packets without acknowledgment.

4. **Client-Server Communication:**
   - In a client-server model, sockets are fundamental for establishing connections. The server creates a socket and binds it to a specific port, waiting for incoming client connections. Clients create sockets to connect to the server's IP address and port.

5. **Importance in Networking:**
   - **Data Transmission:** Sockets facilitate the transmission of data between applications running on different devices. They provide a standardized interface for sending and receiving data.
   - **Protocols Implementation:** Sockets are used to implement various network protocols, such as HTTP, FTP, and others, enabling the exchange of information between clients and servers.
   - **Cross-Platform Communication:** Sockets allow communication between applications running on different operating systems and hardware, promoting interoperability.
   - **Network Programming:** Sockets are essential for network programming, enabling developers to create applications that can communicate over a network, whether it's a local area network (LAN) or the Internet.

6. **Socket Programming:**
   - Developers use socket programming to create applications that can communicate over a network. This involves creating and managing sockets, establishing connections, and handling data transmission.

7. **Security Considerations:**
   - Sockets can be secured using encryption protocols (e.g., SSL/TLS) to protect the confidentiality and integrity of data transmitted over the network.

### Interprocess communication
In networking and operating systems several operations require a dataflow to send and recieve messages. In this cases several ports are selected and opened in the computer to deliver and send and recieve messages.

## TCP vs UDP
| Feature                 | TCP                                      | UDP                                      |
|-------------------------|------------------------------------------|------------------------------------------|
| **Connection**          | Connection-oriented                      | Connectionless                           |
| **Reliability**         | Reliable - ensures data delivery          | Unreliable - no guarantee of data delivery|
| **Ordering**            | In-order delivery of data                | No guaranteed order of delivery          |
| **Acknowledgment**      | Acknowledgment of received data           | No acknowledgment of received data       |
| **Flow Control**        | Yes, uses flow control mechanisms         | No built-in flow control                 |
| **Error Checking**      | Yes, error-checking through checksums     | Limited error checking (optional)        |
| **Header Size**         | Larger header size                       | Smaller header size                      |
| **Overhead**            | Higher overhead due to connection setup   | Lower overhead due to lack of connection setup|
| **Usage**               | Used for applications requiring reliable data transfer, e.g., file transfer, email | Used for real-time applications where low latency is critical, e.g., video streaming, online gaming |

TCP follows virtual circuits

TLS/TSL

## About the transport layer
- It provides logical communication between apps and other processes
- It breake the app segments and then passes on to the network layer
- After the dissassembly of segments it rearranges them.
- There exists more than one transport protocol being **TCP** and **UDP**.

## 
## HTTP
**HTTP Overview from the Perspective of Computer Networks:**

**1. Definition:**
   - **HTTP (Hypertext Transfer Protocol):** It is an application layer protocol used for transmitting hypermedia documents, such as HTML files, over the World Wide Web. It is the foundation of any data exchange on the Web.

**2. Protocol Type:**
   - **Stateless Protocol:** HTTP is inherently stateless, meaning each request from a client to a server is independent and does not retain information about the previous requests. This simplifies communication but requires additional mechanisms (like cookies) for handling state.

**3. Communication Model:**
   - **Client-Server Model:** HTTP follows a client-server model where a client sends requests to a server, and the server responds with the requested resources (e.g., web pages, images).

**4. Connection Establishment:**
   - **Connectionless:** By default, HTTP is connectionless. Each request-response cycle operates independently, and the connection is closed after each transaction.

**5. Transport Protocol:**
   - **Primarily Relies on TCP:** HTTP typically operates over the TCP (Transmission Control Protocol) for reliable and ordered delivery of data. It can also be used over other transport protocols, but TCP is the most common.

**6. Request-Response Cycle:**
   - **Request Format:** Clients send HTTP requests to servers, specifying a method (e.g., GET, POST), a Uniform Resource Identifier (URI), and protocol version in the request header.
   - **Response Format:** Servers respond with an HTTP status code indicating the success or failure of the request, along with the requested resource or an error message.

**7. Stateless Nature:**
   - **No Persistent Connection by Default:** In the traditional HTTP/1.0, each request/response pair is handled in a new connection, and the connection is closed after the response is delivered. This can lead to increased latency for multiple requests.

**8. Persistent Connections:**
   - **HTTP/1.1 introduced Persistent Connections:** To address the latency issue, HTTP/1.1 supports persistent connections, where multiple requests and responses can be sent over a single connection, improving performance.

**9. Security:**
   - **HTTPS (HTTP Secure):** HTTPS is a secure version of HTTP that uses SSL/TLS protocols to encrypt data for secure communication. It adds a layer of security, important for protecting sensitive information.

**10. Header Fields:**
   - **Header Information:** HTTP messages contain header fields that provide information about the message, such as content type, length, and caching directives.

**11. Common Methods:**
   - **GET, POST, PUT, DELETE:** HTTP defines various methods for different operations. GET is used for retrieving resources, POST for submitting data, PUT for updating resources, and DELETE for removing resources.

**12. Cookies:**
   - **State Management:** Cookies are often used to maintain state between client and server in the stateless HTTP protocol.

**13. MIME Types:**
   - **Content Types:** HTTP uses Multipurpose Internet Mail Extensions (MIME) types to specify the type of data being sent, allowing the client to properly interpret and display the content.

### Persistent and non persistent HTTP
| Feature                              | Persistent HTTP                              | Non-Persistent HTTP                          |
|--------------------------------------|----------------------------------------------|--------------------------------------------|
| **Connection Handling**              | Maintains a persistent connection for multiple requests and responses over a single connection | Opens a new connection for each request-response pair, closing the connection after each transaction |
| **Latency**                          | Lower latency as the connection is reused for multiple requests/responses | Higher latency due to the overhead of establishing a new connection for each transaction |
| **Performance**                      | Generally more efficient for multiple requests to the same server | Can be less efficient, especially for a series of rapid, small requests |
| **HTTP Versions**                    | Often associated with HTTP/1.1 and later versions that support persistent connections | Commonly associated with HTTP/1.0, which uses non-persistent connections by default |
| **Header Overhead**                  | Reduced header overhead as headers need to be sent only once for multiple transactions | Increased header overhead as headers must be sent with each new connection |
| **Resource Utilization**             | Better resource utilization, especially in scenarios with multiple requests from the same client | Resources are less efficiently utilized due to frequent connection setup and teardown |
| **Implementation Complexity**        | May require more complex implementation to manage connection reuse and concurrency | Simpler implementation as each request-response cycle is independent |
| **Scalability**                      | Can improve scalability by reducing the load on the server for connection establishment | May face scalability challenges with a high number of short-lived connections |
| **Example Scenario**                 | Downloading multiple resources from a website where the same server is used | Opening a series of links on a webpage, where each link triggers a new connection |
| **Connection Header (HTTP/1.1)**     | Uses the `Connection: keep-alive` header to indicate a persistent connection | Uses the `Connection: close` header to indicate that the connection should be closed after the response |

### Processflow of persistent and non persistent http
- Process Flow of Persistent HTTP:

	1. **Connection Establishment:**
	   - The client initiates a TCP connection to the server.
	   - The connection is established and marked as persistent, allowing multiple requests and responses to occur over the same connection.

	2. **Request-Response Cycle (Persistent):**
	   - After the initial connection setup, the client can send multiple HTTP requests over the same connection without reopening it.
	   - The server processes each request and responds with the corresponding HTTP responses.
	   - The connection remains open until either party explicitly closes it or a timeout occurs.

	3. **Header Information (Persistent):**
	   - Headers, including the `Connection: keep-alive` header, are used to indicate that the connection should be kept open for future transactions.

	4. **Subsequent Requests (Persistent):**
	   - The client can send additional HTTP requests over the same connection without the need to establish a new connection for each transaction.
	   - This process continues until the client or server decides to close the connection.

	5. **Connection Closure (Optional):**
	   - The connection can be explicitly closed by either the client or the server using the `Connection: close` header, or it may be closed due to a timeout.

- Process Flow of Non-Persistent HTTP:

	1. **Connection Establishment:**
	   - The client initiates a TCP connection to the server.

	2. **Request-Response Cycle (Non-Persistent):**
	   - The client sends a single HTTP request to the server over the established connection.
	   - The server processes the request and sends back the corresponding HTTP response.

	3. **Connection Closure:**
	   - The connection is immediately closed by either the client or the server after the response is received.
	   - This closure ensures that each request-response pair occurs in a new, independent connection.

	4. **Header Information (Non-Persistent):**
	   - Each HTTP request and response may include headers, but there is no need for headers to maintain a persistent connection.

	5. **Subsequent Requests (New Connections):**
	   - For each new request, the client must establish a new TCP connection to the server.
	   - The process repeats for each transaction, with the connection being closed after each request-response cycle.

	6. **Connection Overhead (Non-Persistent):**
	   - The overhead of establishing and tearing down connections for each transaction can impact performance, especially in scenarios with multiple rapid requests.

## CDN
A Content Delivery Network (CDN) is a geographically distributed network of servers and their data centers. The goal of a CDN is to provide high availability and performance by distributing the service spatially relative to end-users. CDNs serve a large portion of the Internet content today, including web objects (text, graphics, URLs and scripts), downloadable objects (media files, software, documents), applications, live streaming media, on-demand streaming media, and social networks.

In real life, CDNs are used to speed up websites and ensure they remain accessible to users, even when traffic is high. When a user visits a website that uses a CDN, the CDN will deliver the content from the server closest to the user, rather than the website's original server. This reduces the time it takes for the data to travel, resulting in faster load times for the user.

For example, if a website's original server is in New York and a user in London accesses it, a CDN could serve the website's content from a server in London (or closer) instead of the server in New York. This reduces latency and improves the user's experience.

## Mail protocols

Mail protocols are sets of rules that help in the sending and receiving of emails over a network. The main mail protocols include:

1. **SMTP (Simple Mail Transfer Protocol):** This protocol is used for sending emails from a client to a server or between servers. It's used when email is delivered from an email client, like Outlook, to an email server or when email is delivered from one email server to another.
   - Working of SMTP:
     - The sender's email client connects to the sender's mail server on port 25.
     - The sender's mail server connects to the recipient's mail server on port 25.
     - The sender's mail server sends the email to the recipient's mail server.
     - The recipient's mail server delivers the email to the recipient's email client.

   - Elaboration
      SMTP, or Simple Mail Transfer Protocol, is the standard protocol for sending emails across the Internet. It works in a series of steps:
      - Connection Setup: The process begins when a client (an email client or another mail server) establishes a TCP connection with the SMTP server. This is typically on port 25, or port 587 for submissions.
      - SMTP Greeting: Once the connection is established, the SMTP server sends a greeting message to the client to confirm that it is ready to start the email transaction.
      - Email Submission: The client then submits the email to the SMTP server. This involves several commands:
      - MAIL FROM:: This command specifies the sender's email address.
      - RCPT TO:: This command specifies the recipient's email address.
      - DATA: This command starts the transfer of the email content. The client sends the email headers (like Subject, From, To), a blank line, and then the email body. The end of the data is indicated by a line containing only a period.
      - Email Queuing: After receiving the email, the SMTP server places it in a message queue for further processing.
      - Email Delivery: The SMTP server then delivers the email to the recipient's SMTP server. It establishes a TCP connection with the recipient's SMTP server and uses the same MAIL FROM, RCPT TO, and DATA commands to transfer the email.
      - Confirmation: After the email is successfully transferred, the recipient's SMTP server sends a confirmation back to the sender's SMTP server.
      - Closing the Connection: Finally, the SMTP servers close the TCP connection, completing the email transaction.
      It's important to note that SMTP is a "push" protocol that does not support fetching email from a server. For that, protocols like POP3 or IMAP are used.
2. **POP3 (Post Office Protocol version 3):** This protocol is used by email clients to retrieve email from a server. Once the email is downloaded to your device, it's deleted from the server. This protocol is useful if you want to save storage space on your mail server, but it means you can only access your email from one device.
   - Working of POP3:
     - The email client connects to the mail server on port 110.
     - The email client authenticates with the mail server using a username and password.
     - The email client downloads the email from the mail server.
     - The email client deletes the email from the mail server.

   - Elaboration
      POP3, or Post Office Protocol version 3, is a protocol for retrieving email from a mail server. It works in a series of steps:
      - Connection Setup: The process begins when a client (an email client) establishes a TCP connection with the POP3 server. This is typically on port 110, or port 995 for POP3 over SSL.
      - Authentication: The client authenticates with the POP3 server using a username and password.
      - Email Download: The client then downloads the email from the POP3 server. This involves several commands:
      - USER: This command specifies the username.
      - PASS: This command specifies the password.
      - LIST: This command lists the emails available on the server.
      - RETR: This command retrieves a specific email from the server.
      - DELE: This command deletes a specific email from the server.
      - QUIT: This command closes the connection.
      - Email Deletion: After downloading the email, the client can delete it from the server using the DELE command.
      - Closing the Connection: Finally, the client closes the TCP connection, completing the email retrieval.
      It's important to note that POP3 is a "pull" protocol that does not support sending email. For that, protocols like SMTP are used.
3. **IMAP (Internet Message Access Protocol):** This protocol is also used by email clients to retrieve email from a server. However, unlike POP3, when you use IMAP, the email stays on the server. This means you can access your email from multiple devices. IMAP also allows you to organize your email on the server, which can be useful if you have a lot of emails to manage.

   - Working of IMAP:
     - The email client connects to the mail server on port 143.
     - The email client authenticates with the mail server using a username and password.
     - The email client downloads the email from the mail server.
     - The email client deletes the email from the mail server.

   - Elaboration
      IMAP, or Internet Message Access Protocol, is a protocol for retrieving email from a mail server. It works in a series of steps:
      - Connection Setup: The process begins when a client (an email client) establishes a TCP connection with the IMAP server. This is typically on port 143, or port 993 for IMAP over SSL.
      - Authentication: The client authenticates with the IMAP server using a username and password.
      - Email Download: The client then downloads the email from the IMAP server. This involves several commands:
      - LOGIN: This command specifies the username and password.
      - LIST: This command lists the emails available on the server.
      - FETCH: This command retrieves a specific email from the server.
      - STORE: This command updates the status of an email on the server.
      - CLOSE: This command closes the connection.
      - Email Deletion: After downloading the email, the client can delete it from the server using the STORE command.
      - Closing the Connection: Finally, the client closes the TCP connection, completing the email retrieval.
      It's important to note that IMAP is a "pull" protocol that does not support sending email. For that, protocols like SMTP are used.
These protocols are used in combination to provide email services. For example, you might use SMTP to send an email and IMAP to receive it. This allows you to send and receive emails from multiple devices and keep them in sync.

## DNS
A domain name server is a computer server that contains a database of public IP addresses and their associated hostnames, and in most cases serves to resolve, or translate, those common names to IP addresses as requested. DNS servers run special software and communicate with each other using special protocols. DNS servers are typically configured with a primary server and one or more secondary servers. The primary server contains the master copy of the DNS zone, while the secondary servers contain read-only copies. The secondary servers are used as backups in case the primary server goes down. The primary server is called a root server.

### DNS lookup/name resolution
DNS lookup is the process of translating a domain name to an IP address. It is a crucial part of the Internet infrastructure, allowing users and applications to access websites by domain name instead of IP address. DNS lookup is typically performed by a DNS server, which is a computer server that contains a database of public IP addresses and their associated hostnames. When a user enters a domain name into a web browser, the browser requests the IP address from the DNS server. The DNS server then looks up the IP address in its database and returns it to the browser. The browser then connects to the IP address and loads the website.

**Extra stuff**
- TTL: Time to live is the time for which the DNS server will cache the IP address of the domain name. This is done to reduce the load on the DNS server and to speed up the process of resolving domain names to IP addresses. The TTL is specified in seconds, and the default value is 86400 seconds (24 hours).
- type a: The A record is used to map a domain name to an IP address. It is the most common type of DNS record and is used for the majority of Internet traffic. For example, the A record for google.com points to the IP address
- type ns: The NS record is used to delegate a DNS zone to a set of name servers. It specifies the authoritative name servers for a DNS zone. For example, the NS record for google.com points to the name servers
- type mx: The MX record is used to specify the mail servers for a DNS zone. It specifies the mail servers that are responsible for accepting email messages for the domain. For example, the MX record for google.com points to the mail servers
- type cname: The CNAME record is used to create an alias for a domain name. It specifies that one domain name is an alias for another domain name. For example, the CNAME record for www.google.com points to google.com.

**DNS protocol, messages**
In the DNS protocol, messages are divided into five sections:
- **Header:** The header contains information about the message, such as the ID, flags, and number of questions, answers, authority records, and additional records.
- **Question:** The question section contains the domain name that is being queried and the type of query (e.g., A, NS, MX, CNAME).
- **Answer:** The answer section contains the resource records that match the query.
- **Authority:** The authority section contains the resource records for the authoritative name servers for the domain.
- **Additional:** The additional section contains additional resource records that may be useful for the client.

### Attacking DNS
- **DDos:** Distributed denial of service attack is a type of attack where multiple compromised systems are used to target a single system causing a denial of service attack. The attack is distributed because the attacker uses multiple systems to launch the attack. The attack is a denial of service attack because the attacker is trying to prevent legitimate users from accessing the service.
- **DNS spoofing/poisoning:** DNS spoofing is a type of attack where the attacker sends fake DNS responses to a client, redirecting them to a malicious website. The attacker can then steal the user's credentials or install malware on their computer.
- **Man in the middle:** Man-in-the-middle attack is a type of attack where the attacker intercepts communication between two parties and impersonates each one. The attacker can then steal sensitive information or modify the communication.


## Multiplexing vs demultiplexing
- Multiplexing is the process of combining multiple signals into a single signal. It is used to increase the amount of data that can be transmitted over a network. Multiplexing is typically done at the physical layer of the OSI model.
- Demultiplexing is the process of separating a single signal into multiple signals. It is used to extract data from a multiplexed signal. Demultiplexing is typically done at the physical layer of the OSI model.
- The header is responsible for arranging the signals into correct order during the process of multiplexing and demultiplexing.
- Working
   - The IP datagrams has the source and the destination location within i
   - Each datagram has one transport layer segment, these segments have enought information to multiplexing and demultiplex the data packets.
   - When host recives the segment it checks for the port number and rearranges accordingly.
- Components for demultiplexing UDP
   - Destination IP addr and port no.


### Connectionless demux
- The UDP header has the source and destination port number.
- The UDP header has the source and destination IP address.
- The UDP header has the length of the UDP datagram.
- The UDP header has the checksum of the UDP datagram.

- What is demux (its nothing just a shortform of demultiplexing)
   - Demultiplexing is the process of separating a single signal into multiple signals. It is used to extract data from a multiplexed signal. Demultiplexing is typically done at the physical layer of the OSI model.

### Connection oriented demux
- The TCP header has the source and destination port number.
- The TCP header has the source and destination IP address.
- The TCP header has the sequence number of the TCP segment.
- The TCP header has the acknowledgment number of the TCP segment.
- The TCP header has the length of the TCP segment.
- The TCP header has the checksum of the TCP segment.

### Subnet mask (extra I guess)
A subnet mask is a 32-bit number that is used to divide an IP address into subnets. It is used to determine which part of the IP address is the network address and which part is the host address. The subnet mask is typically written in dotted decimal notation, such as


### Port numbers
Port numbers are used to identify specific applications or services on a network. They are typically used in conjunction with IP addresses, which identify the host on the network. Port numbers are divided into three ranges:
- **Well-known ports:** These ports are reserved for specific applications or services. For example, port 80 is reserved for HTTP traffic, port 443 is reserved for HTTPS traffic, and port 25 is reserved for SMTP traffic.
- **Registered ports:** These ports are assigned by the Internet Assigned Numbers Authority (IANA) to specific applications or services. For example, port 22 is assigned to SSH, port 53 is assigned to DNS, and port 110 is assigned to POP3.
- **Dynamic ports:** These ports are not assigned to any specific application or service. They are used by the operating system for ephemeral ports, which are temporary ports used for communication between two hosts.



### Client server vs P2P file distribution time
- Client server file distribuiton time can be calculated by the following formula
   $$
   Tcs = max{F/u, F/dmin}
   $$
   where F is the file size, u is the server upload rate, and dmin is the minimum of the client download rates.
- P2P file distribution time can be calculated by the following formula
   $$
   Tp2p = max{F/us, F/dmin}
   $$
   where F is the file size, us is the server upload rate, and dmin is the minimum of the client download rates.

## TCP vs UDP

### **TCP**: Transmission Control Protocol
TCP stands for Transmission Control Protocol. It is a connection-oriented protocol that works on the transport layer of the OSI model. It is used for applications that require high reliability and transmission time is relatively less critical. It is used for applications such as file transfer, email, remote login, and web browsing. It is also used for DNS and DHCP. It is slower than UDP as it establishes a connection before sending data and guarantees delivery of data. It is also less efficient than UDP as it has a larger header size. However, it is more reliable than UDP as it guarantees delivery of data and has a flow control mechanism. It is also more secure than UDP as it is connection-based. 

- Components of TCP
   - Source Port: The port number of the application on the host sending the data.
   - Destination Port: The port number of the application on the receiving host.
   - Sequence Number: Used to keep track of the bytes sent and arrange them in the correct order.
   - Acknowledgment Number: Used to confirm the receipt of data.
   - Data Offset: Specifies the size of the TCP header.
   - Reserved: Reserved for future use and should be set to zero.
   - Flags: Control bits used to indicate specific requests or actions (SYN, ACK, FIN, RST, PSH, URG).
   - Window Size: Specifies the size of the sender's receive window (the buffer space available for incoming data).
   - Checksum: Used to check for errors in the header.
   - Urgent Pointer: Points to the sequence number of the byte following the urgent data.
   - Options: Used for optional settings like Maximum Segment Size (MSS), window scaling, selective acknowledgments, etc.
   - Padding: Ensures that the header ends and data begins on a 32 bit boundary.


### **UDP**: User Datagram Protocol
Udp stands for user datagram protocol. It is a connectionless protocol that works on the transport layer of the OSI model. It is used for applications that require fast transmission time and the transmission of data is more critical than reliability. It is used for applications such as video streaming, online gaming, and VoIP. It is also used for DNS and DHCP. It is faster than TCP as it does not establish a connection before sending data and does not guarantee delivery of data. It is also more efficient than TCP as it has a smaller header size. However, it is less reliable than TCP as it does not guarantee delivery of data and does not have a flow control mechanism. It is also less secure than TCP as it is connectionless. The applications of UDP

- Components of UDP
   - Source port no.
   - Destination port no.
   - Length
   - Checksum - **16bit int** to detect errors 

### Differences
| Srno | TCP | UDP |
|------|-----|-----|
| 1 | TCP is a connection-oriented protocol. | UDP is a connectionless protocol. |
| 2 | TCP is reliable as it guarantees delivery of data to the destination router. | UDP is unreliable as it does not guarantee delivery of data to the destination router. |
| 3 | TCP is slower than UDP. | UDP is faster than TCP. |
| 4 | TCP is heavy-weighted. | UDP is lightweight. |
| 5 | TCP is used for applications that require high reliability and transmission time is relatively less critical. | UDP is used for applications that require fast transmission time and the transmission of data is more critical than reliability. |
| 6 | TCP segments are retransmitted if lost. | UDP datagrams are not retransmitted if lost. |
| 7 | TCP has a flow control mechanism. | UDP does not have a flow control mechanism. |
| 8 | TCP is comparatively less efficient. | UDP is comparatively more efficient. |
| 9 | TCP is comparatively more secure as it is connection-based. | UDP is comparatively less secure as it is connectionless. |
| 10 | TCP header size is 20 bytes. | UDP Header size is 8 bytes. |

## Congestion control
Congestion control is a set of techniques used to prevent congestion in a network. It is used to ensure that the network is operating at an optimal level and that the network is not overloaded. Congestion control is typically implemented at the network layer of the OSI model. It is used to prevent congestion in the network by controlling the rate at which packets are sent. It is also used to prevent congestion in the network by controlling the rate at which packets are sent. It is also used to prevent congestion in the network by controlling the rate at which packets are sent. It is also used to prevent congestion in the network by controlling the rate at which packets are sent. It is also used to prevent congestion in the network by controlling the rate at which packets are sent. It is also used to prevent congestion in the network by controlling the rate at which packets are sent. It is also used to prevent congestion in the network by controlling the rate at which packets are sent. It is also used to prevent congestion in the network by controlling the rate at which packets are sent. It is also used to prevent congestion in the network by controlling the rate at which packets are sent. It is also used to prevent congestion in the network by controlling the rate at which packets are sent.

### TCP 3 way handshake
- TCP 3 way handshake in TCP sender\
   The TCP 3-way handshake is a process used to establish a reliable connection between two devices over a network, such as the internet. It's a fundamental concept in networking and it ensures that both devices are ready to communicate before any data is sent.

   Here's a breakdown of the steps involved in the TCP 3-way handshake:

   1. **Client initiates the connection:** The client sends a TCP segment with the SYN (Synchronize) flag set. This flag tells the server that the client is interested in starting a connection and includes a sequence number that the client will use to track the data it sends.
   2. **Server acknowledges and synchronizes:** The server responds to the client's SYN segment with a TCP segment that has both the SYN and ACK (Acknowledge) flags set. The SYN flag tells the client that the server is willing to establish a connection, and the ACK flag acknowledges the client's sequence number. The server also includes its own sequence number in this segment.
   3. **Client acknowledges server's sequence number:** The client sends a final TCP segment with only the ACK flag set. This segment acknowledges the server's sequence number.

   Once the 3-way handshake is complete, the connection is established and data can be sent in both directions.

- TCP 3 way handshake reciever\
   The process begins with the client sending a FIN (Finish) segment to the server. This segment tells the server that the client is finished sending data and wants to close the connection.

   The server acknowledges the FIN segment from the client with an ACK (Acknowledge) segment. This segment tells the client that the server has received the FIN segment and is now waiting to close its own side of the connection.

   The server then sends its own FIN segment to the client. This segment tells the client that the server is also finished sending data and wants to close the connection.

   The client acknowledges the server's FIN segment with an ACK segment. This segment tells the server that the client has received the FIN segment and is now closing its own side of the connection.

   Once both the client and server have acknowledged each other's FIN segments, the connection is closed.

   The diagram also shows the different states that the client and server can be in during the connection closing process. The client can be in the FIN_WAIT_1, FIN_WAIT_2, CLOSING_WAIT, LAST_ACK, and TIME_WAIT states. The server can be in the CLOSE_WAIT, LAST_ACK, and TIME_WAIT states.

   Here's a more detailed explanation of each state:

   1. * **FIN_WAIT_1:** The client has sent a FIN segment to the server, but has not yet received an acknowledgment.
   2. * **FIN_WAIT_2:** The client has received an acknowledgment of its FIN segment from the server, but has not yet sent its own acknowledgment of the server's FIN segment.
   3. * **CLOSING_WAIT:** The server has sent a FIN segment to the client, but has not yet received an acknowledgment.
   4. * **LAST_ACK:** The server has received an acknowledgment of its FIN segment from the client, and has sent its own acknowledgment of the client's FIN segment.
   5. * **TIME_WAIT:** The client or server has sent a FIN segment and is waiting for an acknowledgment, but has not heard back from the other side for a certain period of time. This state is used to ensure that all data has been sent and received before the connection is finally closed.

### RDT
Reliable data transfer is a set of techniques used to get around congestion control in a network. It is used to ensure that the network is operating at an optimal level and that the network is not overloaded. Reliable data transfer is typically implemented at the transport layer of the OSI model. The legacy system is called the RDT 2.0 

$$ Usender = 3L/R \over RTT + L/R $$ 


| Feature        | RDT 2.0                                       | RDT 3.0                                                  |
|----------------|-----------------------------------------------|----------------------------------------------------------|
| Error Handling | Handles lost packets, but not corrupted ones   | Handles both lost and corrupted packets                  |
| Mechanism       | Stop-and-wait ARQ with timeout and retransmission | Pipelining with ACKs and sequence numbers                 |
| Efficiency     | Less efficient due to stop-and-wait nature       | More efficient due to pipelining                         |
| Complexity      | Simpler implementation                          | More complex implementation due to sequence numbering    |
| Sliding Window | Not used                                       | Uses a sliding window to allow multiple packets in transit |
| Timeout       | Longer timeouts to accommodate for potential corruption | Shorter timeouts as corruption is handled separately    |

**Key Points:**

- **RDT 2.0** is a basic reliable data transfer protocol that addresses packet loss using stop-and-wait ARQ. It retransmits lost packets based on timeouts.
- **RDT 3.0** enhances RDT 2.0 by incorporating mechanisms to handle both lost and corrupted packets. It uses sequence numbers and acknowledgments to enable pipelining, improving efficiency.
- **Sliding window** in RDT 3.0 allows multiple packets to be in transit simultaneously, boosting throughput.
- **Timeouts** in RDT 3.0 are typically shorter than in RDT 2.0, as corruption is handled separately.

**In essence, RDT 3.0 offers more robust and efficient data transfer by addressing both packet loss and corruption, as well as employing pipelining to enhance performance.**


### Go back n
Go-back-N is a type of automatic repeat request (ARQ) protocol used in communication networks. It is used to ensure that the network is operating at an optimal level and that the network is not overloaded. Go-back-N is typically implemented at the data link layer of the OSI model. It is used to ensure that the network is operating at an optimal level and that the network is not overloaded. Go-back-N is typically implemented at the data link layer of the OSI model. It is used to ensure that the network is operating at an optimal level and that the network is not overloaded. Go-back-N is typically implemented at the data link layer of the OSI model. It is used to ensure that the network is operating at an optimal level and that the network is not overloaded. Go-back-N is typically implemented at the data link layer of the OSI model. It is used to ensure that the network is operating at an optimal level and that the network is not overloaded. Go-back-N is typically implemented at the data link layer of the OSI model. It is used to ensure that the network is operating at an optimal level and that the network is not overloaded. Go-back-N is typically implemented at the data link layer of the OSI model. It is used to ensure that the network is operating at an optimal level and that the network is not overloaded.

### Selective repeat
Selective repeat is a type of automatic repeat request (ARQ) protocol used in communication networks. It is used to ensure that the network is operating at an optimal level and that the network is not overloaded. Selective repeat is typically implemented at the data link layer of the OSI model. It is used to ensure that the network is operating at an optimal level and that the network is not overloaded. Selective repeat is typically implemented at the data link layer of the OSI model. It is used to ensure that the network is operating at an optimal level and that the network is not overloaded. Selective repeat is typically implemented at the data link layer of the OSI model. It is used to ensure that the network is operating at an optimal level and that the network is not overloaded. Selective repeat is typically implemented at the data link layer of the OSI model. It is used to ensure that the network is operating at an optimal level and that the network is not overloaded. Selective repeat is typically implemented at the data link layer of the OSI model. It is used to ensure that the network is operating at an optimal level and that the network is not overloaded.

**Note:*** Whenever a network transmission happens there are two kinds of actions that can be initiated by the computer. **ACK** and **NAK** stands for acknolwedgement and negative acknowledgement respectively. ACK is sent when the packet is recieved and NAK is sent when the packet is not recieved. The sender sends the packet again when the NAK is recieved. This is continuously done between the two or more computers that are actively participating in netork transmission.


## IPV4 network layer protocol
IPv4 is the fourth version of the Internet Protocol (IP). It is used to identify devices on a network and route traffic between them. IPv4 addresses are 32-bit numbers that are typically expressed in dotted decimal notation, such as

- Functions of ip (internet protocol)
   - **Addressing:** IP addresses are used to identify devices on a network. They are typically expressed in dotted decimal notation, such as
   - **Datagram:** IP uses datagrams to send data over a network. A datagram is a self-contained unit of data that contains the source and destination addresses, as well as the data being transmitted.
   - **Packet handling conventions:** IP uses packet handling conventions to route packets between devices on a network.

- IP datagram format
   - **Version:** This field specifies the version of IP being used. It is typically set to 4 for IPv4.
   - **Header Length:** This field specifies the length of the IP header in 32-bit words. It is typically set to 5 for IPv4.
   - **Type of Service:** This field specifies the type of service requested by the sender. It is typically set to 0 for IPv4.
   - **Total Length:** This field specifies the total length of the IP datagram, including the header and data. It is typically set to 20 bytes for IPv4.
   - **Identification:** This field specifies a unique identifier for the IP datagram. It is typically set to 0 for IPv4.
   - **Flags:** This field specifies whether the IP datagram can be fragmented. It is typically set to 0 for IPv4.
   - **Fragment Offset:** This field specifies the offset of the IP datagram in the original packet. It is typically set to 0 for IPv4.
   - **Time to Live:** This field specifies the maximum number of hops that the IP datagram can take before being discarded. It is typically set to 64 for IPv4.
   - **Protocol:** This field specifies the protocol used in the data portion of the IP datagram. It is typically set to 6 for TCP and 17 for UDP.
   - **Header Checksum:** This field specifies the checksum of the IP header. It is typically set to 0 for IPv4.
   - **Source Address:** This field specifies the IP address of the sender. It is typically set to

## Subnet
A subnet is a logical subdivision of an IP network. It is used to divide a large network into smaller networks.

### DHCP
Dynamic Host Configuration Protocol (DHCP) is a network protocol used to dynamically assign IP addresses to devices on a network. It is used to ensure that the network is operating at an optimal level and that the network is not overloaded. DHCP is typically implemented at the **application layer** of the OSI model. 

### NAT: Network Address Translation
Network Address Translation (NAT) is a technique used to translate private IP addresses to public IP addresses. It is used to ensure that the network is operating at an optimal level and that the network is not overloaded. NAT is typically implemented at the **network layer** of the OSI model. 

## IPV6
IPv6 is the sixth version of the Internet Protocol (IP). It is used to identify devices on a network and route traffic between them. IPv6 addresses are 128-bit numbers that are typically expressed in hexadecimal notation.

### IpV6 datagram format
- **Version:** This field specifies the version of IP being used. It is typically set to 6 for IPv6.
- **Traffic Class:** This field specifies the type of service requested by the sender. It is typically set to 0 for IPv6.
- **Flow Label:** This field specifies the flow label for the IP datagram. It is typically set to 0 for IPv6.
- **Payload Length:** This field specifies the length of the IP datagram, including the header and data. It is typically set to 40 bytes for IPv6.
- **Next Header:** This field specifies the protocol used in the data portion of the IP datagram. It is typically set to 6 for TCP and 17 for UDP.
- **Hop Limit:** This field specifies the maximum number of hops that the IP datagram can take before being discarded. It is typically set to 64 for IPv6.
- **Source Address:** This field specifies the IP address of the sender. It is typically set to
- **Destination Address:** This field specifies the IP address of the receiver. It is typically set to
- **Data:** This field contains the data being transmitted.

## MAC address
A MAC address is a unique identifier assigned to a network interface controller (NIC). It is used to identify devices on a network and route traffic between them. MAC addresses are typically expressed in hexadecimal notation, such as

### MAC protocols taxonomy
The three broad classes are
- Channel partitioning protocols
   - TDMA: time division multiple access
   - FDMA: frequency division multiple access
- Random access protocols
   - Slotted ALOHA: How it works? The sender sends the data in the slot and the reciever recieves the data in the slot. If the data is recieved then the sender sends the data in the next slot. If the data is not recieved then the sender sends the data in the same slot. The reciever sends the acknolwedgement in the next slot. If the acknolwedgement is recieved then the sender sends the data in the next slot. If the acknolwedgement is not recieved then the sender sends the data in the same slot. Efficiency?
   - ALOHA: How it works? The sender sends the data in the slot and the reciever recieves the data in the slot. If the data is recieved then the sender sends the data in the next slot. If the data is not recieved then the sender sends the data in the same slot. The reciever sends the acknolwedgement in the next slot. If the acknolwedgement is recieved then the sender sends the data in the next slot. If the acknolwedgement is not recieved then the sender sends the data in the same slot. Efficiency?
- Taking turns protocols

### Multiple access links
A multiple access link is a link that connects multiple devices to a network. It is used to ensure that the network is operating at an optimal level and that the network is not overloaded. Multiple access links are typically implemented at the **physical layer** of the OSI model.

There are two types of links:
- **Point-to-point links:** These links connect two devices directly. They are typically implemented using a single cable.
- **Broadcast links:** These links connect multiple devices to a network. They are typically implemented using a shared medium, such as a wireless network or a coaxial cable.

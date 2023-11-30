+++
title = 'Computer networks'
date = 2023-11-23T12:50:11+05:30
draft = false
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

## Termworks
1. RSA encryption
	```py
	import random
	import math
	# Function to check if a number is prime
	def is_prime(num):
		if num <= 1:
			return False
		for i in range(2, int(math.sqrt(num)) + 1):
			if num % i == 0:
				return False
		return True
	# Function to generate random prime numbers
	def generate_prime(bits):
		while True:
			num = random.getrandbits(bits)
			if is_prime(num):
				return num
	# Function to compute the greatest common divisor (GCD)
	def gcd(a, b):
		while b:
			a, b = b, a % b
		return a

	# Function to find the modular multiplicative inverse
	def mod_inverse(a, m):
		m0, x0, x1 = m, 0, 1
		while a > 1:
			q = a // m
			m, a = a % m, m
			x0, x1 = x1 - q * x0, x0
		return x1 + m0 if x1 < 0 else x1
	# Function to generate RSA key pairs
	def generate_key_pair(bits):
		p = generate_prime(bits)
		q = generate_prime(bits)
		n = p * q
		phi = (p - 1) * (q - 1)
		while True:
			e = random.randint(2, phi - 1)
			if gcd(e, phi) == 1:
				break
		d = mod_inverse(e, phi)
		public_key = (n, e)
		private_key = (n, d)
		return public_key, private_key
	# Function to encrypt a message
	def encrypt(public_key, message):
		n, e = public_key
		cipher_text = [pow(ord(char), e, n) for char in message]
		return cipher_text

	# Function to decrypt a message
	def decrypt(private_key, cipher_text):
		n, d = private_key
		decrypted_message = ''.join([chr(pow(char, d, n)) for char in cipher_text])
		return decrypted_message
	# Main program
	if __name__ == "__main__":
		bits = 8  # Adjust the number of bits for your desired security level
		public_key, private_key = generate_key_pair(bits)
		print(f" Generated Public Key : {public_key} \n Generated Private Key : {private_key}")
		message = eval(input(" Enter the Message to be Encrypted : "))
		print(" Original message:", message)
		encrypted_message = encrypt(public_key, message)
		print(" Encrypted message:", encrypted_message)
		decrypted_message = decrypt(private_key, encrypted_message)
		print(" Decrypted message:", decrypted_message) 
	```

2. TCP in python \
	Running this code \
	Required packages: `socket`, (pre-installed on python3.10 ubuntu)
	run `python3 server.py` and `python3 client.py` in individual shells to start the program. Then pass the message to the client shell in quotes.

	- Contents of `tcp_client.py`
		```py
		import socket
		client_socket=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
		server_address=('localhost',12345)
		client_socket.connect(server_address)

		try:
			message=eval(input("Enter message:"))
			client_socket.sendall(message.encode())

		finally:
			client_socket.close()
		```

	- Contents of `tcp_server.py`
		```py
		import socket

		server_socket=socket.socket(socket.AF_INET,socket.SOCK_STREAM)

		server_address=('localhost',12345)
		server_socket.bind(server_address)

		server_socket.listen(5)

		print("TCP server is waiting for connections....")

		while True:
			client_socket,client_address=server_socket.accept()
			print(f'connected to{client_address}')

			try:
				data=client_socket.recv(1024)
				if data:
					print(f'Recieved data:{data.decode()}')
				else:
					break
			finally:
				client_socket.close()

		```
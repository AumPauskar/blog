+++
title = 'Lab expriments and termworks'
date = 2023-12-16T17:44:08+05:30
draft = false
+++

# Lab expriments and termworks

## Computer Networks lab
### Template
1. Title of the experiment 
2. Objective of the experiment
3. Brief theory about the experiment
4. Algorithm & Program
5. Sample input/output with calculations if necessary
6. Course Learning Outcome
7. Conclusion
8. References

### Termwork 1 (not included)
- Title of the experiment 
- Objective of the experiment
- Brief theory about the experiment
- Algorithm & Program
- Sample input/output with calculations if necessary
- Course Learning Outcome
- Conclusion
- References
	1. James F Kurose and Keith W Ross, Computer Networking, A Top-Down Approach, Sixth	edition, Pearson,2017 .
	2. Larry L Peterson and Bruce S Davie, Computer Networks, fifth edition, ELSEVIER

### Termwork 2
- Title of the experiment\
Write a program to implement RSA algorithm
- Objective of the experiment
	- To implement RSA algorithm
	- To understand the basic concepts of cryptography
	- To understand network encryption
- Brief theory about the experiment

RSA (Rivest-Shamir-Adleman) is one of the first public-key cryptosystems and is widely used for secure data transmission. The algorithm involves three steps: key generation, encryption, and decryption.

- **Key Generation:** The key generation process in RSA involves the following steps:

	1. Choose two distinct prime numbers p and q. These should be chosen randomly and kept secret.
	2. Compute n = p*q. n is the modulus for both the public and private keys.
	3. Compute the totient function φ(n) = (p-1)*(q-1).
	4. Choose an integer e such that 1 < e < φ(n) and gcd(e, φ(n)) = 1. e is the public key exponent.
	5. Compute d to satisfy the congruence relation d*e ≡ 1 (mod φ(n)). d is the private key exponent.

The public key consists of (e, n) and the private key is (d, n).

- Encryption: The encryption process in RSA is as follows:
	1. Represent the data as an integer m in [0, n-1].
	2. Compute the ciphertext c using the formula c = m^e mod n.
- Decryption: The decryption process in RSA is as follows:
	1. Compute the original message m using the formula m = c^d mod n.

The security of RSA relies on the fact that, given the public key (e, n), it's computationally infeasible to calculate d, unless p and q are known. This is known as the RSA problem. The RSA problem is equivalent to factoring the product of two primes, which is believed to be a hard problem in number theory.

- Algorithm & Program
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
- Sample input/output with calculations if necessary
- Course Learning Outcome
	- Understand the basic concepts of cryptography
	- Understand network encryption
	- Understand the basic concepts of RSA algorithm
- Conclusion
- References
	1. James F Kurose and Keith W Ross, Computer Networking, A Top-Down Approach, Sixth 
	edition, Pearson,2017 .
	2. Larry L Peterson and Bruce S Davie, Computer Networks, fifth edition, ELSEVIER

### Termwork 3
- Title of the experiment\
Write a program to implement UDP client server communication
- Objective of the experiment
	- To implement UDP client server communication
	- To understand the basic concepts of UDP
	- To understand the basic concepts of client server communication
- Brief theory about the experiment

	User Datagram Protocol (UDP) is a transport layer protocol that is used for fast and connectionless transmission of data. Here's the basic theory:
	- Connectionless: Unlike TCP, UDP is a connectionless protocol. This means that it doesn't establish a connection before sending data, it just sends it directly.
	- No Guarantee of Delivery: UDP does not guarantee delivery of data. If a packet is lost in the network, UDP does not know about it and does not retransmit the lost packets.
	- No Congestion Control: UDP does not have a congestion control mechanism. It continues to send data at the same rate even if the network is congested.
	- No Ordering of Data: UDP does not order the packets. The packets might be received in a different order than they were sent.
	- Faster: Because of the lack of these features (connection setup, guarantee of delivery, congestion control, ordering of data), UDP is faster than TCP. It is often used in real-time applications like video streaming and online gaming where speed is more important than reliability.
	- Header: The UDP header is simpler than the TCP header, consisting only of source port, destination port, length, and checksum.
	- Datagram: The data units in UDP are called datagrams. Each datagram is independent of others.

	Remember, while UDP is faster, it should only be used in situations where the loss of some data is acceptable.

- Algorithm & Program
	- Server code
		```py
		# Server (server.py)

		import socket

		def start_udp_server():
			# Create a UDP socket
			server_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

			# Bind the socket to a specific address and port
			server_address = ('localhost', 12345)
			server_socket.bind(server_address)

			print(f"Server listening on {server_address}")

			while True:
				# Wait for a message from the client
				data, client_address = server_socket.recvfrom(1024)
				print(f"Received message from {client_address}: {data.decode()}")

				# Send the same message back to the client
				server_socket.sendto(data, client_address)

		if __name__ == "__main__":
			start_udp_server()
		```

	- Client code
		```py
		# Client (client.py)

		import socket

		def start_udp_client():
			# Create a UDP socket
			client_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

			# Server address and port
			server_address = ('localhost', 12345)

			while True:
				# Get user input for the message
				message = input("Enter message to send (or 'exit' to quit): ")

				if message.lower() == 'exit':
					break

				# Send the message to the server
				client_socket.sendto(message.encode(), server_address)

				# Receive the response from the server
				data, _ = client_socket.recvfrom(1024)
				print(f"Received response from server: {data.decode()}")

			# Close the socket when done
			client_socket.close()

		if __name__ == "__main__":
			start_udp_client()
		```
- Sample input/output with calculations if necessary
- Course Learning Outcome
	- Understand the basic concepts of UDP
	- Understand the basic concepts of client server communication
- Conclusion\
In conclusion, the UDP client-server program efficiently establishes a connection between the client and server and transfers data between them. The code demonstrates key concepts such as socket programming, connection establishment, data transfer, and connection termination.
- References
	1. James F Kurose and Keith W Ross, Computer Networking, A Top-Down Approach, Sixth edition, Pearson,2017.
	2. Larry L Peterson and Bruce S Davie, Computer Networks, fifth edition, ELSEVIER

### Termwork 4
- Title of the experiment\
Write a program to implement TCP client server communication
- Objective of the experiment
	- To implement TCP client server communication
	- To understand the basic concepts of TCP
	- To understand the basic concepts of client server communication
- Brief theory about the experiment

	In a TCP client-server model, the server listens for incoming client requests by binding to a specific address and port, often on a host with a known IP address. The client makes a connection request to the server to initiate communication.

	1. **Connection Establishment (Three-Way Handshake):** The client initiates the connection by sending a SYN (synchronize) message to the server. The server acknowledges this by sending back a SYN-ACK (synchronize-acknowledge) message. Finally, the client sends an ACK (acknowledge) message back to the server, and the connection is established.
	2. **Data Transfer:** Once the connection is established, bytes can be sent from the client to the server and from the server to the client. The sent data is broken down into TCP segments at the source, then reassembled back into the original data at the destination.
	3. **Connection Termination (Four-Way Handshake):** Either the client or server can initiate the connection termination process. The initiating side sends a FIN (finish) message, to which the other side responds with an ACK. Then, the side that received the initial FIN sends its own FIN, which the initiating side acknowledges with an ACK.
	4. **Reliability:** TCP provides reliable delivery of data through the use of sequence numbers and acknowledgments. If the sender does not receive an acknowledgment for a particular segment within a specified time, it retransmits the segment.
	5. **Flow Control:** TCP uses a sliding window for flow control, which allows the receiver to control the amount of data sent by the sender.
	6. **Congestion Control:** TCP uses various mechanisms like slow start, congestion avoidance, fast retransmit, and fast recovery to control network congestion.

	The TCP client-server model is widely used in the internet protocol suite and forms the foundation of web browsing, email, file transfers, and other network communication.

- Algorithm & Program
	- Server code
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

	- Client code
		```py
		#tcp client

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

- Sample input/output with calculations if necessary
- Course Learning Outcome
	- Understand the basic concepts of TCP
	- Understand the basic concepts of client server communication
- Conclusion\
In conclusion, the TCP client-server program efficiently establishes a connection between the client and server and transfers data between them. The code demonstrates key concepts such as socket programming, connection establishment, data transfer, and connection termination.
- References
	1. James F Kurose and Keith W Ross, Computer Networking, A Top-Down Approach, Sixth	edition, Pearson,2017.
	2. Larry L Peterson and Bruce S Davie, Computer Networks, fifth edition, ELSEVIER

### Termwork 5 - distance vector routing
- Title of the experiment\
To implement distance vector routing algorithm
- Objective of the experiment
	- To implement distance vector routing algorithm
	- To find the shortest path between two nodes
- Brief theory about the experiment

	Distance Vector Routing is a routing protocol that uses distance to decide the best packet forwarding path. Distance Vector Routing is also known as Bellman-Ford algorithm or Ford-Fulkerson algorithm. Here's the basic theory:

	- **Routing Information:** Each router in the network maintains a routing table that stores the shortest distance and the line to use to reach each network node. The distance is measured in terms of a metric such as the number of hops.
	- **Information Sharing:** Each router periodically shares its routing table with its immediate neighbors. The neighbors then update their own routing tables based on the information received.
	- **Route Updates:** When a router receives a routing table from a neighbor, it calculates the shortest path to every other router and updates its own table if a shorter path is found. This is done by adding the cost to the neighbor to the cost from the neighbor to all other nodes.
	- **Convergence:** The process of sharing and updating routing information continues until all routers' tables are consistent with each other. This state is known as convergence.
	- **Route Changes:** If a router detects a change in the network (like a link failure), it updates its routing table and broadcasts the change to its neighbors. This triggers another round of updates and convergence.

	One of the main drawbacks of Distance Vector Routing is that it can take a long time to converge, especially in large networks. It's also prone to "counting to infinity" problems in the case of a network failure. These issues are mitigated in more advanced protocols like Link State Routing.

- Algorithm & Program
	```py
	import sys

	class Graph:
		def __init__(self, vertices):
			self.V = vertices
			self.graph = [[0 for column in range(vertices)] for row in range(vertices)]

		def min_distance(self, dist, spt_set):
			min_dist = sys.maxsize
			min_index = -1

			for v in range(self.V):
				if dist[v] < min_dist and spt_set[v] == False:
					min_dist = dist[v]
					min_index = v

			return min_index

		def dijkstra(self, src):
			dist = [sys.maxsize] * self.V
			dist[src] = 0
			spt_set = [False] * self.V

			for _ in range(self.V):
				u = self.min_distance(dist, spt_set)
				spt_set[u] = True

				for v in range(self.V):
					if (
						self.graph[u][v] > 0
						and spt_set[v] == False
						and dist[v] > dist[u] + self.graph[u][v]
					):
						dist[v] = dist[u] + self.graph[u][v]

			print("Vertex \t Distance from Source")
			for node in range(self.V):
				print(f"{node} \t\t {dist[node]}")

	# Example usage
	g = Graph(9)
	g.graph = [
		[0, 4, 0, 0, 0, 0, 0, 8, 0],
		[4, 0, 8, 0, 0, 0, 0, 11, 0],
		[0, 8, 0, 7, 0, 4, 0, 0, 2],
		[0, 0, 7, 0, 9, 14, 0, 0, 0],
		[0, 0, 0, 9, 0, 10, 0, 0, 0],
		[0, 0, 4, 14, 10, 0, 2, 0, 0],
		[0, 0, 0, 0, 0, 2, 0, 1, 6],
		[8, 11, 0, 0, 0, 0, 1, 0, 7],
		[0, 0, 2, 0, 0, 0, 6, 7, 0],
	]

	g.dijkstra(0)
	```
- Sample input/output with calculations if necessary
- Course Learning Outcome
	- To understand the basic concepts of distance vector routing
	- To understand the basic concepts of routing
	- To understand network optimization
- Conclusion\
In conclusion, the distance vector routing program efficiently finds the shortest path between two nodes in a network. The code demonstrates key concepts such as graph representation, Dijkstra's algorithm, and shortest path calculation.
- References
	1. James F Kurose and Keith W Ross, Computer Networking, A Top-Down Approach, Sixth	edition, Pearson,2017.
	2. Larry L Peterson and Bruce S Davie, Computer Networks, fifth edition, ELSEVIER

### Termwork 6 - leaky bucket
- Title of the experiment \
Demonstrate leaky bucket algorithm
- Objective of the experiment
	- To demonstrate rate limiting
	- To demonstrate traffic shaping
	- To demonstrate congestion control
- Brief theory about the experiment \
	The Leaky Bucket Algorithm is a method used in networking to manage and control the rate of data transmission. It's used for traffic shaping, rate limiting, and congestion control. The algorithm works similarly to a literal leaky bucket.

	Imagine a bucket with a small hole at the bottom. Water (representing data packets) is poured into the bucket at varying rates. The water leaks from the hole at a constant rate. If the water is poured too quickly, the bucket overflows, representing data loss. If the water is poured too slowly, the bucket will eventually empty, representing idle capacity.

	In the context of data transmission:

	1. **Bucket Size**: This represents the buffer memory. If data arrives too fast and the buffer gets full, incoming data is discarded or 'spilled'.
	2. **Leak Rate**: This represents the rate at which the data packets are sent. It's constant and does not change based on the incoming data rate.
	3. **Overflow**: If data comes in at a rate that's too fast for the leak rate to handle, and the buffer is full, the incoming data is discarded.
	4. **Idle Time**: If data comes in at a rate that's slower than the leak rate, there will be times when there are no data packets to send.

	The Leaky Bucket Algorithm helps to smooth out bursty traffic, limit the data transmission rate, and control congestion, ensuring that the network can handle the data flow.

- Algorithm & Program
	```py
	# LEAKY BUCKET

	import time

	class LeakyBucket:
		def __init__(self, capacity, rate):
			self.capacity = capacity  # Maximum bucket size
			self.rate = rate  # Rate at which the bucket leaks tokens
			self.tokens = 0  # Current number of tokens in the bucket
			self.last_time = time.time()

		def add_token(self):
			current_time = time.time()
			time_elapsed = current_time - self.last_time
			self.tokens = min(self.capacity, self.tokens + time_elapsed * self.rate)
			self.last_time = current_time

		def transmit(self, packet_size):
			if self.tokens >= packet_size:
				self.tokens -= packet_size
				print(f"Transmitted {packet_size} bytes")
				return True
			else:
				print("Dropped - Insufficient tokens")
				return False

	if __name__ == "__main__":
		bucket = LeakyBucket(capacity=50, rate=10)  # Example: 50 bytes capacity, 10 bytes/second rate

		for i in range(1, 11):
			print(f"Time: {i} seconds")
			bucket.add_token()
			packet_size = eval(input(" Enter the Packet size : "))  # Example: 15 bytes packet size
			bucket.transmit(packet_size)
	```
- Sample input/output with calculations if necessary
- Course Learning Outcome
	1. **Understanding of the Leaky Bucket Algorithm**: Students will gain a deep understanding of the Leaky Bucket Algorithm, including its purpose, how it works, and where it is used in computer networks.
	2. **Practical Implementation of the Leaky Bucket Algorithm**: Students will learn how to implement the Leaky Bucket Algorithm in code, giving them practical experience in network programming.
	3. **Understanding of CRC (Cyclic Redundancy Check)**: Students will learn about CRC, a popular method for detecting errors in data transmission. They will understand how it works and how to implement it in code.
- Conclusion \
	In conclusion, the Leaky Bucket Algorithm is a fundamental concept in computer networks that plays a crucial role in managing data traffic. It helps in smoothing out bursty traffic, controlling the data transmission rate, and preventing network congestion. By implementing this algorithm, students gain practical experience in network programming, enhancing their understanding of how data is managed in real-world networks. This knowledge is essential for anyone looking to delve deeper into the field of computer networks and telecommunications.
- References
	1. James F Kurose and Keith W Ross, Computer Networking, A Top-Down Approach, Sixth	edition, Pearson,2017.
	2. Larry L Peterson and Bruce S Davie, Computer Networks, fifth edition, ELSEVIER

### Termwork 7 - cyclic redundancy check
- Title of the experiment\
To show and demonstrate the use of cyclic redundancy check
- Objective of the experiment\
	- To demonstrate the use of cyclic redundancy check
	- To understand the basic concepts of error detection
- Brief theory about the experiment\
	Cyclic Redundancy Check (CRC) is an error-detecting code commonly used in digital networks and storage devices to detect accidental changes to raw data. Here's the theory behind it:
	1. **Polynomial Codes**: CRC is based on the algebraic structure of polynomial codes over finite fields, specifically the field of two elements, GF(2). Each bitstring corresponds to a polynomial with coefficients in GF(2).
	2. **Division**: The sender treats the data as a polynomial and divides it by a specific polynomial known as the generator polynomial. The remainder of this division is then appended to the data.
	3. **Error Detection**: The receiver performs the same division operation and if the remainder (known as the CRC or checksum) is non-zero, an error is detected.

	The core concepts involved in CRC include:

	1. **Bitwise XOR operation**: The division operation in CRC is performed using bitwise XOR operations.
	2. **Generator Polynomial**: This is a key part of the CRC calculation. It's chosen carefully to maximize the error-detecting capabilities.
	3. **Checksum**: This is the remainder from the division operation. It's appended to the data being sent and used by the receiver to detect errors.

	CRC is used because it's highly effective at detecting errors and it's relatively easy to implement in hardware or software. It's particularly good at detecting common types of errors in networks, like burst errors.
- Algorithm & Program
	```py
	# CRC

	def crc_remainder(input_bitstring, polynomial, initial_fill):
		# Append zeros to the input bitstring (equal to the degree of the polynomial)
		dividend = input_bitstring + '0' * (len(polynomial) - 1)
		dividend = list(dividend)
		polynomial = list(polynomial)

		for i in range(len(input_bitstring)):
			if dividend[i] == '1':
				for j in range(len(polynomial)):
					dividend[i + j] = str(int(dividend[i + j]) ^ int(polynomial[j]))

		# Get the remainder (checksum)
		remainder = ''.join(dividend)[-len(polynomial) + 1:]
		# Append the remainder to the original message
		codeword = input_bitstring + remainder

		return remainder, codeword

	def crc_check(codeword, polynomial):
		# Calculate the remainder using the received codeword and the same polynomial
		remainder, _ = crc_remainder(codeword, polynomial, '0' * (len(polynomial) - 1))
		return remainder == '0' * (len(polynomial) - 1)

	if __name__ == "__main__":
		message = eval(input(" Enter the Message in bit format : "))
		polynomial = eval(input(" Enter the Polynomial divisior in bit format : "))

		remainder, codeword = crc_remainder(message, polynomial, '0' * (len(polynomial) - 1))
		print(" Original Message:", message)
		print(" Polynomial:", polynomial)
		print(" Transmitted Codeword:", codeword)
		print(" Remainder:", remainder)

		print(" Enter the choice \n 1. Error Free Tramsmission \n 2. Simulate Error : ")
		choice = eval(input())

		if choice == 1:
			is_valid = crc_check(codeword, polynomial)
		else:
			# Simulate an error by flipping a bit
			error_position = eval(input("Enter the bit position to introduce Error : "))
			codeword = codeword[:error_position] + ('1' if codeword[error_position] == '0' else '0') + codeword[error_position + 1:]
			print("Received Codeword with Error:", codeword)
			is_valid = crc_check(codeword, polynomial)
								
		if is_valid:
			print("No error detected. The message is valid and the message is : ", codeword)
		else:
			print("Error detected. The message is invalid and the message is : ", codeword)
	```
- Sample input/output with calculations if necessary
- Course Learning Outcome
	- To understand error detection and error mitigation in computer networks
	- To understand the basic concepts of CRC
- Conclusion\
	In conclusion, the CRC program efficiently detects errors in data transmission. The code demonstrates key concepts such as polynomial codes, division, and checksum calculation.
- References
	1. James F Kurose and Keith W Ross, Computer Networking, A Top-Down Approach, Sixth	edition, Pearson,2017.
	2. Larry L Peterson and Bruce S Davie, Computer Networks, fifth edition, ELSEVIER


## Microcontroller lab
### Template
1. Title of the experiment
2. Objective of the experiment
3. Brief theory about the experiment including instructions used in that program with proper syntax
4. Program with comments
5. Sample input/output with calculations if necessary
6. Course Learning Outcome
7. Conclusion
8. References

### Termwork 1a

- Title of the experiment\
Observe the contents of the resister
- Objective of the experiment
To observe the contents of the resister and to understand the basic concepts of ARM assembly language programming
- Brief theory about the experiment including instructions used in that program with proper syntax

	ARM Assembly language is a low-level programming language used for programming ARM processors. It provides direct access to the processor's features and allows precise control over the processor's behavior.

	Here's a brief description of the ARM Assembly instructions and directives you've asked about:

	- `AREA`: This directive is used to define a block of code or data. The syntax is AREA name, type, options. The name is a label that identifies the area. The type can be CODE (for code areas) or DATA (for data areas). The options can include READONLY (the area cannot be written to), ALIGN=n (align the area to a 2^n byte boundary), and others.
	- `ONE`, `CODE`, `READONLY`: In your code, ONE is the name of the area, CODE indicates that this area contains code, and READONLY means that this area cannot be written to.
	- `MOV`: This instruction copies a value into a register. The syntax is MOV Rd, Operand2. Rd is the destination register, and Operand2 is the value to be copied.
	- `ADD`: This instruction adds two values and stores the result in a register. The syntax is ADD Rd, Rn, Operand2. Rd is the destination register, Rn is the first operand, and Operand2 is the second operand.
	- `L BL`: BL is a branch instruction that calls a subroutine. The L label is the target of the branch. The BL instruction also stores the return address in the link register (LR).
	- `END`: This directive marks the end of the assembly file. It's not required in all assemblers, but it's good practice to include it.

- Program with comments
	```asm
		AREA ONE, CODE, READONLY
		ENTRY
		MOV R0, #0X01
		MOV R1, #0X02
		ADD R2, R1, R0

	L	B L
		END
	```
- Sample input/output with calculations if necessary
- Course Learning Outcome
	- Understand the basic concepts of ARM assembly language
	- Understand the basic concepts of ARM assembly language programming
- Conclusion\
In conclusion, the ARM assembly program efficiently adds two numbers and stores the result in a register. The code demonstrates key concepts such as register manipulation, memory access, and conditional branching.
- References
1. Andrew N Sloss, Dominic Symes and Chris Wright, ARM system developers guide, Elsevier, 
Morgan Kaufman publishers, 2008.
2. Shibu K V, “Introduction to Embedded Systems”, Tata McGraw Hill Education, Private Limited, 2nd Edition.

### Termwork 1b
- Title of the experiment\
Develop an assembly language program to transfer a block of data from source to destination.
- Objective of the experiment\
To implement an assembly language program to transfer a block of data from source to destination and to understand the basic concepts of ARM assembly language programming for data processing
- Brief theory about the experiment including instructions used in that program with proper syntax

	In ARM programming, memory is organized into blocks that can be accessed by the processor. Each block has a unique address. The processor can read data from a memory block (load) or write data to a memory block (store).

	- `LOOP`: This is a label that marks the start of a loop. The BNE instruction later in the code branches back to this label to repeat the loop.
	- `LDRH`: This instruction loads a halfword (2 bytes) from memory into a register. The syntax is LDRH Rd, [Rn], #offset. Rd is the destination register, Rn is the base register, and offset is the number of bytes to increment Rn after the load.
	- `STRH`: This instruction stores a halfword (2 bytes) from a register to memory. The syntax is STRH Rd, [Rn], #offset. Rd is the source register, Rn is the base register, and offset is the number of bytes to increment Rn after the store.
	- `SUBS`: This instruction subtracts a value from a register and updates the condition flags. The syntax is SUBS Rd, Rn, #immediate. Rd is the destination register, Rn is the first operand, and immediate is the value to subtract.
	- `BNE`: This instruction branches to a label if the Zero flag is not set (i.e., the last comparison or arithmetic operation did not result in zero). The syntax is BNE label.
	- `FBLOCK`: This is a label that marks the start of a memory block. The DCW directive following this label defines the contents of the block.
	- `DCW`: This directive defines a constant word (4 bytes) in memory. The syntax is DCW value. You can specify multiple values, separated by commas.
	- `SBLOCK`: This is another label that marks the start of a memory block. The DCW directive following this label defines the contents of the block.

- Program with comments
	```asm
		AREA ONE, CODE, READONLY
			ENTRY

			MOV R5, #10
			LDR R0, =FBLOCK   ; Load the address of FBLOCK into R0
			LDR R2, =SBLOCK   ; Load the address of SBLOCK into R2

	LOOP	LDRH R1, [R0], #2  ; Load 2 bytes from the source (increment R0 by 2)
			STRH R1, [R2], #2  ; Store 2 bytes to the destination (increment R2 by 2)
			SUBS R5, R5, #1    ; Subtract 1 from R5
			BNE LOOP           ; Branch back to LOOP if R5 is not zero

	L		B L                ; Infinite loop (useful for preventing the program from falling through)

	FBLOCK DCW 0X1234, 0X5678, 0x2652, 0x1124
		AREA MYDATA, DATA, READWRITE
	SBLOCK DCW 0
	```
- Sample input/output with calculations if necessary
- Course Learning Outcome
	- Understand the basic concepts of loops in ARM assembly language
	- Understanding the basic concepts of ARM assembly language programming for data processing
	- Understanding the concepts of FBLOCK and SBLOCK in ARM assembly language programming for data processing
- Conclusion\
In conclusion, the ARM assembly program efficiently transfers a block of data from source to destination using a loop-based approach. The code demonstrates key concepts such as register manipulation, memory access, and conditional branching.
- References
1. Andrew N Sloss, Dominic Symes and Chris Wright, ARM system developers guide, Elsevier, 
Morgan Kaufman publishers, 2008.
2. Shibu K V, “Introduction to Embedded Systems”, Tata McGraw Hill Education, Private Limited, 2nd Edition.

### Termwork 2
- Title of the experiment\
Write an assembly program to add 16 bit numbers and store the result in internal RAM
- Objective of the experiment\
To implement an assembly program to add 16 bit numbers and store the result in internal RAM and to understand the basic concepts of ARM assembly language programming for data processing
- Brief theory about the experiment including instructions used in that program with proper syntax\
This ARM Assembly code performs the sum of a series of half-word (16-bit) values stored in memory and stores the result in another memory location.

- `LDR R1, =FBLOCK`: This line loads the address of the FBLOCK memory area into register R1.
- `LDR R2, =RESULT`: This line loads the address of the RESULT memory area into register R2
- `LOOP LDRH R3, [R1], #2`: This line starts a loop. It loads a half-word value from the memory address in R1 into register R3, then increments R1 by 2 (to point to the next half-word).
- `ADD R4, R4, R3`: This line adds the value in R3 to the value in R4, storing the result back in R4.
- `BNE LOOP`: If the value in R0 is not zero (i.e., the loop is not finished), this line branches back to the LOOP label.
- `FBLOCK DCW 0X1111, 0X2222, 0X3333, 0X4444, 0X5555, 0X6666, 0X7777`: This line defines a block of memory with the specified half-word values.
- `RESULT DCD 0`: This line defines a word in memory with the initial value 0. This is where the result of the sum is stored.

- Program with comments
	```asm
		AREA THREE, CODE, READONLY
	ENTRY
				MOV R0, #10
				MOV R4, #0000
				LDR R1, =FBLOCK
				LDR R2, =RESULT
	LOOP	LDRH R3, [R1], #2 ; Use LDRH to load a half-word (16-bit) value
				ADD R4, R4, R3
				STR R4, [R2], #4 ; Use post-indexed addressing mode to store the result
				SUBS R0, #1
				BNE LOOP
	L			B L
	FBLOCK DCW 0X1111, 0X2222, 0X3333, 0X4444, 0X5555, 0X6666, 0X7777
				AREA MYDATA, DATA, READWRITE
	RESULT DCD 0
		END
	```
- Sample input/output with calculations if necessary

- Course Learning Outcome
	- Understand various addressing modes in ARM assembly language
	- Understand LDRH instruction in ARM assembly language programming for data processing
	- Understand the concepts of FBLOCK and SBLOCK in ARM assembly language programming for data processing

- Conclusion\
In conclusion, the ARM assembly program efficiently adds a series of half-word values and stores the result in a memory location. The code demonstrates key concepts such as register manipulation, memory access, and conditional branching.
- References
1. Andrew N Sloss, Dominic Symes and Chris Wright, ARM system developers guide, Elsevier, 
Morgan Kaufman publishers, 2008.
2. Shibu K V, “Introduction to Embedded Systems”, Tata McGraw Hill Education, Private Limited, 2nd Edition.

### Termwork 3
- Title of the experiment\
Find the factorial of a number and store the result in internal RAM
- Objective of the experiment\
To implement an assembly language program to find the factorial of a number and store the result in internal RAM
- Brief theory about the experiment including instructions used in that program with proper syntax

	In the provided ARM Assembly code, the factorial of a number is calculated using a loop. The loop starts with the number (in this case, 5) and multiplies it with the result of the previous multiplication (initially set to 1). The number is then decremented by 1, and the process repeats until the number reaches 0.

	Here's a brief description of the MUL instruction in ARM Assembly:

	- `MUL`: This instruction multiplies two registers and stores the result in a third register. The syntax is MUL Rd, Rm, Rs. Rd is the destination register, Rm is the first operand (multiplicand), and Rs is the second operand (multiplier). In the provided code, MUL R3, R2, R1 multiplies the contents of R2 and R1 and stores the result in R3.


- Program with comments
	```asm
		AREA ONE, CODE, READONLY
		ENTRY
			MOV R1, #5	; Set the initial value for the factorial
			MOV R2, #1	; Initialize the result to 1

	L		MUL R3, R2, R1 ; Multiply the result by the current value of R1 and store in R3
			MOV R2, R3      ; Move the result from R3 to R2
			SUBS R1, R1, #1 ; Decrement R1
			BNE L           ; Branch back to L if R1 is not zero

			; At this point, R2 contains the factorial result

			; You can use R2 or store the result in another register/memory location

		END
	```
- Sample input/output with calculations if necessary
- Course Learning Outcome
	- Understanding the MUL intruction in ARM assembly language programming for data processing
	- Understanding the concepts of looping in ARM assembly language programming for data processing
- Conclusion\
In conclusion, the ARM assembly program efficiently calculates the factorial of a number using a loop-based approach. The code demonstrates key concepts such as register manipulation, memory access, and conditional branching.
- References
1. Andrew N Sloss, Dominic Symes and Chris Wright, ARM system developers guide, Elsevier, 
Morgan Kaufman publishers, 2008.
2. Shibu K V, “Introduction to Embedded Systems”, Tata McGraw Hill Education, Private Limited, 2nd Edition.

### Termwork 4
- Title of the experiment\
Write an assembly language program to find the largetst number in an array of 32 bit numbers amd store the result in internal RAM

- Objective of the experiment\
To implement an assembly language program to find the largetst number in an array of 32 bit numbers amd store the result in internal RAM

- Brief theory about the experiment including instructions used in that program with proper syntax\
	In ARM programming, memory is organized into blocks that can be accessed by the processor. Each block has a unique address. The processor can read data from a memory block (load) or write data to a memory block (store).

	The CMP instruction in ARM Assembly compares two values and sets the condition flags based on the result. These flags can then be used by subsequent branch instructions to control the flow of the program.

	Here's a brief description of the ARM Assembly instructions and directives in your code:

	- `LDR`: This instruction loads a word (4 bytes) from memory into a register. The syntax is LDR Rd, [Rn], #offset. Rd is the destination register, Rn is the base register, and offset is the number of bytes to increment Rn after the load.
	- `CMP`: This instruction compares two registers and sets the condition flags based on the result. The syntax is CMP Rn, Operand2. Rn is the first operand, and Operand2 is the second operand.
	- `BHI`: This instruction branches to a label if the last comparison resulted in a higher value (unsigned). The syntax is BHI label.
	- `DCD`: This directive defines a constant doubleword (8 bytes) in memory. The syntax is DCD value. You can specify multiple values, separated by commas.

- Program with comments
	```asm
		AREA ONE, CODE, READONLY
			ENTRY
				MOV R5, #6
				LDR R1, =VALUE1
				LDR R2, [R1], #4
	LOOP
				LDR R4, [R1], #4
				CMP R2, R4
				BHI LOOP1
				MOV R2, R4
	LOOP1 SUBS R5, #1
			BNE LOOP
			LDR R6, =RESULT
			STR R2, [R6]
	L		B L
	VALUE1 DCD 0X44444444, 0X22222222, 0X11111111, 0X22222222, 0XAAAAAAAA, 0X88888888, 0X99999999
		AREA DATA2, DATA, READWRITE
	RESULT DCD 0
		END
	```
- Sample input/output with calculations if necessary

- Course Learning Outcome
	- Understand the basic concepts of ARM assembly language
	- Understand the basic concepts of ARM assembly language programming
	- Understand the basic concepts of ARM assembly language programming for data processing
	- Understand the basic concepts of ARM assembly language programming for data processing using arrays

- Conclusion\
In conclusion, the ARM assembly program efficiently finds the maximum value in an array using a loop-based approach. The code demonstrates key concepts such as register manipulation, memory access, and conditional branching.

- References
1. Andrew N Sloss, Dominic Symes and Chris Wright, ARM system developers guide, Elsevier, 
Morgan Kaufman publishers, 2008.
2. Shibu K V, “Introduction to Embedded Systems”, Tata McGraw Hill Education, Private Limited, 2nd Edition.


### Termwork 5
- Title of the experiment\
Swapping of the digits in ARM assembly language
- Objective of the experiment
	- To understand and implement the use of ARM assembly language for manipulating data stored in memory, specifically for swapping the digits of a number.
	- To gain practical experience with ARM assembly programming concepts such as register manipulation, memory instructions, conditional branching, and loop constructs.
- Brief theory about the experiment including instructions used in that program with proper syntax

	The experiment involves writing an ARM assembly language program to swap the digits of a number. The key concepts involved in this experiment are register manipulation, memory instructions, conditional branching, and loop constructs.
	
	**Instructions**
	- `MOV R8, #4`: Initializes register R8 with the value 4.
	- `LDR R2`, `=CVALUE` and `LDR R3`, `=DVALUE`: Load the addresses of the memory blocks labeled CVALUE and DVALUE into registers R2 and R3, respectively.
	- The `LOOP0` block loads values from the memory blocks pointed to by R2 and R3 into R1, decrementing R8 each time. This loop continues until R8 equals 0.
	- The second `START` block initializes `R5` with 3 and `R7` with 0, and loads the address of `DVALUE` into `R1`.
	- The `LOOP` block loads a value from the memory block pointed to by `R1` into `R2`, compares it with the value in `R3`, and if `R2` is less than `R3`, it jumps to `LOOP2`. If not, it stores `R2` and `R3` into the memory block pointed to by `R1`, sets `R7` to 1, and increments `R1` by 4.
	- The `LOOP2` block decrements `R5` by 1 each time it's executed. If `R5` is not 0, it jumps back to LOOP. If `R5` is 0, it checks if R7 is 0, and if not, it jumps to START1 (which is not defined in the provided code).
	- `NOP` instructions are **no-operation instructions** that do nothing. They're often used for timing purposes or to occupy space that will be replaced with useful instructions later.
	- `CVALUE` and `DVALUE` are memory blocks defined in the code. `CVALUE` contains four 32-bit values, and `DVALUE` is initialized with a single 0.

- Program with comments
	```asm
		AREA ONE, CODE, READONLY
	ENTRY

	START
					MOV R8, #4
					LDR R2, =CVALUE
					LDR R3, =DVALUE
				
	LOOP0
					LDR R1, [R2], #4
					LDR R1, [R3], #4
					
					SUBS R8, R8, #1
					CMP R8, #0
					BNE LOOP0
					
	START1		MOV R5, #3
					MOV R7, #0
					LDR R1, =DVALUE
					
	LOOP		LDR R2, [R1], #4
					CMP R2, R3
					BLT LOOP2
					STR R2, [R1], #-4
					STR R3,[R1]
					MOV R7, #1
					ADD R1, #4
					
	LOOP2
					SUBS R5, R5, #1
					CMP R5, #0
					BNE LOOP
					CMP R7, #0
					BNE START1
			NOP
			NOP
			NOP
			
	CVALUE
				DCD 0X44444444
				DCD 	0X11111111
				DCD 	0X33333333
				DCD 	0X22222222
			
			AREA DATA1, DATA, READWRITE
	DVALUE
				DCD 0X00000000
			END
	```
- Sample input/output with calculations if necessary
- Course Learning Outcome
	- Understand the basic concepts of memory instructions in ARM assembly language
	- Understanding the concepts regarding the swap instructions
- Conclusion\
In conclusion, the ARM assembly program efficiently swaps the digits of a number using a loop-based approach. The code demonstrates key concepts such as register manipulation, memory access, and conditional branching.
- References
	1. Andrew N Sloss, Dominic Symes and Chris Wright, ARM system developers guide, Elsevier, 
	Morgan Kaufman publishers, 2008.
	2. Shibu K V, “Introduction to Embedded Systems”, Tata McGraw Hill Education, Private Limited, 2nd Edition.

## OOPS with python

### Experiment– 1 (Lists)
Develop a menu driven program to implement a queue using lists and functions. The operations would be: \
- Add an item to the queue (Enqueue) \
- Delete an item from queue (Dequeue) \
- Display the item at the front (QFront) \
- Display the item at the rear (QRear) \
- Display the queue

```py
"""
Develop a menu driven program to implement a queue using lists and functions. The
operations would be:
a) Add an item to the queue (Enqueue)
b) Delete an item from queue (Dequeue)
c) Display the item at the front (QFront)
d) Display the item at the rear (QRear)
e) Display the queue
"""

# global variable declarations
myQueue = []

# function declaration
def enqueue(myQueue, val):
  print("Value enqueued", val)
  myQueue.append(val)

def dequeue(myQueue):
  if len(myQueue) > 0:
    print("Value dequeued", myQueue.pop(0))
  else:
    print("Queue underflow")

def display(myQueue):
  if len(myQueue) > 0:
    print(myQueue)
  else:
    print("Empty queue")

def queueFront(myQueue):
  print(myQueue[0])
  
def queueRear(myQueue):
  print(myQueue[-1])
# ----------

def main():
  flag = True # exit control
  while flag:
    print("1. Enqueue\n2. Dequeue\n3. Display\n4. Queue front\n5. Queue rear\n6. Exit")
    choice = int(input("Enter your choice: "))
    # match (switch) - works only in python 3.10+
    match choice:
      case 1:
        val = int(input("Enter enqueue value: "))
        enqueue(myQueue, val)
      case 2:
        dequeue(myQueue)
      case 3:
        display(myQueue)
      case 4:
        queueFront(myQueue)
      case 5:
        queueRear(myQueue)
      case 6:
        flag = False
      case _:
        print("Invalid value")
        
if __name__ == main():
  main()
```

### Experiment– 2 (Dictionaries) \
Store the following information in a dictionary: \
Course Code: Course Name, Faculty, Number of registrations. \
Perform the following operations using functions: \
- Find Course Name that has highest number of registrations. \
- Given the Course Code, display the associated details. \
- Display details of all courses.

```py
'''
Store the following info in a dictionary 

course code: coursename, faculty, number of registrations

perform the following operations using function

a. display details of all courses
b. given the course code display all details
c. Fund coursename that has the highest registration
'''

def addCourse(myDict, courseCode, courseName, courseFaculty, courseReg):
    # finding duplicates
    tmp = myDict.get(courseCode)
    if tmp == None:
        myDict[courseCode] = (courseName, courseFaculty, courseReg)
        print(f"{courseCode} : ({courseName}, {courseFaculty}, {courseReg}) added sucessfully\n")
    else:
        print("Duplicates found, aborting\n")

def remCourse(myDict, courseCode):

    tmp = myDict.pop(courseCode)
    print(tmp, "removed from the dictionary\n")

def dispAll(myDict):
    print(myDict, '\n')

def dispDetails(myDict):
    for i in myDict:
        print(myDict[i])
    print('\n')

def maxPopular(myDict):
    popular = 0
    for i in myDict:
        if popular < myDict[i][2]:
            popular = myDict[i][2]
    print(f"Most popular couse is {i} with popularity {popular} \n")

def main():
    # creating an empty dictionary
    myDict = {}
    flag = True

    # menu
    while flag:
        print("1. Add items to dictionary\n2. Remove items from dictionary\n3. Display all")
        print("4. Display course code with details\n5. Find most popular course\n6. Exit")

        choice = int(input("Enter your choice: "))
        # switch statements
        match choice:
            case 1:
                courseCode = input("Enter a course code: ")
                courseName = input("Enter course name: ")
                courseFaculty = input("Enter faculty name: ")
                courseReg = int(input("Enter no of registrations: "))
                addCourse(myDict, courseCode, courseName, courseFaculty, courseReg)
            case 2:
                courseCode = input("Enter a course code: ")
                remCourse(myDict, courseCode)
            case 3:
                dispAll(myDict)
            case 4:
                dispDetails(myDict)
            case 5:
                maxPopular(myDict)
            case 6:
                flag = False
            case _:
                print("Invalid option selected\n")
        

if __name__ == "__main__":
    main()
```

###	Experiment– 3 (Files)
Write a Python program to read the book information from the user and store in a CSV file containing rows in the following format: bookNo, title, author, price. Develop a menu-driven program (with functions for each) with the following options: \
- Search Book by author \
- Search Books below specified price (Raise an exception if price entered is <= 0) \
- Search Books where title contains the specified word \
- Exit
```py
'''
Problem statement
Write a python program to read the books information from the user and store it in a CSV file containing 
rows in the following format: bookNo,title,author,price 
Develop a menu driven program with following options 
1. Search the book by author 
2. Search books below a specified price, raise an exception if the price entered is < 0
3. Search books where the title contain a certain word
4. Exit
'''

# importing required modules
import csv

# adding books in the records
def addBooks():
	key = True # loop variable
	rows = [[]] # csv writing matrix
	while key:
		bookNo = int(input("Enter book number: "))
		bookName = input("Enter book name: ") 
		bookAuth = input("Enter book author: ")
		bookPrice = int(input("Enter book price: "))
		bookQty = input("Enter book quantity: ")
		continueKey = input("Do you want to continue(y/n): ")
		print('')
		if continueKey.lower() == 'n': # exit control
			key = False
		rows.append([bookNo, bookName, bookAuth, bookPrice, bookQty])
	with open('books.csv', 'a', newline='') as bookFile:
		writeObj = csv.writer(bookFile)
		writeObj.writerows(rows) # writing into csv

# shows books from csv file
def showBooks():
	with open('books.csv', 'r') as bookFile:
		readObj = csv.reader(bookFile)
		for line in readObj:
			print(line) 

# initializes and clears book records
# runs everytime the program is started
def clearBooks():
	loopIndex = 0
	#initialising the fields
	fields = ["No", "Name", "Author", "Price", "Quantity"]
	with open('books.csv', 'w') as bookFile:
		csvwriter = csv.writer(bookFile)        
		csvwriter.writerow(fields)

# searches book via given author
def searchByAuth():
	keyAuthor = input("Enter author name: ")
	tmp = False # records found/not found
	with open('books.csv', 'r') as bookFile:
		readObj = csv.reader(bookFile)
		for records in readObj:
			# uses try/except to handle empty rows
			try:
				if records[2].lower() == keyAuthor.lower():
					tmp = True
					print(records)
			except IndexError:
				pass
	if tmp == False:
		print("Record not found")
	else:
		print("Records found")

# searches book via given title
def searchByTitle():
	keyTitle = input("Enter book title: ")
	tmp = False # records found/not found
	with open('books.csv', 'r') as bookFile:
		readObj = csv.reader(bookFile)
		for records in readObj:
			# uses try/except to handle empty rows
			try:
				if records[1].lower() == keyTitle.lower():
					tmp = True
					print(records)
			except IndexError:
				pass
	if tmp == False:
		print("Record not found")
	else:
		print("Records found")

# searches for book under the specified price
def showLowerPrice():
	maxPrice = int(input("Enter max price: "))
	if maxPrice < 0:
		# for value in -ve
		raise ValueError("Price must be a positive value.")

	tmp = False # records found/not found
	with open('books.csv', 'r') as bookFile:
		readObj = csv.reader(bookFile)
		for records in readObj:
			# uses try/except to handle empty rows
			try:
				if int(records[3]) <= int(maxPrice):
					tmp = True
					print(records)
			except:
				pass
	if tmp == False:
		print("Record not found")
	else:
		print("Records found")

def main():
	# initialising the file
	clearBooks()
	key = True
	while key:
		print("1. Add books\n2. Show books\n3. Clear books\n4. Search by author")
		print("5. Search by max price\n6. Search by title\n7. Exit")
		choice = int(input("Enter choice: "))
		# cli menu
		match choice:
			case 1:
				addBooks()
			case 2:
				showBooks()
			case 3:
				clearBooks()
			case 4:
				searchByAuth()
			case 5:
				showLowerPrice()
			case 6:
				searchByTitle()
			case 7:
				key = False
			case _:
				print("Invalid option selected")
		print("------------------------------")

if __name__ == "__main__":
	main()
```

### Experiment– 4 (Database) \
Write a Python program to perform the following: \
- Create a database named “products.db” \
- Create a table named “products” that has the following fields: \
prodID: int \
name: text \
quantity: int \
price: real \
- Insert n records into the table reading the values for each item from the user. \
- Display the recordset after fetching all the rows. \
- Delete a product whose product ID is entered by the user. \
- Increase the price of all products whose current price is less than Rs.50, by 10%. \
- Display all the products whose quantity is less than 40. \
```py
'''
Write a python program to perfoem the following 
 a) Create a database named products.sqlite 
 b) Create a table named products with following fields: 
     prodid:INT 
     name:Text 
     quantity:INT 
     price:Float 
 c) Insert n records into the table 
 d) Display the recordset after fetching all the rows 
 e) Delete the product whose product id is entered by user 
 f) Increase the price of all the products whose current price is less than 50 by 10% 
 g) Display all the products whose quantity is less than 40
'''

# note program developed and tested in ububtu wsl
import sqlite3

# Function to create the database and table
def create_database_and_table():
    connection = sqlite3.connect('products.sqlite')
    cursor = connection.cursor()

    cursor.execute('''CREATE TABLE IF NOT EXISTS products (
                      prodid INTEGER PRIMARY KEY,
                      name TEXT,
                      quantity INTEGER,
                      price REAL)''')

    connection.commit()
    connection.close()

# Function to insert n records into the table
def insert_records(n):
    connection = sqlite3.connect('products.sqlite')
    cursor = connection.cursor()

    for i in range(1, n+1):
        name = input(f"Enter name for product {i}: ")
        quantity = int(input(f"Enter quantity for product {i}: "))
        price = float(input(f"Enter price for product {i}: "))

        cursor.execute('''INSERT INTO products (name, quantity, price) 
                          VALUES (?, ?, ?)''', (name, quantity, price))

    connection.commit()
    connection.close()

# Function to fetch and display all rows
def display_records():
    connection = sqlite3.connect('products.sqlite')
    cursor = connection.cursor()

    cursor.execute("SELECT * FROM products")
    records = cursor.fetchall()

    print(records)
    if not records:
        print("No records found.")
    else:
        print("Product ID | Name | Quantity | Price")
        print("-" * 40)
        for record in records:
            print(f"{record[0]:^10} | {record[1]:^4} | {record[2]:^8} | {record[3]:^5}")

    connection.close()

# Function to delete a product by product ID
def delete_product_by_id(product_id):
    connection = sqlite3.connect('products.sqlite')
    cursor = connection.cursor()

    cursor.execute("DELETE FROM products WHERE prodid=?", (product_id,))
    connection.commit()

    if cursor.rowcount == 0:
        print(f"Product with ID {product_id} not found.")
    else:
        print(f"Product with ID {product_id} deleted successfully.")

    connection.close()

# Function to increase the price of products with current price < 50 by 10%
def increase_price():
    connection = sqlite3.connect('products.sqlite')
    cursor = connection.cursor()

    cursor.execute("UPDATE products SET price = price * 1.1 WHERE price < 50")
    connection.commit()

    print("Prices updated successfully.")

    connection.close()

# Function to display products with quantity < 40
def display_low_quantity_products():
    connection = sqlite3.connect('products.sqlite')
    cursor = connection.cursor()

    cursor.execute("SELECT * FROM products WHERE quantity < 40")
    records = cursor.fetchall()

    if not records:
        print("No products with quantity less than 40.")
    else:
        print("Product ID | Name | Quantity | Price")
        print("-" * 40)
        for record in records:
            print(f"{record[0]:^10} | {record[1]:^4} | {record[2]:^8} | {record[3]:^5}")

    connection.close()


def main():

    loopKey = True
    while loopKey:
        print('''1. Create database and table
              2. Insert records
              3. Display records
              4. Delete certain record
              5. Increase price
              6. Display low qty products
              7. Exit''')
        choice = int(input("Enter your choice: "))
        match choice:
            case 1:
                create_database_and_table()
            case 2:
                n = int(input("Enter the number of records to insert: "))
                insert_records(n)
            case 3:
                print("\n--- All Records ---")
                display_records()
            case 4:
                product_id_to_delete = int(input("\nEnter the product ID to delete: "))
                delete_product_by_id(product_id_to_delete)
            case 5:
                increase_price()
            case 6:
                print("\n--- Products with Quantity < 40 ---")
                display_low_quantity_products()
            case 7:
                loopKey = False
            case _:
                print("Invalid option selected")

if __name__ == "__main__":
    main()
```
### Experiment-5 (OOP – encapsulation and object composition) \
Create a system using Object Composition and Encapsulation concepts that allows customers to place orders for products.	The program consists of three classes: Customer, Order, and Product. The Customer class stores the customer's name, email and a list of their orders. It has methods to return name and email; place and return orders.	The Order class stores orderID and a list of products and has methods to return orderID and to	calculate total price for an order.	The product class stores the name and price of a product and has methods to return name and	price.
```py
# Expt 5 - Encapsulation and Object Composition

class Customer:
    def __init__(self, name, email):
        self.__name = name #Customer's name (private)
        self.__email = email #Customer's email (private)
        self.orders = [] #list to store customer's order
        
    def place_order(self, order):
        self.orders.append(order) #Add the given order to the list
    
    def get_orders(self):
        return self.orders #Return the list of customer's order
    
    def get_name(self):
        return self.__name #Getter method to access the private name
    
    def get_email(self):
        return self.__email #Getter method to access the private email
    
class Order:
    def __init__(self, order_id, products):
        self.__order_id = order_id 
        self.products = products 
        
    def get_order_id(self):
        return self.__order_id
    
    def get_total_price(self):
        total_price = 0
        for product in self.products:
            total_price += product.get_price()
        return total_price
    
class Product:
    def __init__(self, name, price):
        self.__name = name #Product name (private)
        self.__price = price #Product price (private)
        
    def get_name(self):
        return self.__name #Getter method to access the private name
    
    def get_price(self):
        return self.__price #Getter method to access the private price
    
#Creating objects
noOfCusts = int(input("Enter the number of Customers: "))
Custs=[]
for i in range(noOfCusts):
    name, email = input("Enter name and email for Customer" + str(i+1)+': ').split()
    customer = Customer(name, email)
    Custs.append(customer)
    
    noOfOrders = int(input("Enter number of orders for Customer " + name +": "))
    for j in range(noOfOrders):
        oid = int(input("Enter orderID for Customer "+name+": "))
        Prods = []
        noOfProds = int(input("Enter number of products for order "+str(oid)+" for Customer "+name+': '))
        for k in range(noOfProds):
            pName,price = input("Enter name and price of products: ").split()
            price = float(price)
            Prod=Product(pName,price)  #Product instantiation
            Prods.append(Prod)
        
        order = Order(oid,Prods)   #order instantiation
        customer.place_order(order)
        
print("\nDetails of Customer orders: ")
for cust in Custs:
    # Accessing customer information using the getter methods
    print("Customer Name:", cust.get_name())
    print("Customer Email:", cust.get_email())
    
    #Accessing order information
    orders = cust.get_orders()
    for order in orders:
        print("Order ID: ", order.get_order_id())
        print("Products:")
        for product in order.products:
            print(product.get_name(), "Rs" , product.get_price())
        print("Total price:",order.get_total_price())
        print()
```
### Experiment– 6 (OOP - Inheritance and polymorphism) \
Create an object-oriented program that allows you to enter data for customers and employees.Create a Person class that provides attributes for first name, last name, and emailaddress. This class should provide a property or method that returns the person’s fullname. Create a Customer class that inherits the Person class. This class should add anattribute for a customer number.	Create an Employee class that inherits the Person class. This class should add anattribute for a PAN number.	The program should create a Customer or Employee object from the data entered bythe user, and it should use this object to display the data to the user. To do that, theprogram can use the	isinstance() function to check whether an object is a Customer orEmployee object.
```py
'''
Create an oop that allows you to enters data for customer and employesss. 
create a person class with attributes first name, last name and email. This class should have a method  that return full name. 

Craete a employee class that inherits the person class , ad an attribute for customer no. 

Create a customer class which inherits a person class , add an attribute pan number. 

The program should create a Customer and Employee object from the data entered by the user and it should use this object to display the  
data to the user. to do that the program can use isinstance() function to check whether the object is a customer or employee
'''

# Define the base class 'Person'
class Person:
	def __init__(self, firstName, lastName, email):
		self.firstName = firstName
		self.lastName = lastName
		self.email = email

	def getName(self):
		return f"{self.firstName} {self.lastName}"

# Define the 'Employee' class which inherits from 'Person'
class Employee(Person):
	def __init__(self, firstName, lastName, email, empNo):
		super().__init__(firstName, lastName, email)
		self.empNo = empNo


# Define the 'Customer' class which inherits from 'Person'
class Customer(Person):
	def __init__(self, firstName, lastName, email, panNo):
		super().__init__(firstName, lastName, email)
		self.panNo = panNo

# Function to gather user input and display data
def main():
	# Ask the user for data type ('customer' or 'employee')
	data_type = input("Enter data type (customer/employee): ").lower()

	# Gather common data from the user
	firstName = input("Enter first name: ")
	lastName = input("Enter last name: ")
	email = input("Enter email: ")

	# Create a new object based on the data type entered by the user
	if data_type == "employee":
		# If 'employee', ask for the employee number and create an 'Employee' object
		empNo = input("Enter employee number: ")
		person_obj = Employee(firstName, lastName, email, empNo)
		# If 'customer', ask for the PAN number and create a 'Customer' object
	elif data_type == "customer":
		panNo = input("Enter PAN number: ")
		person_obj = Customer(firstName, lastName, email, panNo)
	else:
		# If an invalid data type is entered, display an error message and return
		print("Invalid data type. Please enter 'customer' or 'employee'.")
		return

	# Display the entered data
	print("Data entered:")
	print(f"Full Name: {person_obj.getName()}")
	print(f"Email: {person_obj.email}")

	# Use 'isinstance()' to check whether the object is an 'Employee' or 'Customer'
	if isinstance(person_obj, Employee):
		# If 'Employee', display the employee number
		print(f"Employee No: {person_obj.empNo}")
	elif isinstance(person_obj, Customer):
		# If 'Customer', display the PAN number
		print(f"PAN Number: {person_obj.panNo}")


if __name__ == "__main__":
	main()
```
### Experiment– 7 (GUI)
Develop the following GUI application. \
(Calculator app)
```py
# importing main module
from tkinter import *

# root functionalities
root = Tk()
root.title('Calculator')
root.geometry('640x360')

# will house the display
canvas1 = Canvas(root)
canvas1.pack()

# will house the buttons
canvas2 = Canvas(root)
canvas2.pack()

num1 = 0
num2 = 0
# ------------------------------

# functions
def fnInitialize():
	global num1, num2
	num1 = float(entryNum1.get())
	num2 = float(entryNum2.get())

def fnAddNum():
	fnInitialize()
	ans = num1 + num2
	labelAnsVal.config(text = f"Answer: {str(round(ans, 2))}")

def fnSubNum():
	fnInitialize()
	ans = num1 - num2
	labelAnsVal.config(text = f"Answer: {str(round(ans, 2))}")

def fnMulNum():
	fnInitialize()
	ans = num1 * num2
	labelAnsVal.config(text = f"Answer: {str(round(ans, 2))}")

def fnDivNum():
	fnInitialize()
	ans = num1 / num2
	labelAnsVal.config(text = f"Answer: {str(round(ans, 2))}")

# ------------------------------
# widgets

# first number prompt
lablelNum1 = Label(canvas1, text = "Enter num 1:")
lablelNum1.grid(row = 1, column = 1)

# first number will be here
entryNum1 = Entry(canvas1)
entryNum1.grid(row = 1, column = 2)

# second number prompt
lablelNum2 = Label(canvas1, text = "Enter num 2:")
lablelNum2.grid(row = 2, column = 1)

# second number will be here
entryNum2 = Entry(canvas1)
entryNum2.grid(row = 2, column = 2)

# answer prompt
lablelAns = Label(canvas1, text = "Answer")
lablelAns.grid(row = 3, column = 1)

# answer label
labelAnsVal = Label(canvas1)
labelAnsVal.grid(row = 3, column = 2)

# addition button
ButtonAdd = Button(canvas2, text = "Add", command = fnAddNum)
ButtonAdd.grid(row = 1, column = 1)

# subtraction button
ButtonSub = Button(canvas2, text = "Sub", command = fnSubNum)
ButtonSub.grid(row = 1, column = 2)

# multiplication button
ButtonMul = Button(canvas2, text = "Mul", command = fnMulNum)
ButtonMul.grid(row = 1, column = 3)

# division button
ButtonDiv = Button(canvas2, text = "Div", command = fnDivNum)
ButtonDiv.grid(row = 1, column = 4)

# looping trough the program
root.mainloop()
```
### Experiment– 8 (NumPy, Pandas, Matplotlib)
An exam has been conducted for a class of students. The exam data is stored in a CSV file, containing the student names and their scores. Develop a Python program to analyse the exam scores, calculate key statistics, and visualize the data to gain insights into the students' performance.
```py
# Importing required libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Step 2: Calculate key statistics using Numpy
def calculate_statistics(data):
    # Calculating average score
    average_score = np.mean(data['Score'])
    # Calculating maximum and minimum scores
    max_score = np.max(data['Score'])
    min_score = np.min(data['Score'])
    # Calculating number of students
    num_students = len(data)
    return average_score, max_score, min_score, num_students

# Step 3: Visualize the exam scores using matplotlib
def create_visualizations(data):
    # Histogram of exam scores
    plt.figure(figsize=(8, 6))
    plt.hist(data['Score'], bins=10, edgecolor='black')
    plt.xlabel('Score')
    plt.ylabel('Frequency')
    plt.title('Exam Score Distribution')
    plt.show()

    # Bar chart for top-performing students
    top_students = data[data['Score'] >= 90]
    plt.figure(figsize=(8, 6))
    plt.bar(top_students['Name'], top_students['Score'], color='green')
    plt.xlabel('Student Name')
    plt.ylabel('Score')
    plt.title('Top-performing Students')
    plt.xticks(rotation=45)
    plt.show()

# Main function to execute the program
def main():
    # Step 1: Load the exam data
    exam_data=pd.read_csv("Exam scores.csv")

    # Step 2: Calculate key statistics
    avg_score, max_score, min_score, num_students = calculate_statistics(exam_data)
    print("Average Score:", avg_score)
    print("Maximum Score:", max_score)
    print("Minimum Score:", min_score)
    print("Number of Students:", num_students)

    # Step 3: Create visualizations
    create_visualizations(exam_data)

if __name__ == "__main__":
    main()
```
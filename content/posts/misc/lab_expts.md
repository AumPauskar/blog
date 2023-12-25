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
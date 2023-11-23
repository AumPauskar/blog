+++
title = 'Computer network'
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

1. **Processing Delay (d_proc):** The time it takes for a router or switch to examine the incoming packet header and determine where to forward the packet.

2. **Queuing Delay (d_queue):** The time the packet spends waiting in a queue before it can be processed by the router or switch.

3. **Transmission Delay (d_trans):** The time it takes to push the bits of the packet onto the link. This is influenced by the link's bandwidth.

4. **Propagation Delay (d_prop):** The time it takes for a bit to travel from the source to the destination. This is determined by the distance between the nodes and the speed of the medium (e.g., speed of light in fiber).

The formula for nodal delay (D) can be expressed as the sum of these individual components:

\[ D = d_{\text{proc}} + d_{\text{queue}} + d_{\text{trans}} + d_{\text{prop}} \]

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
+++
title = 'Operating systems'
date = 2023-12-30T17:09:25+05:30
draft = false
tags = ["operating systems", "os", "linux", "unix"]
author = "Aum Pauskar"
+++

# Operating systems
## Bases of an operating system
- Execute user programs and make solving user problems easier
- Make the computer system convenient to use
- Use the computer hardware in an efficient manner

A computer system can be divided roughly into four components: the **hardware**, the **operating system**, the **application programs**, and the **users**.

### Use of an operating system
- The operating system is responsible for the following activities in connection with process management
	- Process creation and deletion
	- Process suspension and resumption
	- Provision of mechanisms for process synchronization
	- Provision of mechanisms for process communication
	- Provision of mechanisms for deadlock handling

Operating systems is a **resource allocator** and it is a **control program**.

### Kernel
The kernel is the one program running at all times on the computer. It is the core of the operating system. It performs the following functions:
- It is a program that remains in the memory at all times and is responsible for all the major activities of the operating system
- It is the first program to be loaded into the memory after the booting process is completed
- It is the last program to be removed from the memory when the computer is shut down
- Other programs are classified into two categories: **system programs** and **application programs**

### Dual mode operation of the operating system
In layman terms, the modern operating systems have two modes to run on, user mode and kernel mode. In general there are certain privalages being placed on certain programs that may only run in the kernel mode. Some computers even come with a VMM (virtual machine manager) for running guest opearting systems.

### Process management
- Process creation and deletion
- Process suspension and resumption
- Provision of mechanisms for process synchronization
- Provision of mechanisms for process communication
- Provision of mechanisms for deadlock handling

### Memory management
The job of a memory management software is to manage all process within a certain limitations of the memmory allowed by the computer's hardware specifications. The memory management software is responsible for the following:
- Keeping track of which parts of memory are currently being used and by whom
- Deciding which processes (or parts thereof) and data to move into and out of memory
- Allocating and deallocating memory space as needed
- (Optional) Swapping between the main memory and the secondary memory

### CPU scheduling
The job of a CPU scheduling software is to manage all process within a certain limitations of the CPU allowed by the computer's hardware specifications. The CPU scheduling software is responsible for the following:
- Deciding which process to run next
- Deciding when to allocate and deallocate CPU to a process
- Deciding when to suspend and resume a process
- Deciding which process to move into and out of memory
- Deciding which process to move into and out of the secondary memory

### Storage management
The job of a storage management software is to manage all process within a certain limitations of the storage allowed by the computer's hardware specifications. The storage management software is responsible for the following:
- A storage management system is responsible to keep track of the status of each storage unit, whether it is allocated or free
- Memory management is a part of storage management
- Modern operating systems use a file system to manage the secondary storage
- The file system might be FAT, NTFS, ext4, etc.
- In case of a file system, the computer has a table contatining the location of all the memory blocks that are free and the ones that are occupied
- The storage management system is also reponsible for running data across various data blocks in SSDs to increase hardware lifespan.
- Various storage devices
	- Ragisters
	- Cache
	- (DDR) RAM
	- SSD / HDD


### Protection
- The operating system must ensure that the access to the resources is controlled and to ensure the isolation of the various processes
- The operating system must also ensure that the computer is safe from any external attacks and viruses
- In operating systems like Linux, the user is given a unique user ID and a group ID to ensure the users are isolated.
- Some operations require special privileges and are only allowed to be executed by the root user this is called superuser mode and can be accessed by the `sudo` command.

### Distributed systems
Distributed systems refer to a group of computers working together as a unified computing resource. These systems often run on separate machines that are physically located in different locations, but they work together to perform tasks. They are designed to handle high levels of redundancy and replication to ensure data is always available, even in the event of a failure in part of the system. Distributed systems can be complex to manage due to issues like network latency, fault tolerance, and security concerns. However, they offer benefits in terms of scalability, performance, and reliability.

### Functions / interfaces of an operating system
- GUI
- CLI
- API
- Batch files

### System calls
System calls are the interface between the user-level applications and the kernel. They provide a way for programs to request services from the operating system such as file operations, process control, networking, device manipulation, and more. System calls allow user-level software to interact with hardware and system resources in a secure and controlled manner. They are crucial for the functioning of an operating system as they form the bridge between software and hardware.

- How are system calls used \
	System calls are used in a program when a process in user space requires resources or services from the kernel. This could be for operations such as creating processes, reading from or writing to files, communicating over network, accessing system clocks, etc.

	- The first input that the program will need is the names of the two files: the input file and the output file. These names can be specified in many ways, depending on the operating-system design.
	- One approach is for the program to ask the user for the names of the two files.
	- In an interactive system, this approach will require a sequence of system calls, first to write a prompting message on the screen and then to read from the keyboard the characters that define the two files.
	- On mouse-based and icon-based systems, a menu of file names is usually displayed in a window. The user can then use the mouse to select the source name, and a window can be opened for the destination name to be specified.



## Processes
When a linux operating system is run then many processes are created, these usually run at the user level rather running at the kernal level. \
Processes can be run via the `ps`
```bash
ps
```
Output
```
    PID TTY          TIME CMD
    372 pts/0    00:00:00 zsh
    470 pts/0    00:00:00 ps
```
An alternative to running the ps command is running the `top` or `htop` command. Htop is not natively installed in many systems and can be installed via `sudo apt install htop` in debian based systems.\
To see every process on the system 
```bash
ps -e
```


## Deadlocks
A deadlock is a situation in which two computer programs sharing the same resource are effectively preventing each other from accessing the resource, resulting in both programs ceasing to function. The earliest computer operating systems ran only one program at a time. All of the resources of the system were available to this one program. Later, operating systems ran multiple programs at once, interleaving them. Programs would often request resources in a specific order. If a program requested resource A and later requested resource B, another program would be able to run in between and use resource B, but not A, since it had not yet been released. If the first program then requested resource B, it would be locked out forever, since the other program had locked B and was waiting for A. This was the first and simplest sort of deadlock. Deadlocks can occur in operating systems, parallel computing, and distributed systems, as well as in everyday life.

## Safe state
In the context of operating systems, a safe state is a state where the system can allocate resources to each process in some order and avoid a deadlock. In other words, a system is in a safe state if there exists a sequence (called a safe sequence) in which each process can request and be allocated all its remaining required resources, execute to completion, release all its allocated resources, and still ensure that every other process can similarly complete. If no such sequence exists, the system is said to be in an unsafe state. It's important to note that being in an unsafe state does not imply that deadlock is inevitable, but it does mean that the risk of deadlock is present.


### Safe, unsafe, deadlock state

- resource allocation graph scheme

## Algorithms
### Banker's algorithm
Let n = number of processes, and m = number of resources types
- Available: Vecotor of length m. If available [j] = k, there are k instances of resource type Rj available.
- Max: n x m matrix. If Max [i,j] = k, then process Pi may request at most k instances of resource type Rj.
- Allocation: n x m matrix. If Allocation [i,j] = k then Pi is currently allocated k instances of Rj.
- Need: n x m matrix. If Need [i,j] = k, then Pi may need k more instances of Rj to complete its task.
- Need [i,j] = Max [i,j] - Allocation [i,j]

 ### Safety algorithm (banker's algorithm)
- Let work and finish be vectors of length m and n, respectively
	Initialize:
	Work = Available
	Finish [i] = false for i = 0, 1, ..., n-1
- Find an i such that both
	- Finish [i] = false
	- Need < Work
	If no such i exists, go to step 4
- Work = Wirj + Allocation
	Finish [i] = true
	go to step 2
- If finish [i] == true for all i, then the system is in a safe state


#### Example

1. Work = Available \
Work = 3 3 2 \
Finish [i] = false for i = 0, 1, 2, 3, 4

2. Finish [p0] = false \
Need [p0] <= Work \
7 4 3 <= 3 3 2 (false) \
Finish [p1] = false \
Need [p1] <= Work \
1 2 2 <= 3 3 2 (true) \
Work = Work + Allocation [p1]  \
	3 3 2 + 2 0 0 = 5 3 2 \
Work = 5 3 2	\
5 5 <p1>	\
**Finish [p1] = true** - 1	\
**Finish [p2] = false**	\
Need [p2] <= Work	\
6 0 0 <= 5 3 2 (true)	\
Finish [p3] = false	\
Need [p3] <= Work	\
0 1 1 <= 5 3 2 (true)	\
Work = Work + Allocation [p3] \
	5 3 2 + 2 1 1 = 7 4 3 \
**Finish [p3] = true** - 2 	\
5 5 <p1 p3>	\
Finish [p0] = false	\
need [p0] <= Work	\
4 3 1 <= 7 4 3 (true)	\
Work = Work + Allocation [p0]	\
	7 4 3 + 0 0 2 = 7 4 5	\
**Finish [p0] = true** - 3	\
5 5 <p1 p3 p0>	\
Finish [p2] = false	\
Need [p2] <= Work	\
7 4 3 < 7 4 5 (true)	\
Work = Work + Allocation [p2]	\
	7 4 5 + 0 1 0 = 7 5 5	\
**Finish [p2] = true** - 4	\
5 5 <p1 p3 p0 p2>	\
Finish [p4] = false	\
Need [p4] <= Work	\
6 0 0 <= 7 5 5 (true)	\
Work = Work + Allocation [p4]	\
	7 5 5 + 3 0 2 = 10 5 7	\
**Finish [p4] = true** - 5	\
5 5 <p1 p3 p0 p2 p4>

### Resource request algorithm (banker's algorithm)
Request = request vector for process Pi. If request [j] = k, then process Pi wants k instances of resource type Rj.
1. If request [i] <= Need [i], go to step 2. Otherwise, raise an error condition, since the process has exceeded its maximum claim.
2. If request [i] <= Available, go to step 3. Otherwise, Pi must wait, since the resources are not available.
3. Have the system pretend to have allocated the requested resources to process Pi by modifying the state as follows:
	Available = Available - request [i]
	Allocation [i] = Allocation [i] + request [i]
	Need [i] = Need [i] - request [i]

	- If safe -> the resources are allocated to Pi
	- If unsafe -> Pi must wait, and the old resource-allocation state is restored

### Example
Consider the following snapshot of a system:
| | Allocation | Need | Available |
| --- | --- | --- | --- |


- Answer the following questions using banker's algo
	- What is the content of the matrix Need? \
	Need = Max - Allocation

	| | A | B | C | D |
	| --- | --- | --- | --- | --- |
	| P0 | 0 | 0 | 0 | 0 |
	| P1 | 0 | 7 | 5 | 0 |
	| P2 | 1 | 0 | 0 | 2 |
	| P3 | 0 | 0 | 2 | 0 |
	| P4 | 0 | 6 | 4 | 6 |

	Work = 1 5 2 0 \
	Finish [i] = false
	Need [p0] <= Work \
	0 0 0 0 <= 1 5 2 0 (true) \
	Finish [p0] = true \
	5 5 <P0>
	Finish [p1] = false \
	Nedd [p1] <= Work \
	0 7 5 0 <= 1 5 3 2 (false) \
	Finish [p2] = false \
	1 0 0 2 <= 1 5 3 2 (true) \
	Work = Work + Allocation [p2] \
		1 5 2 0 + 1 0 0 2 = 2 5 2 2 \
	Finish [p2] = true \
	5 5 <P0 P2> \
	Finish [p3] = false \
	0 0 2 0 <= 2 5 2 2 (true) \
	Work = Work + Allocation [p3] \
		2 5 2 2 + 0 0 2 0 = 2 5 4 2 \
	Finish [p3] = true \
	5 5 <P0 P2 P3> \
	Finish [p4] = false \
	0 6 4 6 <= 2 5 4 2 (true) \
	Work = Work + Allocation [p4] \
		2 5 4 2 + 0 6 4 6 = 2 11 8 8 \
	Finish [p4] = true \
	5 5 <P0 P2 P3 P4> \
	Finish [p1] = false \
	0 7 5 0 <= 2 11 8 8 (true) \
	Work = Work + Allocation [p1] \
		2 11 8 8 + 0 7 5 0 = 2 18 13 8 \
	Finish [p1] = true \
	

	- Is the system in a safe state? If yes then give the safety sequence.
	- If a request from process P1 arrives for (0, 4, 2, 0), can the request be granted immediately?

### Producer consumer problem
- Producer process
	- Produces information
	- Puts information in buffer
- Consumer process
	- Consumes information
	- Takes information out of buffer
- Buffer
	- Shared data structure
	- Size of buffer is fixed
	- Producer must wait if buffer is full
	- Consumer must wait if buffer is empty

- Code for producer process
```c
while (true) {
	/* produce an item in next_produced */
	while (((in + 1) % BUFFER_SIZE) == out)
		/* do nothing */
	buffer [in] = next_produced;
	in = (in + 1) % BUFFER_SIZE;
}
```

- Race condition: A race condition in operating systems occurs when the behavior of a system or program depends on the relative timing or interleaving of multiple concurrent operations. It can lead to unpredictable and undesired outcomes, such as incorrect results, crashes, or deadlock. Race conditions typically arise when multiple threads or processes access shared resources or variables without proper synchronization mechanisms.

### Critical section problem
- Consider a system with n processes, each of which has a segment of code called a critical section, in which the process may be changing common variables, updating a table, writing a file, and so on.
- The important feature of the system is that, when one process is executing in its critical section, no other process is to be allowed to execute in its critical section.
- The critical-section problem is to design a protocol that the processes can use to cooperate. Each process must request permission to enter its critical section. The section of code implementing this request is the entry section. The critical section may be followed by an exit section. The remaining code is the remainder section.
- General structure of process P1
```c
do {
	/* entry section */
	/* critical section */
	/* exit section */
	/* remainder section */
} while (true);
```
- Solution to critical-section-problem
	- Mutual exclusion
		- If process Pi is executing in its critical section, then no other processes can be executing in their critical sections
	- Progress
		- If no process is executing in its critical section and there exist some processes that wish to enter their critical section, then the selection of the processes that will enter the critical section next cannot be postponed indefinitely
	- Bounded waiting
		- A bound must exist on the number of times that other processes are allowed to enter their critical sections after a process has made a request to enter its critical section and before that request is granted

## Memory
## Virual memory
### Copy on write
Copy-on-write (COW) is a resource-management technique used in computer programming to efficiently duplicate or copy modifiable resources, such as memory pages, storage sectors, files, and data structures. The main idea is to delay the actual copying of the data until it is actually needed, which can save time and memory.

Here's how it works:

1. **Sharing**: Multiple users or processes can initially share a single copy of the resource. This means they all have the same pointer to the same data in memory or storage.
2. **Copy on write**: If one user or process wants to modify the data, a copy is made **only for that user or process**. The original data is left unchanged for anyone else who is still sharing it.
3. **Private modifications**: The user or process with the copy can then modify the data in their private copy without affecting the original data or anyone else who is still using the shared copy.

There are several benefits to using copy-on-write:

* **Reduced memory usage**: By sharing a single copy of the data until it needs to be modified, COW can significantly reduce memory usage. This is especially beneficial for large data sets or when there are many users or processes sharing the same data.
* **Improved performance**: Copying data can be time-consuming. By delaying the copy until it is actually needed, COW can improve the performance of applications.
* **Simplified resource management**: COW can simplify the management of resources such as memory and storage. Instead of explicitly copying data when it is needed, COW allows the system to automatically handle the copying when a modification occurs.

Here are some real-world examples of how copy-on-write is used:

* **Operating systems**: Many operating systems use COW to implement the `fork` system call, which creates a new process that is a copy of an existing process. Instead of copying all of the memory used by the existing process, the new process initially shares the same memory pages. Only when the new process modifies a page is a copy made for that process.
* **File systems**: Some file systems use COW to create snapshots of files or directories. This allows users to see what the file system looked like at a previous point in time without actually copying any data.
* **Virtualization**: Virtualization software often uses COW to manage the memory used by virtual machines. This allows multiple virtual machines to share the same physical memory until they need to modify it.

### Page replacement
## Memory Pages and Page Replacement in Operating Systems

Imagine your computer's memory like a large desk, and the programs you run are like open textbooks and documents spread across it. Each textbook or document takes up a certain amount of space, just like programs use up memory. But the desk, like your computer's memory, is limited in size.

This is where **memory pages** come in. They act like dividers on your desk, splitting the available space into smaller, manageable chunks. Each program is then divided into its own pages, which can be loaded onto the desk (memory) as needed. This allows multiple programs to share the memory space efficiently, without everything having to be loaded at once.

However, there's a catch: the desk (memory) is often much smaller than all the textbooks and documents (programs) you might want to use at once. This is where **page replacement** comes into play. It's like reorganizing your desk – when you need a new document, you might put away an old one to make space.

Here's how page replacement works within an operating system:

1. **Programs are divided into pages**: Each program is broken down into fixed-size blocks called pages. These pages are like individual chapters in a book.
2. **Only some pages are loaded in memory**: Not all the pages of a program need to be in memory at the same time. The operating system keeps track of which pages are currently being used and loads them into available memory frames (think of these as sections of the desk).
3. **Page fault**: If a program tries to access a page that's not in memory, a **page fault** occurs. This is like realizing you need a specific chapter of a book that's not on your desk.
4. **Page replacement algorithm**: The operating system then uses a **page replacement algorithm** to decide which page in memory to evict (put away) to make room for the needed page. This is like choosing which document to temporarily remove from your desk.
5. **Swapping pages**: The evicted page is written to disk (like putting a document in a drawer) and the needed page is loaded into memory from disk (like taking a new document from your bag).

There are different page replacement algorithms, each with its own advantages and disadvantages. Some common ones include:

* **First-In-First-Out (FIFO)**: Evicts the page that has been in memory the longest, regardless of how recently it was used. (Think of taking out the first document you put on your desk.)\
	**Example**: `7, 0, 1, 2, 0, 3, 0, 4, 2, 3, 0, 3 ,2, 1, 2 ,0 ,1, 7, 0, 1`
	Consider the follwoing string and identify the page faults for three frames

| 7 | 0 | 1 | 2 | 0 | 3 | 0 | 4 | 2 | 3 | 0 | 3 | 2 | 1 | 2 | 0 | 1 | 7 | 0 | 1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 7 | 7 | 0 | 2 |

What do you mean by **belady's anomaly** and what does it indicate?\
A: Belady's anomaly occurs whan more frames are added in the memory pages the page faults will increase. It is an edge case scenario.


Here as you can see in this example of finding page faults 
* **Least Recently Used (LRU)**: Evicts the page that has been used the least recently. (Think of taking out the document you haven't touched in a while.)
* **Most Recently Used (MRU)/optimal algorithm**: Never evicts the page that was most recently used. (Think of always keeping the document you're currently using on your desk.)


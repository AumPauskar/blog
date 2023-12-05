+++
title = 'Big data and hadoop ecosystem'
date = 2023-12-05T12:17:46+05:30
draft = false
+++

# Big data

## Just data
- Structured data: data that has a defined length and format for each record. It's stored in a fixed format such as a relational database or spreadsheet. It's easy to search and analyze. It's used for transactional data.
- Unstructured data: data that has an unknown length and format. It's stored in a free format such as a text file. It's difficult to search and analyze. It's used for non-transactional data.
- Semi-structured data: data that has a defined length and format for each record but doesn't conform to the structure of a relational database. It's stored in a semi-structured format such as XML or JSON. It's easy to search and analyze. It's used for non-transactional data.
- Types of data analysis
	1. descriptive: what happened?
	2. diagnostic: why did it happen?
	3. predictive: what will happen?
	4. prescriptive: how can we make it happen?

## Data management software
### Hadoop
Hadoop is a framework for distributed storage and processing of large data sets using the MapReduce programming model. It consists of a distributed file system (HDFS) and a distributed processing framework (MapReduce). It's written in Java and is open source. It's designed to scale up from single servers to thousands of machines, each offering local computation and storage. Rather than rely on hardware to deliver high-availability, the library itself is designed to detect and handle failures at the application layer, so delivering a highly-available service on top of a cluster of computers, each of which may be prone to failures. Its use cases include data lake, data warehouse, data hub, data science, and data engineering. It's used by Facebook, Yahoo, LinkedIn, eBay, and Twitter. It's core components are HDFS, YARN, and MapReduce.

- Goals
	- High scalability and availability
	- Fault tolerance
	- Low cost
	- High throughput

- Disadvantages
	- It's not suitable for real-time processing of data
	- It's not suitable for processing small data sets
	- It's not suitable for processing unstructured data
	- It's not suitable for processing data that requires multiple iterations

- Distributed processing: processing of data sets across multiple computers in a cluster. It's used for parallel processing of large data sets. It's used for batch processing of data sets. It's used for processing of unstructured data sets. It's used for processing of data sets that require multiple iterations. It's used for processing of data sets that require real-time processing.

- Apache hardoop ecosystem
	- HDFS: distributed file system
	- YARN: resource management platform
	- MapReduce: distributed processing framework
	- Hive: data warehouse
	- Pig: data flow language
	- HBase: NoSQL database
	- ZooKeeper: distributed coordination service
	- Sqoop: data transfer tool
	- Flume: data collection tool
	- Oozie: workflow scheduler
	- Spark: distributed processing framework

#### HDFS
HDFS is a distributed file system that provides high-throughput access to application data. It's suitable for applications that have large data sets. It's designed to run on commodity hardware. It's highly fault-tolerant and is designed to be deployed on low-cost hardware. It provides high throughput access to application data and is suitable for applications that have large data sets. It relaxes a few POSIX requirements to enable streaming access to file system data. It's written in Java and is open source. It's used by Facebook, Yahoo, LinkedIn, eBay, and Twitter. It's core components are NameNode, DataNode, and Secondary NameNode. It's core components are NameNode, DataNode, and Secondary NameNode.

- Features of HDFS
	- High throughput
	- Fault tolerance
	- Horizontal scalability
	- High availability
	- Data locality
	- Data integrity
	- Data compression
	- Data access


#### HDFS namenode
- HDFS namenode: Namenode is a centerpiece of HDFS. It keeps the directory tree of all files in the file system, and tracks where across the cluster the file data is kept. It does not store the data of these files itself. The namenode is a single point of failure for the HDFS cluster.
- FSI: file system image. It's a file that contains the metadata of the HDFS. It's stored in the namenode.
- edit log: It's a file that contains the changes made to the FSI. It's stored in the namenode.

- Functions of the namenode
	- It manages the file system namespace.
	- It regulates client's access to files.
	- It executes file system operations such as renaming, closing, and opening files and directories.
	- It maps data blocks to data nodes.
	- It manages the replication of data blocks.
	- It executes periodic checkpoints of the file system metadata.

- Datanode: It's a slave node that stores the actual data in HDFS. It's responsible for serving read and write requests from the file system's clients. 

- Functions of datanode: 
	- It stores data in the local file system.
	- It sends heartbeats and block reports to the namenode.
	- It executes operations such as block creation, deletion, and replication as instructed by the namenode.
	- It serves read and write requests from the file system's clients.
	- It performs block creation, deletion, and replication upon instruction from the namenode.

- (File) Blocks: It's the smallest unit of data that can be stored or retrieved from a storage device. It's a sequence of bytes with a maximum size of 128 MB in hadoop2.x (64MB in 1.x). It's stored in the datanode.

- Advantages of blocks
	- It's easy to manage.
	- It's easy to replicate.
	- It's easy to distribute.
	- It's easy to process.

- Rack: It's a collection of 30 or 40 machines that are physically stored together. It's used to improve the network performance of the HDFS. It's used to improve the fault tolerance of the HDFS.

#### HDFS read write operations
- Read operation
	1. The client sends a read request to the namenode.
	2. The namenode sends the metadata of the file to the client.
	3. The client sends a read request to the datanode.
	4. The datanode sends the data block to the client.
	5. The client reads the data block.

- Write operation
	1. The client sends a write request to the namenode.
	2. The namenode sends the metadata of the file to the client.
	3. The client sends a write request to the datanode.
	4. The datanode sends an acknowledgement to the client.
	5. The client sends the data block to the datanode.
	6. The datanode sends an acknowledgement to the client.
	7. The client sends a write request to the namenode.
	8. The namenode sends an acknowledgement to the client.



#### HDFS CLI
It can be managed by a command line interface (CLI) or a web UI. The CLI is used for file operations, cluster maintenance, and data transfer. The web UI is used for monitoring and managing the cluster. It's core components are NameNode, DataNode, and Secondary NameNode.

Some of its basic commands are:
- `hadoop fs -ls /`: list the contents of the root directory
- `hadoop fs -ls /user`: list the contents of the user directory
- `hadoop fs -mkdir /user/hadoop`: create a directory named hadoop in the user directory
- `hadoop fs -put /home/hadoop/file.txt /user/hadoop`: copy the file.txt file from the local file system to the HDFS
- `hadoop fs -get /user/hadoop/file.txt /home/hadoop`: copy the file.txt file from the HDFS to the local file system
- `hadoop fs -cat /user/hadoop/file.txt`: display the contents of the file.txt file
- `hadoop fs -rm /user/hadoop/file.txt`: delete the file.txt file
- `hadoop fs -rm -r /user/hadoop`: delete the hadoop directory
- `hdfs fsck /`: check the HDFS for errors
- `hdfs dfs -ls /`: list the contents of the root directory
- `hdfs dfs -mkdir <dirname>`: create a directory
- `hdfs dfs -cat <filename>`: display the contents of a file
- `hdfs dfs -rm <filename>`: delete a file
- `hdfs dfs -rm -r <dirname>`: delete a directory
- `hdfs dfs -count <file/dir>`: count the number of directories, files, and bytes under the paths that match the specified file pattern
- `hdfs dfs -cp <source> <destination>`: copy files from the source to the destination
- `hdfs dfs -mv <source> <destination>`: move files from the source to the destination
- `hdfs dfs -get <source> <destination>`: copy files from the HDFS to the local file system
- `sbin/start-all.sh`: start all the hardoop daemons
- `sbin/stop-all.sh`: stop all the hardoop daemons
- `jps`: list the java processes running on the machine


### YARN
YARN stands for Yet Another Resource Negotiator. It's a resource management platform responsible for managing computing resources in clusters and using them for scheduling of users' applications. It's the architectural center of Hadoop that allows multiple data processing engines such as interactive SQL, real-time streaming, data science, and batch processing to handle data stored in a single platform, unlocking an entirely new approach to analytics. It's written in Java and is open source. It's used by Facebook, Yahoo, LinkedIn, eBay, and Twitter. It's core components are ResourceManager, NodeManager, and ApplicationMaster.

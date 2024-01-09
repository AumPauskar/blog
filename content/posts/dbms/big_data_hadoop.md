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

## NoSQL
NoSQL, which stands for "Not Only SQL", is a type of database that provides a mechanism for storage and retrieval of data that is modeled in means other than the tabular relations used in relational databases (RDBMS). 

NoSQL databases are designed to handle large volumes of data that don't fit well into tables, are distributed among many servers, or have a schema that changes rapidly. They are often used in big data and real-time web applications.

Here's how NoSQL differs from RDBMS:

1. **Schema**: NoSQL databases are typically schema-less, meaning they allow insertion of data without a predefined schema. This makes them more flexible than RDBMS, which require a predefined schema.
2. **Scalability**: NoSQL databases are designed to expand easily to handle large amounts of data and high user loads. This is in contrast to RDBMS, which are typically scaled by upgrading the hardware on a single server.
3. **Data Structure**: NoSQL databases can store data in a variety of ways, including key-value pairs, wide-column stores, graph databases, or document-oriented databases. RDBMS, on the other hand, store data in tables.
4. **Transactions**: RDBMS offer complex transactions with rollbacks, atomicity, consistency, isolation, and durability (ACID), while NoSQL databases sacrifice ACID compliance for performance and horizontal scalability.
5. **Consistency**: RDBMS ensure consistency across all nodes at any given time (strong consistency), while NoSQL databases typically ensure eventual consistency, where database changes are propagated to all nodes over time.
6. **Normalization**: RDBMS use normalization to reduce data redundancy. NoSQL databases, on the other hand, often use denormalization to improve performance.

Each type of database has its strengths and weaknesses, and the choice between using NoSQL or RDBMS will depend on the specific requirements of the project.

### SQL v NoSQL
| Feature | SQL (RDBMS) | NoSQL |
| --- | --- | --- |
| Schema | Predefined schema required | Typically schema-less |
| Scalability | Scaled by upgrading the hardware (vertical scaling) | Designed to expand easily across multiple servers (horizontal scaling) |
| Data Structure | Data stored in tables | Data can be stored in key-value pairs, wide-column stores, graph databases, or document-oriented databases |
| Transactions | Supports ACID transactions | Typically sacrifices ACID compliance for performance and scalability |
| Consistency | Strong consistency | Eventual consistency |
| Normalization | Uses normalization to reduce data redundancy | Often uses denormalization to improve performance |

### Advantages and Disadvantages of NoSQL Databases

| Feature | Advantages | Disadvantages |
|---|---|---|
| **Data Model Flexibility** | No predefined schema, can store diverse data types | Lack of schema can lead to data inconsistency and difficulty in querying |
| **Scalability** | Horizontally scalable by adding more nodes | Vertical scaling can be limited compared to relational databases |
| **Performance** | Often faster read and write speeds for specific operations | Complex queries can be slower than relational databases |
| **Availability** | High availability due to distributed nature | Data integrity can be compromised if not carefully managed |
| **Cost-Effectiveness** | Often cheaper than relational databases, especially for large datasets | Can be more expensive for complex workloads due to need for specialized skills |


**Additional points to consider:**

* NoSQL databases are a good choice for applications that require high scalability, performance, and flexibility.
* Relational databases are still the best choice for applications that require strong data consistency and complex queries.
* The choice between NoSQL and relational databases depends on the specific needs of the application.

### Types of NoSQL
NoSQL databases offer diverse data models, each excelling in specific scenarios. Here's a breakdown of the main types:

**1. Key-Value Stores:**

* **Structure:** Simple pairs of unique keys and associated values.
* **Use case:** Ideal for caching, session management, and storing simple configurations.
* **Examples:** Redis, Memcached, DynamoDB.

**Advantages:**

* **Fast access:** Direct retrieval by key minimizes search time.
* **Scalability:** Easily horizontally scalable by adding more nodes.
* **Simple:** Easy to understand and manage.

**Disadvantages:**

* **Limited querying:** Difficult to perform complex queries on multiple keys or values.
* **Data relationships:** Not suitable for storing complex relationships between data points.

**2. Document Stores:**

* **Structure:** Documents containing flexible data structures like JSON or XML.
* **Use case:** Perfect for storing semi-structured data like user profiles, articles, and product information.
* **Examples:** MongoDB, Couchbase, Cosmos DB.

**Advantages:**

* **Flexibility:** Store data in varying formats without schema restrictions.
* **Nested data:** Model complex relationships within documents.
* **Fast queries:** Efficient for querying documents based on specific fields.

**Disadvantages:**

* **Schema inconsistency:** Potential for data inconsistencies due to schema flexibility.
* **Joins:** Complex joins across documents can be less efficient than relational databases.

**3. Column-Oriented Databases:**

* **Structure:** Data organized by columns instead of rows, optimizing storage and queries.
* **Use case:** Excellent for time-series data, sensor readings, and analytics on large datasets.
* **Examples:** Cassandra, HBase, ScyllaDB.

**Advantages:**

* **Efficient queries:** Fast retrieval and aggregation of data based on specific columns.
* **Scalability:** Highly scalable for handling massive datasets.
* **Time-series data:** Optimized for storing and querying time-series data.

**Disadvantages:**

* **Complex joins:** Joining data across columns can be challenging.
* **Learning curve:** Requires understanding of data modeling for efficient usage.

**4. Graph Databases:**

* **Structure:** Represent data as nodes (entities) and edges (relationships) between them.
* **Use case:** Ideal for social networks, recommendation systems, and knowledge graphs.
* **Examples:** Neo4j, OrientDB, TigerGraph.

**Advantages:**

* **Natural representation:** Captures complex relationships between entities seamlessly.
* **Efficient navigation:** Fast traversal of paths and connections within the graph.
* **Insights discovery:** Uncovers hidden patterns and connections in data.

**Disadvantages:**

* **Limited querying:** Traditional SQL queries not directly applicable.
* **Data complexity:** Designing and maintaining large graphs can be challenging.

## Distributed models and sharding
Distributed models and sharding are techniques used to handle large amounts of data across multiple systems, often in the context of databases and machine learning. Here's a breakdown:

**Distributed Models:**

* **Concept:** Splitting a system or workload into smaller parts ("tasks") that are executed concurrently across multiple machines (nodes) in a network.
* **Benefits:**
    * **Scalability:** Handles massive datasets and computational demands by adding more nodes.
    * **Performance:** Parallelization accelerates tasks and improves response times.
    * **Availability:** Fault tolerance; system remains operational even if specific nodes fail.
* **Examples:**
    * Distributed databases (Cassandra, HBase)
    * MapReduce framework for parallel processing
    * Distributed machine learning models (Federated Learning)

**Sharding:**

* **Concept:** Horizontally partitioning a large dataset into smaller, independent subsets ("shards") stored on different nodes in a distributed system.
* **Benefits:**
    * **Scalability:** Increases storage capacity and read/write throughput by spreading data across nodes.
    * **Load balancing:** Distributes workload evenly across nodes, improving performance.
    * **Fault tolerance:** Data loss is limited to the affected shard if a node fails.
* **Examples:**
    * NoSQL databases with sharding capabilities (MongoDB, DynamoDB)
    * Web caching systems with sharded servers
    * Large content delivery networks (CDNs) with geographically distributed content shards

**Relationship:**

Sharding is a common implementation technique for distributed models, especially in database systems. It helps break down large datasets into manageable chunks, enabling efficient storage, retrieval, and manipulation across multiple nodes.

**Additional points:**

* Distributed models and sharding come with complexity in managing data consistency, routing queries, and handling node failures.
* The choice of model and sharding strategy depends on factors like data size, access patterns, and desired performance and availability.

### Replication
In distributed models, replication refers to the **creation and maintenance of multiple copies of the same data or model across different nodes within the system**. This technique offers several key advantages:

**1. Increased Availability:**

* Having multiple copies ensures that the system remains operational even if some nodes fail. Users can still access data or model predictions from healthy replicas.

**2. Improved Performance:**

* By spreading data and model computations across multiple nodes, latency is reduced for user requests. Accessing local replicas can be faster than reaching a central server.

**3. Enhanced Scalability:**

* Adding more nodes allows for replication across additional machines, effectively increasing the capacity of the system to handle larger datasets and workloads.

**4. Fault Tolerance:**

* Data or model corruption on one node is isolated, as other replicas remain intact. This allows for easier recovery and minimizes data loss.

**Types of Replication in Distributed Models:**

* **Full Replication:** All nodes hold an identical copy of the data or model. This guarantees high availability but requires substantial storage and network bandwidth.
* **Partial Replication:** Only a subset of data or model components are replicated across specific nodes. This offers a balance between availability, performance, and resource usage.
* **Dynamic Replication:** Replication is adjusted based on load, resource availability, and data access patterns. This can optimize performance and cost-effectiveness.

**Challenges of Replication:**

* **Maintaining Consistency:** Ensuring all replicas remain consistent after updates requires efficient synchronization mechanisms. Delays or inconsistencies can affect data integrity and model accuracy.
* **Overhead:** Replication incurs additional storage and network resource consumption, increasing system complexity and potentially impacting performance.
* **Complexity of Management:** Choosing the right replication strategy and managing diverse replicas requires careful planning and expertise.

## The CAP Theorem Explained: Consistency, Availability, and Partition Tolerance

The CAP theorem, also known as Brewer's theorem, is a fundamental principle in distributed systems architecture. It states that in the presence of network partitions (communication breaks between nodes), a distributed system can only guarantee two out of the following three properties:

**1. Consistency:** Every read operation receives the most recent write or an error. This ensures that all nodes in the system have the same up-to-date view of the data.

**2. Availability:** Every request receives a response, even if it's not necessarily the most recent data. This means the system remains operational and accessible even during network failures.

**3. Partition Tolerance:** The system continues to operate despite an arbitrary number of messages being dropped or delayed by the network between nodes. This ensures resilience and fault tolerance in the face of network disruptions.

Essentially, the CAP theorem imposes a trade-off: you can't have all three properties simultaneously. Depending on your application's specific needs, you need to prioritize two of them.

Here's a breakdown of the trade-offs involved:

**CAP Trade-offs:**

* **CA (Consistent and Available):** This is impossible in a partitioned network. If you always want to provide up-to-date data (consistency), there might be situations where a node can't access other nodes due to a partition, making it unavailable.
* **AP (Available and Partition-tolerant):** This is achieved by prioritizing availability over consistency. Even if some nodes are down, users can still read and write data, but the retrieved data might not be the most recent version. This approach is often used in NoSQL databases like Cassandra and Couchbase.
* **CP (Consistent and Partition-tolerant):** This is possible but comes at the cost of availability. When a partition occurs, the system might block further reads or writes until the network heals, ensuring data consistency across all nodes but sacrificing immediate availability. This approach is often used in relational databases and ACID transactions.

### ACID
**ACID properties in transactions:**

- **Atomicity:** Either the entire transaction succeeds or fails as a whole unit. There are no partial executions. 
- **Consistency:** The transaction brings the database from one valid state to another valid state according to the pre-defined rules.
- **Isolation:** Concurrent transactions do not interfere with each other, and each sees a consistent view of the database.
- **Durability:** Once committed, changes made by a successful transaction are permanent and survive even system failures.

## Mapreduce
The need for MapReduce arose from the challenges of processing **massive datasets** that wouldn't fit on a single machine and couldn't be handled efficiently by conventional sequential processing. Here's a breakdown of the reasons why MapReduce became necessary:

**Challenges of Big Data Processing:**

* **Scalability:** Traditional serial processing struggles to handle the massive volumes of data generated nowadays, leading to slow processing times and bottlenecks.
* **Fault Tolerance:** Single server failures can halt data processing completely, requiring robust systems to handle disruptions.
* **Cost-Effectiveness:** Scaling up computational power by adding more expensive hardware isn't always feasible or cost-efficient.

**MapReduce to the Rescue:**

MapReduce addresses these challenges by providing a **framework for parallel processing of large datasets across distributed cluster systems**. It works by dividing the data into smaller chunks and processing them simultaneously on multiple nodes in the cluster. This approach offers several advantages:

**Benefits of MapReduce:**

* **Parallelism:** By splitting the data and processing it concurrently on multiple nodes, MapReduce significantly increases processing speed.
* **Scalability:** The framework can easily scale to handle larger datasets by adding more nodes to the cluster.
* **Fault Tolerance:** If a node fails, its tasks can be reassigned to other nodes, ensuring continued processing without significant data loss.
* **Cost-Effectiveness:** Utilizing commodity hardware instead of expensive high-performance machines makes MapReduce cost-efficient for handling big data.

**How MapReduce Works:**

1. **Map Phase:** The input data is divided into smaller chunks and processed by **mapper functions** running on each node. These functions typically transform the data into key-value pairs.
2. **Shuffle Phase:** The key-value pairs are shuffled and sorted based on their keys across the cluster. This ensures that all values associated with a specific key are grouped together on the same node.
3. **Reduce Phase:** **Reducer functions** process the grouped key-value pairs on each node, performing aggregations, calculations, or any other desired operations on the values.
4. **Output:** The final results of the Reduce phase are written to a distributed file system.

### Working of mapreduce
 **Here's a comprehensive explanation of MapReduce, its stages, and communication with HDFS, incorporating visual aids:**

**MapReduce Overview:**

- Framework for parallel processing of large datasets across distributed systems.
- Designed to handle massive data volumes that traditional systems cannot process efficiently.
- Divides data into smaller chunks, processes them concurrently on multiple nodes, and then aggregates results.
- Offers scalability, fault tolerance, and cost-effectiveness.

**MapReduce Stages:**

**1. Map Phase:**

- **Breaks down input data into smaller chunks.**
- **Distributes chunks to mapper functions running on different nodes.**
- **Mappers process each chunk, transforming data into key-value pairs.**
- **Outputs intermediate key-value pairs.**

[Image of MapReduce Map Phase]

**2. Shuffle Phase:**

- **Collects intermediate key-value pairs from all mappers.**
- **Sorts and groups pairs by key, ensuring values with the same key are sent to the same reducer.**
- **Shuffles and distributes grouped pairs to reducers.**

[Image of MapReduce Shuffle Phase]

**3. Reduce Phase:**

- **Reducers receive grouped key-value pairs.**
- **Process each group, performing aggregations, calculations, or other operations on the values.**
- **Generate final results, typically as key-value pairs or summary data.**
- **Writes final output to HDFS.**

[Image of MapReduce Reduce Phase]

**Communication with HDFS:**

- **Input Data:** Stored in HDFS, accessed by mappers directly.
- **Intermediate Data:** Written to local disks during Map phase, then transferred to reducers during Shuffle phase.
- **Output Data:** Written back to HDFS by reducers, stored for further analysis or downstream tasks.

[Image of MapReduce Interaction with HDFS]

**Key Points:**

- MapReduce is a powerful framework for handling big data.
- It excels in parallel processing, scalability, and fault tolerance.
- HDFS provides robust storage for massive datasets.
- Understanding MapReduce stages and HDFS interaction is crucial for effective big data processing.

## YARN
## What is YARN?

**Yet Another Resource Negotiator (YARN)** is a core component of the Apache Hadoop ecosystem responsible for resource management and job scheduling in big data processing frameworks. It acts as the **traffic controller** for Hadoop, overseeing the allocation of resources like CPU, memory, and storage across the cluster and coordinating the execution of various applications.



**In simpler terms, imagine YARN as the conductor of a Hadoop orchestra. While Hadoop provides the instruments (MapReduce, Spark, etc.), YARN assigns musicians (tasks) to sections (nodes), ensures everyone has the necessary resources (memory, CPU), and coordinates their performance (job execution) to produce a harmonious result (data processing).**

## What is the Use of YARN?

YARN offers several key benefits over the earlier resource management system in Hadoop (JobTracker):

**1. Increased Flexibility:** YARN supports running various big data processing frameworks like MapReduce, Spark, Apache Flink, and more simultaneously on the same Hadoop cluster. This allows you to choose the right tool for each specific task without restricting yourself to just MapReduce.



**2. Efficient Resource Management:** YARN dynamically allocates resources based on application needs, optimizing resource utilization and preventing bottlenecks. This reduces idle time and improves overall cluster performance.

**3. Improved Scalability:** YARN can easily scale horizontally by adding more nodes to the cluster, allowing you to handle ever-larger datasets and more complex workloads.

**4. Fault Tolerance:** YARN implements a distributed architecture, where applications are managed by independent components. If a node fails, YARN can reschedule tasks on other healthy nodes, ensuring job completion even with individual failures.

## How does YARN tie in with the Apache ecosystem?

YARN plays a crucial role in the Apache ecosystem by serving as the central platform for:

**1. Resource Management:** It offers a unified resource management system for diverse big data processing frameworks within the Hadoop ecosystem.

**2. Job Scheduling:** YARN coordinates the execution of various applications across the cluster, ensuring efficient scheduling and preventing conflicts.

**3. Data Sharing:** YARN facilitates seamless data sharing between different applications running on the cluster, enabling collaborative data analysis and processing.

**4. Scalability and Flexibility:** YARN's architecture allows for scalable and flexible big data processing, adapting to the ever-evolving needs of data analytics and computing.

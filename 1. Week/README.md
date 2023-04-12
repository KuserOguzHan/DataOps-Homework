This section is aimed to learn Hadoop Systems. Although utilization of the Hadoop System decreases every year, we should learn as it is a pioneer in cloud architecture services.

In addition, Hadoop still is used many sectors.

### 1. What is Hadoop?

Hadoop is a popular, open-source Apache project developed with the JAVA programming language using the MapReduce programming model. 
The purpose of this software is to enable secure and scalable computing by being responsible for load balancing, data distribution, and processing.


### 2. What is HDFS (Hadoop Distributed File System)?
HDFS, one of the basic building blocks of Hadoop, is a distributed file system.
- Master or Name Node; Where the information of the data is located. How many copies of each data are there, and on which worker-data node it is located?
- Worker or Data Node; Where the data is kept.
- Edge Node; The first place where the customer communicates to receive or send information.
- Journal Node; If the master-name node fails, a new master-name node is created by Zookeeper. 

### 3. What is MapReduce?
MapReduce is a system that allows very large data to be easily analyzed on a distributed architecture.

### 4. YARN (Yet Another Resource Negotiator)
YARN makes it easy to monitor scheduled tasks, general management and monitoring cluster nodes and other resources.

### 5. What is HIVE?
Hive is a SQL-like query tool for querying data stored on HDFS.
Metastore: Metastore is the central repository of Apache Hive metadata. It stores metadata for Hive tables (their schemas and locations, etc.) and partitions in a relational database. It provides client access to this information using the metastore API.

### 6. What are Partitions?
Partitioning is an important factor for performance. Basically, we store table data by partitioning the data according to a specific column value, which we call the partition key. When scanning petabyte-sized data, the process will take considerably longer than the data size, as the entire table will be scanned (full scan) while filtering in our queries. For this reason, when we want to filter the data by determining the correct partition key, we will only access the relevant data. This significantly increases our reading performance. There are two types of partitioning in Hive: Static and Dynamic. Let's look at them now.

- Static Partitioning; With static partitioning, we load partitions manually. For this, we need to know which data should be added to which partition. Let's explain this with an example.

- Dynamic Partitioning; As you can understand dynamic partitioning, automatically performs the partition process according to the incoming data, so you do not need manual intervention.


### 7. What are Buckets?
Bucket is another way of partitioning data like partitioning. But why should we use bucketing when we have partitioning?
We have already explained that when you partition, you actually create a directory and the related files are collected under these directories. In bucketing, similar data is physically written in the same place, which will make it much easier to retrieve the relevant data during a search.
Partitioning only gains efficiency if the data is evenly distributed, whereas in the real world we know that this data will not be evenly distributed. This is a loss of efficiency. For this reason, a solution such as bucketing was needed when there was partitioning.

### 8- What is Sqoop?
Apache Sqoop is a java-based tool that enables the transfer of large data between relational databases and hadoop. This transfer can be done in both directions. It can read the data from the relational database (oracle, mysql, sqlserver ...) and transfer it to the hadoop distributed file system (HDFS, Hive, Hbase ...) as well as read it from the hadoop environment and write it to the relational database.




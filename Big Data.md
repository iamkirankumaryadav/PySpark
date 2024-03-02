### **What is Big Data?**

Big data refers to gigantic collections of information that are too massive and complex for regular software to handle. 

This data comes from everywhere:
* **What you do online:** Websites you visit, things you buy, videos you watch.
* **Sensors:**  Traffic cameras, weather stations, machines in factories.
* **Social Media:** Posts, likes, and shares.
* **Businesses:** Sales records, customer information 

### **Why is big data important?**

Inside those giant warehouses of data are hidden patterns and connections. 

Big data tools are like powerful searchlights:
* **Companies:** Understand customers better, predict trends, make smarter decisions.
* **Scientists:** Discover new medical treatments, track climate patterns.
* **Cities:** Improve traffic flow, optimize energy use, make life better for people.

### **Hadoop:**

* **The storage room:**  Hadoop is a framework that stores and manages massive amounts of data across multiple computers in a distributed way.
* It's like having a network of warehouses to hold all those information boxes.
* Hadoop is a way to distribute very large data sets across multiple machines. It uses the Hadoop Distributed File System (HDFS)
* HDFS allows a user to work with large datasets, it also duplicates blocks of data for fault tolerance.

### **MapReduce:**

* **The sorting process:**  MapReduce is a programming model within the Hadoop framework.
* It takes a big job, breaks it down into smaller, more manageable tasks (like sorting through individual boxes), and distributes those tasks across the network of computers.
* Once individual tasks are complete, MapReduce gathers the results and presents the final output.
* MapReduce is a way of splitting a computation task to a distributed data sets.
* MapReduce consist of Job Tracker (Master Node) and multiple Task Trackers (Worker Nodes)
* The Job Tracker sends code to run on the Task Trackers, the Task Trackers allocate CPU and memory for the tasks and monitor the tasks on the worker nodes.

### **Spark:**

* **The advanced search tool:**  Spark is another framework that sits on top of Hadoop, but it offers a faster and more flexible way to handle and process big data.
* It can process data in **memory** (like having readily accessible information on a desk) instead of just relying on hard drives (like the warehouse shelves).
* This makes Spark ideal for real-time processing and iterative tasks where you need to keep going back and analyzing the data multiple times.
* Spark is a flexible alternative to **MapReduce**, Spark can used data stored in a variety of formats (Cassandra DB, AWS S3, HDFS, etc)

### Why Spark is better than MapReduce?

- MapReduce required files to be stored only in HDFS, Spark can use data stored at various source.
- Spark can perform operations 100x faster than MapReduce.
- MapReduce writes most data to disk (Hard Drive) after each map and reduce operation, Spark keeps most of the data in memory (RAM) after each transformation.
- Spark can spill over to disk (Hard Drive) if the memory (RAM) is filled.
- At the core of Spark is the idea of Resilient Distributed Dataset (RDD)

### **Resilient Distributed Dataset (RDD)**
- Distributed Collection of Data
- Fault tolerant
- Parallel operation - Partitioning
- Ability to use many data sources
- Master Node assign Tasks to the Worker Nodes
- Worker Nodes returns results
- RDDs are immutable 

Here's a table summarizing the key differences:

| Feature                 | Hadoop                | MapReduce         | Spark               |
|:---|:---|:---|:---|
| **Purpose**               | Data storage and management | Data processing model | Data processing framework |
| **Processing speed**    | Slower (disk-based)  | Slower (disk-based) | Faster (memory-based) |
| **Processing type**     | Batch processing      | Batch processing  | Batch & real-time processing |
| **Ease of use**          | More complex        | Complex             | More user-friendly |
| **Security**             | More secure          | More secure          | Less secure (developing) |

Choosing between them depends on your specific needs. If you need to store and manage massive datasets, **Hadoop** is a good foundation. If you need to process large datasets in batches, **MapReduce** might suffice. But if you need faster processing, real-time analysis, or want to explore data iteratively, **Spark** is often the preferred choice.

### **Local System:**

* **A single computer:** A local system is a complete computing environment running on a single machine. It has its own processor, memory, storage, and operating system. Think of it like a single, self-contained workstation.
* **Pros:**
    * **Simple:** Easy to set up and manage.
    * **Fast:** Communication and data access happen within the same machine, leading to faster performance.
    * **Cost-effective:** Requires only one machine for operation.
* **Cons:**
    * **Limited resources:** Processing power, memory, and storage are limited to the capabilities of the single machine.
    * **Scalability:** Difficult to scale up by adding more resources when needed.
    * **Single point of failure:** If the machine fails, the entire system becomes unavailable.

### **Distributed System:**

* **A network of computers working together:** A distributed system consists of multiple computers connected to a network and working together as a single unit. Each computer has its own resources and contributes to the overall functionality of the system. Imagine a team of specialists collaborating on a large project, each contributing their expertise.
* **Pros:**
    * **Scalability:** Resources can be easily added or removed by adding or removing machines, allowing the system to grow as needed.
    * **Reliability:** If one machine fails, the remaining machines can continue to operate, providing redundancy and fault tolerance.
    * **Parallel processing:** Tasks can be divided and processed simultaneously across multiple machines, potentially improving performance and handling larger workloads.
* **Cons:**
    * **Complexity:** Setting up and managing distributed systems can be more complex than local systems.
    * **Communication overhead:** Data and information need to be transferred across the network, which can introduce additional overhead and impact performance compared to local access.
    * **Potential for single points of failure:** Depending on the architecture, certain components within the system could still be single points of failure.

**Choosing between local and distributed systems depends on your specific needs:**

* **Use local systems:** When you have a simple task with limited data and resources, and high performance is crucial.
* **Use distributed systems:** When you need to handle large amounts of data, require scalability, and can tolerate some additional complexity for increased reliability and potential performance gains through parallel processing.

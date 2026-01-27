# Grep on Hadoop using Cloudera

## Project Overview
<p align="justify">
This project focuses on designing and implementing a Grep application using Hadoop MapReduce to perform efficient keyword or pattern-based searching on large-scale text data stored in the Hadoop Distributed File System (HDFS). Instead of processing files on a single machine, the application takes advantage of Hadoop’s distributed architecture to handle large datasets by splitting the input data across multiple nodes and processing it in parallel.
</p>

<p align="justify">
The application is developed entirely in Java and executed on Apache Hadoop running inside the Cloudera QuickStart Virtual Machine, which provides a pre-configured environment for learning and experimenting with Hadoop ecosystem components. By using MapReduce, the project demonstrates how data-intensive text processing tasks can be broken down into smaller units of work, processed simultaneously, and then combined to produce the final result.
</p>

<p align="justify">
Functionally, this project replicates the behavior of the traditional Linux grep command, but in a scalable and distributed manner. While the standard grep utility works well for small files on a local system, this Hadoop-based implementation is suitable for searching keywords or patterns within very large text files, such as logs or documents, stored in HDFS. Overall, the project highlights the power of distributed computing and serves as a practical introduction to Hadoop MapReduce programming, HDFS operations, and large-scale text analysis.
</p>

**Sample Input File Name:** `constitution.txt`

---

## Technology Stack
- **Apache Hadoop**
  - HDFS
  - MapReduce
- **Java**
- **Cloudera QuickStart VM**
- **Eclipse IDE**
- **WinSCP**

---

## Prerequisites

### Java
- JDK 7 or above installed
- `JAVA_HOME` configured properly

### Hadoop (Cloudera QuickStart)
- Cloudera QuickStart VM installed and running
- Hadoop services up and running inside the VM

### Eclipse
- Eclipse IDE for Java Developers
- Used for writing, compiling, and exporting the MapReduce project as a JAR

### WinSCP
- Used to transfer files between the local system and Cloudera VM

---

## Establishing Connection Between Local Host and Cloudera using WinSCP

**Connection Details:**
- **Hostname:** `localhost`
- **Protocol:** SFTP
- **Port:** `22`
- **Username:** `cloudera`
- **Password:** `cloudera`

### Steps to Connect WinSCP to Cloudera VM
1. Open **WinSCP**
2. Select **SFTP** as the protocol
3. Enter the hostname, port, username, and password
4. Click **Login**
5. Once connected, access the Cloudera home directory

**Purpose:**
- Transfer **JAR files** from local system to Cloudera VM
- Download **output files** from Cloudera to local system

---

## Project Structure

 Reducer file 
   └──  part-r-00000 
 Sample 
   └──  constitution.txt 
 grep 
   ├──  bin 
   │   └──  grep
   ├──  src 
   │   └── grep 
   └──  Grep.java 
 jar file 
   └──  grep.jar 
   
README.md 



---

## Java Program Explanation

### Mapper (Grep Logic)
- Reads each line from the input file
- Checks whether the line contains the specified keyword/pattern
- Emits the matched line with a count of `1`

**Input:**  
`<LongWritable, Text>`

**Output:**  
`<Text, IntWritable>`

---

### Reducer
- Aggregates the counts of matched lines
- Outputs the final matched lines and their occurrences

---

### Driver Class
- Configures the MapReduce job
- Sets:
  - Mapper class
  - Reducer class
  - Input and output paths
- Submits the job to Hadoop for execution

---

## Steps to Execute the Project on Cloudera

### 1. Creating Java Project in Eclipse
- Open Eclipse
- Create a new **Java Project**
- Add package and Java classes (Mapper, Reducer, Driver)

### 2. Adding External Hadoop JARs
- Right-click project → **Build Path**
- Add required Hadoop JARs from Cloudera installation

### 3. Exporting the Project as a JAR
- Right-click project → **Export**
- Select **Runnable JAR**
- Export as `GrepHadoop.jar`

### 4. Uploading Sample File to HDFS

`<hadoop fs -mkdir -p /user/cloudera/input/>
<hadoop fs -put constitution.txt /user/cloudera/input/>`

**Running Grep MapReduce Job**
`<hadoop jar GrepHadoop.jar com.hadoop.grep.GrepDriver \>
</user/cloudera/input/constitunial /user/cloudera/output>`


### Output Directory Creation

- Hadoop automatically creates the output directory

- Ensure the directory does not already exist

###  Output File

`<part-r-00000>`

- Reading Output
`<Using hadoop fs -cat>`
`<hadoop fs -cat /user/cloudera/output/part-r-00000>`

- Transferring Output from Cloudera to Local System
- Using `<hadoop fs -get>`
`<hadoop fs -get /home/cloudera/output/part-r-00000 /home/cloudera/>`

### Using WinSCP

- Navigate to the output file location in Cloudera

- Download `<part-r-00000>` to the local machine

### HDFS Commands Used
`<hadoop fs -ls>`<br>
`<hadoop fs -mkdir>`<br>
`<hadoop fs -put>`<br>
`<hadoop fs -cat>`<br>
`<hadoop fs -get>`<br>
`<hadoop fs -rm -r>`<br>

---
### Conclusion

This project successfully demonstrates how to implement a **Grep program using Hadoop MapReduce**. By running the application on **Cloudera QuickStart VM**, it showcases the power of distributed processing for text searching tasks. The project also provides hands-on experience with **HDFS commands**, **MapReduce programming**, and **file transfer using WinSCP**.

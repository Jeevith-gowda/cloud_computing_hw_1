# Hadoop MapReduce WordCount Project

## 📌 Project Overview
This project demonstrates the **Hadoop MapReduce WordCount** program.  
The purpose is to read an input text file, process it using a Mapper and Reducer, and produce the frequency of each word as output.  
This assignment also teaches how to set up a Hadoop environment using **Docker**, build a Java project with **Maven**, and interact with **HDFS**.

---

## ⚙️ Approach and Implementation

### Mapper Logic
The Mapper reads each line of the input file, splits it into words, and emits each word as a key with a value of `1`.  
Words with fewer than 3 characters are ignored.  

**Example:**
Input: "hello world"
Mapper Output: (hello, 1), (world, 1)

### Reducer Logic
The Reducer sums all the values for the same word key to compute the total count.  

**Example:**
Input: (hello, [1, 1])
Reducer Output: (hello, 2)


---

## 🚀 Execution Steps

### Build the Project
```bash
cd "C:\Users\jeevi\L5 hands on\H3_itcs6190_Hadoop_MapReduce_Wordcount"
mvn clean package
```

### Start Hadoop Cluster with Docker
```bash
docker compose up -d
```

### Copy Files to Docker Container
```bash
docker cp target/WordCountUsingHadoop-0.0.1-SNAPSHOT.jar resourcemanager:/opt/hadoop-3.2.1/share/hadoop/mapreduce/
docker cp shared-folder/input/data/input.txt resourcemanager:/opt/hadoop-3.2.1/share/hadoop/mapreduce/

```

### Connect to Hadoop Container
```bash
docker exec -it resourcemanager /bin/bash
cd /opt/hadoop-3.2.1/share/hadoop/mapreduce/

```

### Set Up HDFS and Upload Dataset
```bash
hadoop fs -mkdir -p /input/data
hadoop fs -put ./input.txt /input/data
```

### Run WordCount MapReduce Job
```bash
hadoop jar WordCountUsingHadoop-0.0.1-SNAPSHOT.jar com.example.controller.Controller /input/data/input.txt /output1
```

### View Output
```bash
hadoop fs -cat /output1/*
```
### Copy Output from HDFS to Local
```bash
hdfs dfs -get /output1 /opt/hadoop-3.2.1/share/hadoop/mapreduce/
docker cp resourcemanager:/opt/hadoop-3.2.1/share/hadoop/mapreduce/output1/ shared-folder/output/
```

### Input
```bash
hello world
how are you doing
good morning
have a good day
good evening
how was your day
```
### Output
```bash
good    3
how     2
your    2
day     2
world   1
own     1
was     1
hello   1
Create  1
morning 1
dataset 1
are     1
evening 1
have    1
input   1
doing   1
you     1


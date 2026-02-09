# Mini-MapReduce on Amazon EMR

## Project Overview
This project demonstrates a simple **MapReduce pipeline** using **Hadoop Streaming** on **Amazon EMR**.  
The goal is to process a large text dataset stored in **HDFS**, count word occurrences, and output aggregated results back to HDFS.  

The lab showcases:
- Parallel processing across multiple nodes
- Fault tolerance
- Data distribution and HDFS usage
- Performance differences with varying cluster sizes

---

## Dataset Description
We use a **sample dump of Simple English Wikipedia**:

- Source: [Simple English Wikipedia dump](https://github.com/LGDoor/Dump-of-Simple-EnglishWiki)
- File used: `corpus.txt`
- Contents: plain text with multiple Wikipedia articles in English.
- Storage: copied into HDFS input folder:
  ```bash
  hdfs dfs -mkdir -p /user/hadoop/input
  hdfs dfs -put corpus.txt /user/hadoop/input/

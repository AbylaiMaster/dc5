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
  ```

This dataset is suitable for word count experiments and demonstrates distributed processing without being too large for EMR Learner Lab.

Project Structure

project/

mapper.py   

reducer.py

README.md

corpus.txt


Prerequisites

Amazon EMR cluster with Hadoop installed

Python 3 installed on EMR nodes (mapper/reducer are Python scripts)

HDFS input folder containing corpus.txt

Running the MapReduce Job
1. Prepare HDFS output folder
hdfs dfs -rm -r /user/hadoop/output
hdfs dfs -mkdir -p /user/hadoop/output
2. Run Hadoop Streaming Job
hadoop jar /usr/lib/hadoop-mapreduce/hadoop-streaming.jar \
 -files mapper.py,reducer.py \
 -mapper mapper.py \
 -reducer reducer.py \
 -input /user/hadoop/input/ \
 -output /user/hadoop/output
3. Check output
hdfs dfs -ls /user/hadoop/output
hdfs dfs -cat /user/hadoop/output/part-00000 | head

Note: If you re-run the job, either remove the previous output folder or use a new folder name like /user/hadoop/output_2nodes.

Experiment Notes

Scaling experiment: compare runtime with 2 core nodes vs 4 core nodes

Timing: use time to measure job execution

time hadoop jar /usr/lib/hadoop-mapreduce/hadoop-streaming.jar \
 -files mapper.py,reducer.py \
 -mapper mapper.py \
 -reducer reducer.py \
 -input /user/hadoop/input/ \
 -output /user/hadoop/output_2nodes

Record real time for analysis

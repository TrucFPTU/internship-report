---
title: "Blog 2"
date: "2025-12-09"
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# Optimizing the Amazon EMR runtime for Apache Spark with EMR S3A

_By Giovanni Matteo Fumarola, Narayanan Venkateswaran, Syed Shameerur Rahman, Sushil Kumar Shivashankar, and Rajarshi Sarkar – September 24, 2025 – Amazon EMR, Analytics, Best Practices, Intermediate (200), Permalink_

With the Amazon EMR 7.10 runtime, Amazon EMR introduced **EMR S3A**, an enhanced version of the open-source S3A file system connector. This enhanced connector is now automatically configured as the **default S3 file system connector** for Amazon EMR deployment options, including:

- Amazon EMR on EC2
- Amazon EMR Serverless
- Amazon EMR on Amazon EKS
- Amazon EMR on AWS Outposts

while maintaining full compatibility with the open-source Apache Spark APIs.

In the Amazon EMR 7.10 runtime for Apache Spark, the **EMR S3A connector** delivers read performance comparable to **EMRFS**, as demonstrated by the _TPC-DS query benchmark_. The most significant performance improvements are observed for write workloads, with gains of:

- **7%** for static partition overwrites
- **215%** for dynamic partition overwrites compared to EMRFS

In this post, we present the improved read and write performance benefits of using **Amazon EMR 7.10.0 runtime for Apache Spark with EMR S3A**, compared with EMRFS and the open-source S3A file system connector.

---

## Read performance comparison

To evaluate read performance, we used a test environment based on **Amazon EMR runtime version 7.10.0** running:

- Apache Spark **3.5.5**
- Apache Hadoop **3.4.1**

The test infrastructure consisted of an **Amazon EC2 cluster** with nine **r5d.4xlarge instances**:

- Primary node: 16 vCPUs and 128 GB of memory
- Eight core nodes: a total of 128 vCPUs and 1024 GB of memory

The performance evaluation was conducted using a comprehensive benchmarking methodology to ensure accurate and meaningful results.

The input dataset was selected with a **TPC-DS scale factor of 3 TB**, containing **17.7 billion records**, equivalent to approximately **924 GB of compressed data**, partitioned in **Parquet** file format.

Setup instructions and technical details are available in the associated GitHub repository. We used **Spark’s in-memory data catalog** to store metadata for the TPC-DS databases and tables.

To ensure a fair and accurate comparison between **EMR S3A**, **EMRFS**, and the **open-source S3A** implementation, we followed a three-phase benchmarking approach:

### Phase 1: Baseline performance

- Establish baseline performance using the default Amazon EMR configuration with the EMR S3A connector
- Create a reference point for subsequent comparisons

### Phase 2: EMRFS analysis

- Keep the default file system as **EMRFS**
- Keep all other configurations unchanged

### Phase 3: Open-source S3A testing

- Replace only the `hadoop-aws.jar` file with the **open-source Hadoop S3A 3.4.1** implementation
- Keep all other components configured identically

This controlled test environment is critical for the evaluation for the following reasons:

- It isolates the **specific performance impact** of the S3A connector implementation
- It eliminates hidden variables that could skew the results
- It provides accurate measurements of performance improvements between Amazon’s S3A implementation and the open-source alternative

---

## Benchmark execution and results

Throughout the benchmark runs, we maintained **consistent testing conditions and configurations**, ensuring that any observed performance differences could be directly attributed to variations in the S3A connector implementation.

- A total of **104 SparkSQL queries** were executed
- Each query was run for **10 consecutive iterations**
- The **average runtime** across the 10 iterations per query was used for comparison

The average runtime for the 10 iterations on Amazon EMR 7.10 runtime for Apache Spark with **EMR S3A** was **1116.87 seconds**, which is:

- **1.08× faster** than the open-source S3A connector
- Comparable to **EMRFS**

The following table summarizes the metrics:

| Metric                                  | OSS S3A |   EMRFS | EMR S3A |
| --------------------------------------- | ------: | ------: | ------: |
| Average runtime (seconds)               | 1208.26 | 1129.64 | 1116.87 |
| Geometric mean of query runtimes (sec.) |    7.63 |    7.09 |    6.99 |
| Total cost \*                           |   $6.53 |   $6.40 |   $6.15 |

\* Detailed cost estimates are discussed later in this post.

A corresponding chart (not shown here) illustrates the **per-query performance improvements** of EMR S3A over the open-source S3A connector on Amazon EMR 7.10 runtime for Apache Spark:

- Performance speedups vary across queries
- The maximum observed speedup is **1.51× for query q3**, where Amazon EMR S3A outperforms the open-source S3A
- The x-axis orders TPC-DS 3 TB benchmark queries by decreasing performance improvement
- The y-axis represents the speedup factor

---

## Read cost comparison

Our benchmark reports produced both **total runtime** and the **geometric mean of query runtimes** to measure Spark runtime performance. Adding a cost metric provides additional insight.

Cost estimates were computed using the following formulas. These include costs for:

- Amazon EC2
- Amazon Elastic Block Store (Amazon EBS)
- Amazon EMR

Amazon S3 GET and PUT request costs are **not included**.

```text
Amazon EC2 cost (including SSD)
  = number of instances × r5d.4xlarge hourly rate × job runtime (hours)

r5d.4xlarge hourly rate = $1.152 per hour

Root Amazon EBS cost
  = number of instances × Amazon EBS per GB-hourly rate × root EBS size × job runtime (hours)

Amazon EMR cost
  = number of instances × r5d.4xlarge Amazon EMR cost × job runtime (hours)

r5d.4xlarge Amazon EMR cost = $0.27 per hour

Total cost = Amazon EC2 cost + Root Amazon EBS cost + Amazon EMR cost
```

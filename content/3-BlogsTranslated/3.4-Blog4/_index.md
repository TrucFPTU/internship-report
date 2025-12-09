---
title: "Blog 3"
date: "2025-12-09"
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

# Optimizing Amazon EMR runtime for Apache Spark with EMR S3A

_By Giovanni Matteo Fumarola, Narayanan Venkateswaran, Syed Shameerur Rahman, Sushil Kumar Shivashankar, and Rajarshi Sarkar – September 24, 2025 – in Amazon EMR, Analytics, Best Practices, Intermediate (200), Permalink_

With the Amazon EMR 7.10 runtime, Amazon EMR introduced EMR S3A, an enhanced implementation of the open source S3A file system connector. This enhanced connector is now automatically configured as the default S3 file system connector for Amazon EMR deployment options, including Amazon EMR on EC2, Amazon EMR Serverless, Amazon EMR on Amazon EKS, and Amazon EMR on AWS Outposts, while maintaining full compatibility with the open source Apache Spark APIs.

In the Amazon EMR 7.10 runtime for Apache Spark, the EMR S3A connector delivers read performance comparable to EMRFS, as demonstrated by TPC-DS query benchmarks. The most significant performance improvements appear in write operations, with a 7% improvement for static partition overwrites and a 215% improvement for dynamic partition overwrites compared to EMRFS. In this post, we present the improved read and write performance benefits when using the Amazon EMR 7.10.0 runtime for Apache Spark with EMR S3A, compared to EMRFS and the open source S3A file system connector.

## Read performance comparison

To evaluate read performance, we used a test environment based on Amazon EMR runtime version 7.10.0 running Spark 3.5.5 and Hadoop 3.4.1. The test infrastructure consists of an Amazon Elastic Compute Cloud (Amazon EC2) cluster with nine `r5d.4xlarge` instances. The primary node has 16 vCPUs and 128 GB of memory, and the eight core nodes provide a total of 128 vCPUs and 1024 GB of memory.

The performance evaluation was conducted using a comprehensive benchmarking approach to ensure accurate and meaningful results. The input dataset uses a scale factor of 3 TB, with 17.7 billion records, approximately 924 GB of compressed data, partitioned in Parquet format. Setup instructions and technical details are available in a GitHub repository. We used Spark’s in-memory data catalog to store metadata for the TPC-DS databases and tables.

To create a fair and accurate comparison between EMR S3A, EMRFS, and open source S3A implementations, we used a three-phase testing approach:

### Phase 1: Baseline performance

- Establish baseline performance using the default Amazon EMR configuration with the EMR S3A connector
- Create a reference point for subsequent comparisons

### Phase 2: EMRFS analysis

- Keep the default file system as EMRFS
- Keep all other configurations unchanged

### Phase 3: Open source S3A testing

- Replace the `hadoop-aws.jar` file with the open source Hadoop S3A 3.4.1 implementation
- Keep all other component configurations identical

This controlled testing environment is crucial for the following reasons:

- Isolates the specific performance impact of the S3A connector implementation
- Eliminates hidden variables that could skew results
- Provides accurate measurements of performance improvements between the Amazon S3A implementation and the open source alternative

### Test execution and results

Throughout the tests, we kept the test conditions and configurations consistent so that any observed performance differences could be attributed directly to variations in the S3A connector implementation.

We executed a total of 104 SparkSQL queries, each run 10 times. The average runtime over the 10 iterations for each query was used for comparison. The average runtime over 10 iterations on Amazon EMR 7.10 runtime for Apache Spark with EMR S3A was **1116.87 seconds**, which is **1.08x faster than open source S3A** and comparable to EMRFS. The figure (not shown here) illustrates the total runtime in seconds.

The following table summarizes the metrics:

| Metric                              | OSS S3A | EMRFS   | EMR S3A |
| ----------------------------------- | ------- | ------- | ------- |
| Average runtime (seconds)           | 1208.26 | 1129.64 | 1116.87 |
| Geometric mean of queries (seconds) | 7.63    | 7.09    | 6.99    |
| Total cost \*                       | $6.53   | $6.40   | $6.15   |

\* Detailed cost estimates are discussed later in this post.

A chart (not shown) illustrates query-level performance improvements of EMR S3A compared to open source S3A on Amazon EMR 7.10 runtime for Apache Spark. The speedup varies by query, with the fastest achieving a **1.51x** speedup for query `q3`, where Amazon EMR S3A outperforms open source S3A. The x-axis orders the 3 TB TPC-DS benchmark queries by decreasing performance gain observed with Amazon EMR, and the y-axis shows the magnitude of the speedup as a ratio.

## Read cost comparison

Our benchmark outputs total runtime and geometric mean metrics to measure Spark runtime performance. A cost metric provides additional insight. Cost estimates are computed using the following formulas. They include Amazon EC2, Amazon Elastic Block Store (Amazon EBS), and Amazon EMR costs, but exclude Amazon Simple Storage Service (Amazon S3) GET and PUT costs.

- **Amazon EC2 cost (including SSD cost)**  
  `EC2 cost = number of instances * r5d.4xlarge hourly rate * job runtime (hours)`

  - `r5d.4xlarge` hourly rate = **$1.152 per hour**

- **Root Amazon EBS cost**  
  `Root EBS cost = number of instances * EBS per GB-hour rate * root EBS size * job runtime (hours)`

- **Amazon EMR cost**  
  `EMR cost = number of instances * r5d.4xlarge EMR cost * job runtime (hours)`

  - `r5d.4xlarge` Amazon EMR cost = **$0.27 per hour**

- **Total cost**  
  `Total cost = EC2 cost + root EBS cost + EMR cost`

The following table summarizes the cost comparison:

| Metric                    | EMRFS | EMR S3A                            | OSS S3A                              |
| ------------------------- | ----- | ---------------------------------- | ------------------------------------ |
| Runtime (hours)           | 0.50  | 0.48                               | 0.51                                 |
| Number of EC2 instances   | 9     | 9                                  | 9                                    |
| Root Amazon EBS size      | 0 GB  | 0 GB                               | 0 GB                                 |
| Amazon EC2 cost           | $5.18 | $4.98                              | $5.29                                |
| Amazon EBS cost           | $0.00 | $0.00                              | $0.00                                |
| Amazon EMR cost           | $1.22 | $1.17                              | $1.24                                |
| **Total cost**            | $6.40 | $6.15                              | $6.53                                |
| Cost savings vs. baseline | Base  | EMR S3A is 1.04x faster than EMRFS | EMR S3A is 1.06x faster than OSS S3A |

## Write performance comparison

We also benchmarked write performance for the Amazon EMR 7.10 runtime for Apache Spark.

### Static table/partition overwrite

We evaluate static table/partition overwrite write performance across different file systems using the following Spark SQL `INSERT OVERWRITE` query. The `SELECT * FROM range(...)` clause generates data at runtime. This produces approximately 15 GB of data across exactly 100 Parquet files in Amazon S3.

```sql
SET rows=4e9; -- 4 Billion
SET partitions=100;

INSERT OVERWRITE DIRECTORY 's3://${bucket}/perf-test/${trial_id}'
USING PARQUET
SELECT * FROM range(0, ${rows}, 1, ${partitions});
```

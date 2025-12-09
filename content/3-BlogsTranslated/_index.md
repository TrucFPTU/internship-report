---
title: "Translated Blogs"
date: "2025-12-09"
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

This section will list and introduce the blogs you have translated. For example:

### [Blog 1 - AWS Site-to-Site VPN Now Supports IPv6 on External IP Addresses](3.1-Blog1/)

This blog introduces the newly added capability that allows AWS Site-to-Site VPN tunnels to use IPv6 addresses for their external endpoints. This enhancement enables customers to build fully native IPv6 networking without requiring IPv6-to-IPv4 translation, which simplifies network modernization and supports IPv6-only architectures. You will learn why IPv6 adoption is growing, how it helps conserve scarce IPv4 space, reduces networking costs, and helps regulated industries meet IPv6 compliance requirements.

The blog also walks you through deploying a simulated on-premises environment and AWS infrastructure using CloudFormation, configuring an IPv6 VPN connection via Transit Gateway, understanding route propagation behavior, and validating tunnel connectivity in a real-world hybrid network setup.

### [Blog 2 - Optimizing the Amazon EMR Runtime for Apache Spark with EMR S3A](3.2-Blog2/)

This blog explains how Amazon EMR 7.10 significantly improves Apache Spark read and write performance using EMR S3A—an enhanced version of the open-source S3A connector now enabled by default across EMR on EC2, Serverless, EKS, and Outposts. You will learn how EMR S3A provides EMRFS-comparable read performance while delivering major write performance gains, including 7% improvements for static partition overwrites and up to 215% for dynamic partition overwrites.

The article presents the benchmarking architecture (Spark 3.5.5, Hadoop 3.4.1, r5d.4xlarge cluster), the three-phase evaluation methodology (baseline EMR S3A, EMRFS testing, and OSS S3A comparison), and results from executing 104 SparkSQL queries. It also includes cost comparisons covering Amazon EC2, EBS, and EMR charges to give a complete view of performance and cost efficiency when using EMR S3A over EMRFS and the open-source S3A implementation.

### [Blog 3 - Cross-account Disaster Recovery with AWS Elastic Disaster Recovery in Secure Networks (Part 1)](3.3-Blog3/)

This blog is the first part of a two-part series that demonstrates how to build a secure, cross-account disaster recovery (DR) architecture using AWS Elastic Disaster Recovery (DRS). It focuses on the network architecture and required configurations to maintain network isolation, preserve IP addressing schemes, and ensure application continuity during failover and failback operations.

The article explains how AWS PrivateLink, VPC Peering, and Route 53 private hosted zones enable secure, private connectivity to AWS services without exposing traffic to the public internet—making it suitable for highly regulated or sensitive environments. The reference architecture spans production and recovery accounts across two AWS Regions (Ireland and London), each with production, staging, and recovery VPCs. It also details how to configure VPC endpoints for Elastic Disaster Recovery, Amazon S3, AWS STS, and Amazon EC2 to support replication, failover, and reverse replication. This foundation enables resilient, secure DR workflows for mission-critical workloads.

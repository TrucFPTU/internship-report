---
title: "Workshop"
date: "2025-12-09"
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Deploying a Spring Boot REST API application to AWS Elastic Beanstalk

#### Overview

This workshop demonstrates the process of deploying a **Spring Boot REST API** application to **Elastic Beanstalk** in **Single Instance** mode.  
This deployment model **does not use a Load Balancer**, **does not configure Auto Scaling**, and runs entirely within the **default VPC** of the AWS account.

### The goals of this workshop include:

- Building the `.jar` file of the Spring Boot project.
- Creating a simple Elastic Beanstalk Application and Environment.
- Uploading and deploying the `.jar` file to the environment.
- Testing the API using Postman.
- Observing and analyzing logs through _request logs_.

#### Content

1. [Workshop overview](5.1-Workshop-overview)
2. [Prerequiste](5.2-Prerequiste/)
3. [Create environment](5.3-S3-vpc/)
4. [Upload and Deploy](5.4-S3-onprem/)
5. [Access the application and test](5.5-Policy/)
6. [Monitoring and Clean up](5.6-Cleanup/)

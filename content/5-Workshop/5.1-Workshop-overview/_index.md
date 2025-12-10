---
title: "Introduction"
date: "2025-12-09"
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

## Introduction

Elastic Beanstalk (EB) is an application management service (Platform as a Service – PaaS) provided by AWS, enabling developers to deploy and operate web applications without directly managing server infrastructure.

In this workshop, a **Spring Boot REST API** application will be deployed on Elastic Beanstalk using the **Single Instance** configuration and the **Default VPC**, ensuring simplicity, ease of deployment, and suitability for learning, experimentation, and technical demonstration.

The deployment process focuses on the following core steps:

- Packaging the Spring Boot application into an executable `.jar` file.
- Creating an Application and Environment on Elastic Beanstalk.
- Uploading and deploying the application version.
- Testing the service using Postman.
- Monitoring system logs to evaluate application behavior and troubleshoot issues.

Through this workshop, participants will understand the standardized process of deploying a Java backend service on AWS, as well as how Elastic Beanstalk manages the application lifecycle in a Single Instance environment.

This also serves as a foundation for expanding into more advanced scenarios such as **Load Balanced Environments**, integrating **RDS**, or implementing **CI/CD** in future workshops.

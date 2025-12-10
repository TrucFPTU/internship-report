---
title: "Upload and deploy"
date: "2025-12-09"
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

## Upload the .jar file and deploy the application

In the newly created Environment screen → select **Upload and Deploy**.  
Proceed with:

- Selecting the built `.jar` file
- Setting a **Version label** (e.g., `v1-initial`)
- Confirming the deployment

  ![](/images/2-Proposal/Upload.jpg)

Elastic Beanstalk will automatically:

- Upload the file to S3
- Launch a single EC2 instance
- Start the Spring Boot application in the selected Java environment

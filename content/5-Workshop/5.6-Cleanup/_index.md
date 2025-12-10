---
title: "Monitoring and Clean up"
date: "2025-12-09"
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

## Monitoring deployment logs and application logs

Elastic Beanstalk provides two methods for viewing logs:

### 1. Request Logs in Elastic Beanstalk

Accessible via **Logs → Request logs → Last 100 lines**.  
This log shows:

- The Spring Boot startup process
- Error logs if the application fails
- Requests/responses processed by the runtime environment

### 2, CloudWatch Logs

Elastic Beanstalk automatically pushes certain logs to CloudWatch,  
especially system logs from the EC2 instance.

## Clean up resources after deployment

To avoid unexpected costs, it is recommended to delete the resources created after completing the workshop.

### 1. Delete the Environment

Go to Elastic Beanstalk → select the environment → Actions → **Terminate environment**.  
This will remove the EC2 instance, the auto-generated security groups, and related resources.

### 2. Delete the Application (if no longer needed)

Elastic Beanstalk → Application → Actions → **Delete Application**.

### 3. Delete files in S3

Elastic Beanstalk stores `.jar` versions inside an S3 bucket.  
Go to S3 → locate the bucket created by EB → delete the unnecessary versions.

### 4. Review CloudWatch Logs

You may delete the log groups if you want to clean up further.

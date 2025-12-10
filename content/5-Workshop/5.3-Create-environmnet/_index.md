---
title: Create environment
date: "2025-12-09"
weight: 3
chapter: false
pre: " <b> 5.3 </b> "
---

## Create Elastic Beanstalk Application (Default VPC)

Log in to the AWS Console and open the Elastic Beanstalk service.  
Proceed to create a new Application with the following settings:

- **Application name:** set according to the project name
- **Platform:** Java (Corretto) – matching the JDK version used by the application
- **Environment type:** Web Server
- **VPC:** use the Default VPC (Elastic Beanstalk automatically detects and selects it)
- **Environment tier:** Single Instance (no Load Balancer)

Using the Default VPC simplifies the deployment process,  
eliminating the need to manually configure subnets, route tables, or security groups.

---
title: "Proposal"
date: "2025-12-09"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy verbatim** for your report, including this warning.
{{% /notice %}}

In this section, you need to summarize the contents of the workshop that you **plan** to conduct.

# SportShop E-Commerce Platform

## A Cost-Optimized AWS Three-Tier Architecture for Online Sports Retail

---

### 1. Executive Summary

The SportShop E-Commerce Platform is designed to modernize online retail operations using a simplified and cost-optimized AWS architecture, suitable for student projects and small-scale applications. The system uses ReactJS for the frontend, Spring Boot for the backend, and Amazon RDS MySQL for persistent data storage.

To reduce cost and complexity, the architecture removes Amazon Cognito, the Application Load Balancer (ALB), NAT Gateway, and banking payment integration. User authentication is handled directly by the backend, which runs on **Elastic Beanstalk single-instance mode**, while static content is delivered through **S3 + CloudFront**.

Despite being simplified, the architecture still follows AWS best practices for security and CI/CD using ACM, Parameter Store, CloudWatch, CodePipeline, and CodeBuild.

---

### 2. Problem Statement

#### Current Problems

- Slow, manual, and inconsistent deployment workflows
- Risk of leaked or improperly stored credentials
- Limited system monitoring and alerting
- High chance of downtime during updates

#### Proposed Solution

The platform leverages AWS managed services to automate deployments, enhance security, and implement a clean three-layer architecture:

- **Edge:** Route 53, CloudFront (ACM)
- **Application:** Elastic Beanstalk (single-instance)
- **Data:** RDS MySQL, S3, CloudWatch

Secrets such as database credentials and JWT signing keys are securely stored in **Parameter Store**.  
CI/CD is managed through GitLab → CodePipeline → CodeBuild.

#### Benefits

- Lower AWS cost and reduced architectural complexity
- Faster deployments through automation
- Global HTTPS delivery through CloudFront
- Clear separation between frontend, backend, and database layers

---

### 3. Solution Architecture

#### AWS Services Used

- **Amazon Route 53** — DNS
- **Amazon CloudFront** — CDN and HTTPS distribution
- **AWS Certificate Manager** — SSL/TLS certificates
- **Elastic Beanstalk (Single Instance)** — Backend hosting
- **Amazon RDS MySQL** — Main database
- **Amazon S3** — Static hosting & media storage
- **Parameter Store** — Secure secret management
- **CloudWatch** — Logs and metrics
- **CodePipeline + CodeBuild** — CI/CD automation

#### Layered Architecture

**Edge Layer**

- Route 53 → CloudFront
- CloudFront serves the ReactJS frontend globally over HTTPS

**Application Layer**

- Spring Boot backend deployed on Elastic Beanstalk single-instance
- Authentication handled with JWT
- Secure configuration loaded from Parameter Store

**Data Layer**

- RDS MySQL stores structured application data
- S3 stores static content and media files
- CloudWatch provides centralized monitoring

---

![Architecture](/images/2-Proposal/anh1.jpg)

### 4. Technical Implementation

- Configure VPC, subnets, and security groups
- Host frontend on S3 + CloudFront
- Deploy backend with Elastic Beanstalk
- Provision RDS MySQL
- Store secrets in Parameter Store
- CI/CD pipeline: GitLab → CodePipeline → CodeBuild
- Enable monitoring via CloudWatch

**Tech Stack:**

- **Frontend:** ReactJS (S3 + CloudFront)
- **Backend:** Spring Boot (Java 17)
- **Database:** Amazon RDS MySQL
- **CI/CD:** AWS CodePipeline, CodeBuild
- **Security:** IAM, ACM, Parameter Store, CloudWatch

---

### 5. Timeline & Milestones

#### Month 1

- Set up AWS environment (VPC, RDS, S3, CloudFront, Route 53)
- Deploy backend & frontend
- Configure CI/CD pipeline

#### Month 2

- Implement JWT authentication
- Develop modules: product, order, user management
- Set up monitoring & alerting

#### Month 3

- Testing and optimization
- Final deployment
- Documentation and training

---

### 6. Budget Estimation

You can see the cost on the [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=621f38b12a1ef026842ba2ddfe46ff936ed4ab01)
Or download the [budget estimate file](../attachments/budget_estimation.pdf).

| AWS Service                      | Monthly Cost |
| -------------------------------- | ------------ |
| Amazon RDS MySQL                 | $21.84       |
| Elastic Beanstalk (EC2 t3.micro) | $11.68       |
| Amazon S3                        | $0.26        |
| Data Transfer                    | $0.60        |
| CloudFront                       | $0.88        |
| Route 53                         | $0.90        |
| ACM Public Certificate           | $0           |
| CloudWatch Metrics               | $3.02        |
| CodePipeline                     | $0           |
| CodeBuild                        | $0.50        |
| Parameter Store                  | $0           |
| CloudWatch Logs                  | $1.41        |

**Estimated total:** ~$35–40 per month  
**Yearly:** ~$420–480

---

### 7. Risk Assessment

#### Risks

- Single-instance backend → No fault tolerance
- No NAT Gateway → Backend cannot call external APIs
- Risk of JWT token misuse without proper security

#### Mitigation

- Enable Elastic Beanstalk auto-recovery and health checks
- Apply secure authentication & token handling practices
- Utilize RDS automated backups and snapshots

---

### 8. Future Enhancements

1. **Amazon Cognito** — MFA, OAuth, Social Login
2. **Application Load Balancer** — Multi-instance scaling & high availability
3. **NAT Gateway** — Allow backend to call external APIs
4. **Payment Integrations:** VNPay, Stripe, PayPal
5. **RDS Multi-AZ** — High availability and automatic failover
6. **S3 Lifecycle + Glacier** — Cost-optimized long-term storage
7. **AWS X-Ray + OpenSearch** — Tracing and advanced logging
8. **Microservices Architecture with ECS/EKS** — Scale backend into multiple services

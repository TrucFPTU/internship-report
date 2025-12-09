---
title: "Event5"
date: 2025-11-29T08:30:00+07:00
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---

{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy it verbatim** into your report, including this warning.
{{% /notice %}}

# Summary Report: “AWS Well-Architected – Security Pillar Workshop”

### Event Objectives

- Understand the **five pillars** of the AWS Security Framework  
- Learn best practices for IAM, detection, data protection, and incident response  
- Explore prevention strategies for cloud threats commonly seen in Vietnam  
- Practice real-world simulations including IAM policy validation and detection workflows  

### Event Details

- **Date:** 29/11/2025 (Morning)  
- **Time:** 08:30 AM – 12:00 PM  
- **Location:** AWS Vietnam Office  


##  Security Foundation

- Importance of the **Security Pillar** in AWS Well-Architected  
- Core principles: **Least Privilege – Zero Trust – Defense in Depth**  
- Deep dive into the **Shared Responsibility Model**  
- Review of common cloud threats in Vietnam (data exposure, weak IAM, misconfigurations)

---

##  Pillar 1 — Identity & Access Management (IAM)

### Modern IAM Architecture (08:50 – 09:30)

- Avoid long-term credentials → adopt **IAM Roles**, federation, and short-lived tokens  
- Use **IAM Identity Center** for SSO and centralized permission sets  
- Guard multi-account security with **SCP** and **permission boundaries**  
- Strengthen authentication with **MFA**, credential rotation, Access Analyzer  
- *Mini Demo:* Validate IAM policy & simulate access evaluation  

Key learning:  
→ IAM is the **first line of defense**, and misconfiguration is the #1 root cause of cloud breaches.

---

##  Pillar 2 — Detection & Monitoring

### Continuous Monitoring (09:30 – 09:55)

- AWS-native detection tools: **CloudTrail**, **GuardDuty**, **Security Hub**  
- Enable logging across all layers: VPC Flow Logs, ALB Logs, S3 Access Logs  
- Event-driven alerting pipelines using **EventBridge**  
- “Detection-as-Code”: maintain detection rules with IaC + version control  

Key learning:  
→ Security works **only if you monitor** everything continuously and consistently.

---

##  Pillar 3 — Infrastructure Protection

### Network & Workload Security (10:10 – 10:40)

- VPC segmentation: private vs public subnet placement  
- Security Groups vs NACLs: when to use each model  
- Advanced protection: **AWS WAF**, **Shield**, **Network Firewall**  
- Workload coverage: EC2 hardening, EKS/ECS baseline security  

Key learning:  
→ Infrastructure must adopt **multi-layer protection**, not just SG/NACL.

---

##  Pillar 4 — Data Protection

### Encryption, Keys & Secrets (10:40 – 11:10)

- **AWS KMS**: key policies, grants, automatic rotation  
- Encryption at rest and in transit: S3, EBS, RDS, DynamoDB  
- Secrets management with **Secrets Manager** & Parameter Store  
- Data classification and guardrails for controlled access  

Key learning:  
→ Encryption is **not optional**; effective key management is equally important.

---

##  Pillar 5 — Incident Response

### IR Playbook & Automation (11:10 – 11:40)

- Incident lifecycle following AWS best practices  
- Hands-on playbooks:
  - Compromised IAM access key  
  - S3 public exposure  
  - EC2 malware detection  
- Isolation workflow: snapshots, quarantining, evidence collection  
- Automated response using **Lambda** and **Step Functions**

Key learning:  
→ IR must be **prepared before incidents**, not built during the crisis.

---

## Key Takeaways

### Security Mindset

- Prevention > Remediation — eliminate long-lived credentials, enforce Zero Trust  
- Avoid internet-facing resources except when absolutely necessary  
- Everything should be defined and enforced using **Infrastructure as Code**

### Technical Knowledge

- Understand how detection sources (CloudTrail, DNS logs, VPC Flow Logs) form a complete picture  
- Learn structured IR workflow instead of reacting ad-hoc  
- Network Firewall + DNS Firewall help block malicious traffic proactively  
- Managed threat signatures + GuardDuty = continuous threat intelligence

### Practical Skills

- Validating IAM policies with Access Analyzer  
- Setting up org-level CloudTrail with EventBridge  
- Using S3 Block Public Access effectively  
- Applying encryption policies and secret rotation patterns  

---

# Applying to Work

- Implement **short-lived credentials** and enforce MFA across all accounts  
- Introduce **GuardDuty**, **Security Hub**, and centralized logging  
- Review VPC architecture to limit public exposure  
- Apply encryption standards consistently (S3, RDS, EBS, DynamoDB)  
- Build simple IR runbooks for common incidents in the environment  
- Automate alert → containment → remediation using Lambda  

---

# Event Experience

Attending the **AWS Security Pillar Workshop** helped reinforce both theoretical and practical aspects of cloud security.

### Insights from speakers

- The speakers highlighted how security failures often stem from **misconfigurations**, not from AWS itself.  
- Their real-world examples clarified the importance of **least privilege**, network segmentation, and continuous monitoring.

### Practical sessions

- Running IAM access simulations gave me a clearer understanding of effective permission boundaries.  
- The walkthrough of S3 exposure scenarios helped me understand how quickly data can leak without proper guardrails.  
- Learning about AWS Network Firewall and DNS Firewall opened a new view on proactive threat blocking.

### Tools & automation

- GuardDuty findings, Active Threat Defense, and automated remediation workflows showed how security can scale across multi-account environments.  
- I saw how IaC and “Detection-as-Code” can make security predictable and reproducible.

### Discussion & networking

- Discussions with AWS experts and participants helped me understand common security mistakes among Vietnamese companies.  
- Conversations reinforced that **security is a continuous process**, not a one-time effort.

### Lessons learned

- Zero Trust + Least Privilege are non-negotiable.  
- Automate everything: logging, detection, incident response.  
- Prevention reduces 80% of potential incidents.  
- Build IR playbooks before emergencies.

---

### Some event photos
*Add your event photos here*

> The workshop reshaped the way I think about cloud security—from reactive protection to proactive, automated, and continuously improving defense.
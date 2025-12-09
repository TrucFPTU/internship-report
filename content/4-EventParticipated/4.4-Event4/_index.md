---
title: "Event4"
date: 2025-11-17T08:30:00+07:00
draft: true
---



{{% notice warning %}}
⚠️ **Note:** This content is rewritten for variation and should be used only as reference. Do **not copy directly** into your final report.
{{% /notice %}}

# Summary Report: “Cloud Mastery Series #2: DevOps on AWS”

### Event Objectives
- Strengthen understanding of DevOps culture and key performance indicators such as deployment speed and MTTR.  
- Introduce AWS services that support automated CI/CD pipelines from code commit to production release.  
- Explain Infrastructure as Code (IaC) using CloudFormation and CDK to standardize cloud resource provisioning.  
- Provide fundamental knowledge of Docker and AWS container platforms for modern application deployment.  
- Highlight monitoring, observability, and real-world DevOps best practices.  

### Speakers
- **Bao Huynh** – AWS Community Builder  
- **Thinh Nguyen** – AWS Community Builder  
- **Vi Tran** – AWS Community Builder  

---

## Key Highlights

### Limitations of manual (“ClickOps”) operations  
- Consumes significant developer/ops time, delaying feature delivery.  
- Increases risk of misconfiguration due to human error.  
- Creates difficulty maintaining identical environments across development stages.  

### Understanding Infrastructure as Code (IaC)  
- Manages infrastructure using code templates instead of console actions.  
- Improves reliability, automation, and repeatability of deployments.  

### AWS CloudFormation Overview  
- AWS-native IaC service based on JSON/YAML.  
- Supports lifecycle management for entire stacks.  
- Offers drift detection to ensure the infrastructure remains aligned with templates.  

### AWS Cloud Development Kit (CDK)  
- Enables IaC using programming languages like TypeScript, Python, and Java.  
- Construct hierarchy includes:  
  - L1: Raw CloudFormation mappings  
  - L2: High-level abstractions with smart defaults  
  - L3: Ready-to-use architectural patterns  
- Common CDK commands: `init`, `synth`, `deploy`, `diff`, `doctor`  

### Selecting IaC Tools  
- Depends on cloud approach, team expertise, and existing architecture.  
- CDK suits developer-centric teams; CloudFormation fits ops teams; Terraform fits hybrid/multi-cloud setups.  

### Docker & Container Essentials  
- Containers package applications and dependencies into portable, lightweight units.  
- Ensures consistent behavior across all environments.  
- Amazon ECR provides image hosting, vulnerability scanning, and version control.  

### AWS Container Services  
- **ECS:** Simple, AWS-native container orchestration.  
- **EKS:** Full Kubernetes for complex and scalable workloads.  
- **App Runner:** Serverless platform for deploying web applications quickly.  

### CI/CD Pipeline on AWS  
- CodeCommit → CodeBuild → CodeDeploy → CodePipeline form a complete delivery workflow.  
- Supports zero-downtime deployments using blue/green, rolling, or canary strategies.  
- Demonstrations showed automatic deployment triggered by code changes.  

### Monitoring & Observability  
- **CloudWatch:** Central place for logs, metrics, alerts, and dashboards.  
- **X-Ray:** Visual tracing for performance bottlenecks and request flow analysis.  
- Practical guidance for setting up alerting and improving incident response.  

---

## Key Takeaways

### DevOps Mindset  
- Encourages strong collaboration between development and operations.  
- Uses **DORA metrics** to measure and improve team performance.  
- Emphasizes continuous enhancement driven by business priorities.  

### Technical Best Practices  
- IaC ensures consistency, faster provisioning, and fewer configuration issues.  
- CDK constructs help build scalable architectures quickly.  
- Evaluate ECS/EKS based on complexity and operational needs.  
- Reliable CI/CD pipelines reduce risk and accelerate feature delivery.  

### Observability & System Reliability  
- CloudWatch + X-Ray improve troubleshooting and incident detection.  
- Gradual release models (canary/blue-green) help minimize downtime.  
- Drift detection preserves environment correctness and stability.  

### Modernization Strategy  
- Assess existing workloads before planning modernization steps.  
- Adopt incremental migration tactics for safer transitions.  
- Consider modern services like App Runner for rapid deployment improvements.  

---

## Applying to Work  
- Implement Git workflows integrated with automated CodePipeline stages.  
- Start experimenting with CDK to streamline cloud provisioning.  
- Build dashboards in CloudWatch to track performance and reduce MTTR.  
- Encourage internal discussions on container-first architectures.  
- Prepare for AWS DevOps certifications to strengthen personal career growth.  

---

## Event Experience

Attending **“Cloud Mastery Series #2: DevOps on AWS”** delivered a practical and holistic view of DevOps implementation on AWS.

### Learning from Experts  
- Speakers shared hands-on techniques and real-world project experiences.  
- Comparisons between ECS, EKS, and serverless made architectural decisions clearer.  

### Practical Technology Exposure  
- Observed how automated CI/CD pipelines accelerate delivery.  
- Understood how IaC eliminates inconsistencies and streamlines deployment workflows.  
- Practiced interpreting metrics and logs using CloudWatch and X-Ray.  

### Leveraging AWS Technologies  
- CDK simplifies cloud infrastructure creation through code.  
- App Runner demonstrated extremely fast deployment without server management.  

### Interaction & Networking  
- Q&A segments clarified common DevOps challenges and tool choices.  
- Group discussions emphasized aligning DevOps transformation with business value.  

### Lessons Learned  
- Manual ClickOps introduces operational risk—automation is essential.  
- Integration of IaC, CI/CD, and containers builds scalable, resilient systems.  
- Strong observability improves reliability and reduces recovery time.  

---

### Event Photos  
*Insert your photos here*  

> This event significantly enhanced my understanding of DevOps on AWS and provided actionable insights to apply these practices effectively in real-world projects.


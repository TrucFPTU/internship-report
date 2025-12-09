---
title: "Event2"
date: 2025-12-09T19:29:15+07:00
draft: true
---


{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy it verbatim** into your report, including this warning.
{{% /notice %}}

# Summary Report: “Defense from Public Threat: AWS WAF & Application Protection”

### Event Objectives
- Provide an overview of common security risks faced by public-facing applications.
- Explain how AWS WAF operates, how to design effective rule groups, and how to mitigate false positives.
- Demonstrate AWS WAF Bot Control for identifying and blocking malicious automation.
- Introduce AWS Shield’s DDoS defense layers and recent enhancements such as bundled flat-rate pricing.
- Help attendees understand how to build a layered protection model using Route 53, CloudFront, WAF, and Shield.

### Speakers
- **AWS Security Specialists** – experts focused on application and network security (names not disclosed in the provided materials).

---

# Key Highlights

### Understanding modern internet threats
- Public endpoints expose applications to high-frequency attacks that may cause downtime, cost spikes, and compliance issues.
- Consequences include increased infrastructure consumption, data leakage, credential stuffing, and degraded customer trust.
- Threat categories include:
  - **DoS/DDoS attacks** across L3/L4 infrastructure and L7 application traffic.
  - **Application-level vulnerabilities**, including common CVEs and OWASP Top 10 patterns.
  - **Bot activities**, from scraping to credential abuse, with rapid growth in **AI-powered bots** (e.g., GPT, Claude, Meta AI).

### Escalating attack trends
- Recent data shows a continual rise in DDoS frequency year over year.
- AI-based clients significantly increase automated and unpredictable traffic patterns.
- Timelines from 2021–2025 illustrate more frequent and more sophisticated attack behavior.

---

# Architecture & Protection Strategies

### Reinforcing perimeter security using AWS services
- **Amazon Route 53**: Resilient DNS with global redundancy and built-in DDoS protections.
- **Amazon CloudFront**:
  - Acts as a reverse proxy, terminating TLS at edge PoPs.
  - Blocks attacks early at the edge and reduces backend load.
  - Supports private VPC origin mode to hide ALB/EC2 from the public internet.

### AWS Shield (Standard & Advanced)
- Shield provides network-layer filtering, SYN/UDP protection, and health-based traffic mitigation.
- Shield Advanced adds:
  - Automated L7 rule creation
  - Cost protection against scaling surges during attacks
  - Support from the Shield Response Team (SRT)

### New CloudFront Flat-Rate Bundles
- Fixed monthly pricing tiers (Free, Pro, Business, Premium), each bundling CDN + WAF + DDoS + DNS + logging + edge compute.
- Enables predictable budgeting, eliminates surprise bills from unexpected traffic spikes.
- Attack traffic (WAF-blocked or DDoS) **does not count** toward usage quotas.

---

# AWS WAF Deep Dive

### How WAF works
- Web ACLs combine rules, priority ordering, managed rule groups, and default actions.
- Supports multiple actions: **Allow, Block, Challenge, CAPTCHA, Count**.
- Rate-based rules throttle excessive traffic by IP or custom keys.
- Labels allow rule chaining, exclusions, and contextual decisions.

### Recommended rule hierarchy
1. IP allowlists/blocklists  
2. Anti-DDoS managed rules  
3. Rate-based limits  
4. Anonymous/verified client checks  
5. Core OWASP/CVE protections  
6. Bot and fraud detection  
7. Custom business rules (start in **Count** mode)

### Bot Control mechanisms
- Recognizes benign vs. malicious bots using IP reputation, user agents, TLS fingerprints, browser checks, and telemetry.
- Detects anomalies like token reuse, multi-IP hopping, or automation signatures.
- Supports challenges (JS/Challenge/CAPTCHA) before enforcing block rules.

---

# Key Takeaways

### Security Mindset
- Treat internet exposure as a primary risk factor needing a layered, defense-in-depth approach.
- Start with traffic observations (Count mode) before tightening enforcement.
- Combine L3/L4 infrastructure defenses with granular L7 application firewalls.

### Technical Architecture
- CloudFront as the first line of defense reduces compute and bandwidth cost.
- Use WAF labels, scoped-down rules, and managed groups to maintain precision.
- Apply bot interrogation techniques for high-value endpoints like login or checkout.

### Strategy & Cost Management
- Flat-rate CloudFront bundles simplify budgeting for startups and production systems.
- Shield Advanced reduces both downtime and unexpected attack-related costs.
- Incremental rollout + continuous monitoring ensures minimal disruption.

---

# Applying to Work

- **Evaluate public exposure**: Identify all internet-facing endpoints and apply foundational WAF rules.
- **Enable Bot Control** to protect login, search, and API routes from scraping and brute force.
- **Adopt CloudFront** for edge filtering, performance improvement, and origin protection.
- **Configure rate limiting** and leverage Shield where high availability is required.
- **Pilot flat-rate plans** starting from Free/Pro, scaling to Business/Premium when workloads grow.
- **Monitor via CloudWatch** to identify anomalies and iteratively refine rules.

---

# Event Experience

Attending the **“Defense from Public Threat: AWS WAF & Application Protection”** workshop provided a complete and practical view of modern application security.

### Learning from AWS experts
- Gained clarity on how global infrastructures (CloudFront PoPs, Route 53, edge networks) help defend at scale.
- Real incidents and recent trends made the risks and mitigation strategies more tangible.

### Hands-on exploration
- Practiced creating rule groups, configuring rate-based protections, and setting up label-based exceptions.
- Explored bot detection signals and compared challenge vs block strategies.
- Understood how private origins with CloudFront add an additional protection layer.

### Exploring new innovations
- Flat-rate CloudFront bundles stood out as a significant shift—simplifying cost control while bundling security.
- Learned techniques to optimize rules, reduce false positives, and manage premium rule costs with scope-down statements.

### Collaboration & Discussions
- Discussions around incident handling, DDoS response, and rule tuning helped connect theory to real operations.
- Reinforced the importance of phased validation before full enforcement.

### Lessons Learned
- Automated and intelligent protection is essential as threat volume and complexity grow.
- Monitoring traffic patterns before enforcing strict rules avoids operational disruptions.
- Security and cost optimization can go hand-in-hand using CloudFront, Shield, and managed rules.

---

### Some event photos
*Add your event photos here*

> Overall, the workshop strengthened my understanding of modern application security and equipped me with practical strategies to apply these defenses into real-world systems.


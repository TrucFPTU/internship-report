---
title: "Event 1"
date: "2025-12-09"
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Summary Report: “GenAI-powered App-DB Modernization workshop”

### Event Objectives

- Introduce how Generative AI is transforming the software development lifecycle.

- Showcase Amazon Q Developer’s capabilities in coding, testing, documentation, and architecture support.

- Demonstrate how Kiro enhances DevOps and operations through log analysis, troubleshooting, and automation.

- Present the AI-Driven Development model and how teams can integrate AI into daily workflows.

- Provide practical demos to help participants understand how to apply these tools effectively.

### Speakers

- **Toan Huynh** –PMP, Senior Solutions Architect (AWS)
- **My Nguyen** – Senior Solutions Architect | Applied AI Specialist | Thought Leader

### Key Highlights

- Understanding limitations such as scalability issues, high maintenance cost, tight coupling, and slow deployment cycles.
- Limited Scalability – Hard to scale to meet growing user demand.

- High Maintenance Costs – Legacy systems require more resources and effort to maintain.

- Tight Coupling – Components are often interdependent, making updates risky.

#### Identifying the drawbacks of legacy application architecture

- Long product release cycles → Lost revenue/missed opportunities
- Inefficient operations → Reduced productivity, higher costs
- Non-compliance with security regulations → Security breaches, loss of reputation

#### Transitioning to modern application architecture – Microservices

Migrating to a modular system — each function is an **independent service** communicating via **events**, built on three core pillars:

- **Queue Management**: Handles asynchronous tasks reliably.Ensures smooth communication between services without blocking.
- **Caching Strategy**: Optimizes performance and reduces latency.Reduces repeated computations and database load.
- **Message Handling**: Enables flexible, event-driven communication.
  Supports pub/sub, point-to-point, and streaming patterns.

### Domain-Driven Design (DDD) – Workshop Notes

**Overview:**  
DDD helps align software design with business needs, reducing complexity in large systems.  
Focused on applying practical techniques during modernization using AI tools like Amazon Q Developer.

**Four-Step Method (As presented in the workshop):**

- **Identify Domain Events** – Capture key business events that drive the system.
- **Arrange Timeline** – Map events in chronological order to understand flow.
- **Identify Actors** – Determine users or systems interacting with these events.
- **Define Bounded Contexts** – Separate the system into independent domains for clarity and scalability.

**Workshop Case Study:**

- **Bookstore Example:**
  - Demonstrated real-world DDD application.
  - Domain events: “Order Placed”, “Payment Completed”, “Book Shipped”.
  - Bounded contexts: Order Management, Payment Processing, Inventory.

**Context Mapping:**

- 7 patterns introduced for integrating bounded contexts:
  - Shared Kernel, Customer-Supplier, Conformist, Anticorruption Layer, Open Host Service, Published Language, Separate Ways.

**Key Takeaways:**

- Using DDD reduces tight coupling and improves system clarity.
- Amazon Q Developer can assist in modeling, generating code, and documentation for bounded contexts.
- Context mapping ensures smooth communication between independent services during modernization.

#### Event-Driven Architecture

- **Integration patterns**: Publish/Subscribe, Point-to-Point, Streaming
- **Benefits**: Loose coupling, scalable, resilient
- **Sync vs Async**: Trade-offs for performance and reliability

#### Compute Evolution

- **Shared Responsibility**: EC2 → ECS → Fargate → Lambda
- **Serverless**: No server management, auto-scaling, pay-per-use
- **Choosing Compute**: Functions vs Containers based on workload

#### Amazon Q Developer

- Automates **SDLC tasks**: planning → coding → testing → deployment → maintenance
- Supports **code transformation**: Java upgrades, .NET modernization
- Works with **AWS Transform agents**: VMware, Mainframe, .NET migrations

### Key Takeaways

#### Design Mindset

- **Business-first approach**: Start from business needs
- **Ubiquitous language**: Shared vocabulary between business & tech
- **Bounded contexts**: Manage complexity in large systems

#### Technical Architecture

- **Event storming**: Model business processes effectively
- Use **event-driven communication** to reduce tight coupling
- **Integration patterns**: Apply sync, async, pub/sub, streaming as needed
- **Compute selection**: Decide between VM, containers, or serverless based on use case

#### Modernization Strategy

- **Phased Approach**: Follow a clear roadmap, avoid rushing
- **7Rs Framework**: Multiple modernization paths depending on application
- **ROI Measurement**: Focus on cost reduction and business agility

### Applying to Work

- **Apply DDD**: Event storming sessions with business teams
- **Refactor Microservices**: Use bounded contexts to define service boundaries
- **Implement Event-Driven Patterns**: Replace some synchronous calls with async messaging
- **Adopt Serverless**: Pilot AWS Lambda where suitable
- **Try Amazon Q Developer**: Integrate into dev workflow to boost productivity

### Event Experience

**Learning from Speakers**

- Gained best practices in modern application design from AWS and tech experts
- Understood real-world application of DDD and Event-Driven Architecture

**Hands-On Exposure**

- Event storming sessions helped model business processes into domain events
- Learned splitting microservices and defining bounded contexts
- Explored sync vs async communication patterns, including pub/sub, point-to-point, streaming

**Leveraging Tools**

- Explored **Amazon Q Developer** for SDLC automation from planning to maintenance
- Automated code transformation and piloted serverless with **AWS Lambda**

#### Networking and Discussions

- Opportunities to exchange ideas with experts, peers, and business teams
- Enhanced **ubiquitous language** between business and tech
- Real-world examples highlighted the **business-first approach**

#### Lessons Learned

- DDD + Event-Driven patterns reduce **coupling** and improve **scalability** and **resilience**
- Modernization requires a **phased approach** with **ROI measurement**; rushing is risky
- AI tools like **Amazon Q Developer** can **boost productivity** when integrated into workflows

#### Event Photos

_Add your event photos here_

> Overall, the workshop provided technical knowledge and reshaped thinking on application design, system modernization, and cross-team collaboration.

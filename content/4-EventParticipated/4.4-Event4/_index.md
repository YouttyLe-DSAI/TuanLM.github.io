---
title: "Event 4"
weight: 4
chapter: false
pre: " <b> 4.4. </b> "
---

# AWS Cloud Mastery Series #2: DevOps on AWS

> **Time:** Monday, November 17, 2025, 8:30 – 17:00 <br>
> **Location:** AWS Vietnam Office, Bitexco Financial Tower, District 1, Ho Chi Minh City <br>
> **Role:** Attendee (Learner)

### Event Objectives

- Shift mindset from traditional system administration to **DevOps Mindset** and CI/CD culture.
- Master the **AWS Developer Tools** suite (CodeCommit, CodeBuild, CodeDeploy, CodePipeline) to automate development workflows.
- Approach **Infrastructure as Code (IaC)** techniques with CloudFormation and AWS CDK.
- Deep dive into **Containerization** technologies (Docker, ECR, ECS/EKS) and operating Microservices on AWS.
- Master **Monitoring & Observability** to supervise full-stack systems.

### Speakers

- **AWS Technical Team:**
    - Solutions Architects (SA) specializing in DevOps and Modern Application Development.
    - Experts in Containers and Serverless computing.

### Key Highlights

The full-day event covered the journey from mindset to detailed practice:

1.  **CI/CD Pipeline on AWS:**
    - Full workflow demo: Source Control (CodeCommit) -> Build & Test (CodeBuild) -> Deploy (CodeDeploy) -> Orchestration (CodePipeline).
    - Safe deployment strategies like **Blue/Green Deployment** and **Canary Release** to minimize downtime risks.

2.  **Infrastructure as Code (IaC):**
    - The difference between manual "ClickOps" on the Console and defining infrastructure as code.
    - Introduction to **AWS CDK (Cloud Development Kit)**: Allows using familiar programming languages (Python, TS, Java) to provision infrastructure instead of writing lengthy YAML in CloudFormation.

3.  **Container Services:**
    - Reference architecture for Microservices using **Amazon ECS** and **Fargate** (Serverless compute for containers).
    - The process of packaging Docker Images, storing on **ECR**, and automatic security scanning.

4.  **Observability:**
    - Beyond basic logs and metrics, understanding systems through **Distributed Tracing** with AWS X-Ray.

### Key Takeaways

- **DevOps Metrics:** Understanding DORA metrics (Deployment Frequency, Lead Time for Changes...) to measure team efficiency.
- **Git Strategies:** Knowing how to choose the right branching model (GitFlow vs. Trunk-based development) for different project scales.
- **Container Workflow:** Mastering the lifecycle of a container from writing a Dockerfile to running in a Production environment with Auto Scaling.
- **Drift Detection:** How to detect and handle discrepancies between actual Cloud configuration and the defined IaC code.

### Applying to Work

- **Automate Build & Deploy:** Propose shifting from manual deployment (copy-pasting files) to using **AWS CodePipeline** combined with existing Github Actions to reduce human error.
- **Implement IaC:** Start using **AWS CDK** for new projects to easily manage infrastructure versions and reuse code (Constructs).
- **Improve Monitoring:** Integrate **CloudWatch Alarms** and **X-Ray** into critical services to receive early warnings before customers report errors.

### Personal Experience

Attending a full day on DevOps helped me "crack" many aspects of professional software processes:

- The **CI/CD Pipeline** demo was visually satisfying. Just pushing code to the repo triggered automated tests, docker image builds, and server updates without manual intervention.
- I really enjoyed the session on **AWS CDK**. I used to be intimidated by thousand-line CloudFormation templates, but with CDK, defining VPCs, Subnets, and EC2s takes just a few lines of clean, logical Python code.
- The **ECS architecture** drawn on the whiteboard (as captured in the photos) helped me clearly visualize the request flow from Internet Gateway -> ALB -> Target Group -> Container, and how to separate Public/Private subnets for security.

### Event Photos

![aws-mastery-1](/images/4-event/event4-1.png)
![aws-mastery-2](/images/4-event/event4-2.png)
![aws-mastery-3](/images/4-event/event4-3.png)


> Summary: "Automation is King." The event made me realize that any task repeated more than twice should be automated. DevOps is not just tools; it's a culture of efficiency.
---
title: "Week 7 Worklog"
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---
# 📘 Week 7 Worklog – AWS Journey

## 1. Weekly Objectives

During **Week 7**, the focus was on building **High Availability (HA)** and **Scalability** into the architecture. Key objectives included:

*   **Auto Scaling & Load Balancing** – Configuring systems to handle varying traffic loads automatically using ASG and ALB.
*   **Decoupling Architecture** – Using SQS and SNS to enable asynchronous communication between microservices.
*   **Network Monitoring** – Enhancing observability by capturing and analyzing network traffic with VPC Flow Logs.

This week transforms a static infrastructure into a dynamic, resilient system capable of self-healing and scaling based on demand.

---

## 2. Detailed Work Summary

### 🗂 Table of Activities

| Day | Tasks | Start Date | Completion Date | Reference |
| :--- | :--- | :--- | :--- | :--- |
| **Monday** | - Learn about High Availability, Fault Tolerance, and Elasticity concepts<br>- Introduction to Auto Scaling Group (ASG) and Elastic Load Balancer (ELB) | 20/10/2025 | 20/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Tuesday** | - Practice creating Auto Scaling Group for EC2 instance<br>- Set up launch template, scaling policy, and target tracking | 21/10/2025 | 21/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Wednesday** | - Create and configure Application Load Balancer (ALB)<br>- Connect ALB with ASG for load distribution<br>- Test website access through ALB DNS | 22/10/2025 | 22/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thursday** | - Get familiar with Amazon SQS and SNS services<br>- Create SQS queue, SNS topic, and subscription<br>- Send and receive notifications between components | 23/10/2025 | 23/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Friday** | - Enable VPC Flow Logs to monitor network traffic<br>- Analyze logs in CloudWatch Logs<br>- Summarize knowledge about reliability & scaling | 24/10/2025 | 24/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |

---

## 3. Technical Implementation Details

### 3.1 Auto Scaling Group (ASG)
*   **Launch Template:** Created a template defining the AMI, Instance Type (t2.micro), and Security Groups.
*   **Scaling Policies:** Implemented **Target Tracking Scaling Policy** to maintain average CPU utilization at 50%.
*   **Capacity:** Configured Min: 2, Max: 4, Desired: 2 to ensure high availability across multiple Availability Zones.

### 3.2 Application Load Balancer (ALB)
*   **Target Group:** Created a target group for HTTP (Port 80) traffic.
*   **Listener Rules:** Configured the ALB to listen on HTTP and forward traffic to the ASG Target Group.
*   **Health Checks:** Configured `/index.html` as the health check path to ensure only healthy instances receive traffic.
*   **DNS:** Validated access using the auto-generated ALB DNS name (`my-loadbalancer-123.region.elb.amazonaws.com`).

### 3.3 Decoupling with SQS & SNS
*   **SNS (Simple Notification Service):** Created a Topic (`OrderAlerts`) and subscribed an email address for notifications.
*   **SQS (Simple Queue Service):** Created a Standard Queue (`OrderQueue`).
*   **Fan-out Pattern:** Subscribed the SQS queue to the SNS topic. Published a message to SNS and verified it appeared in both the Email inbox and the SQS queue polling.

### 3.4 VPC Flow Logs & Monitoring
*   **Setup:** Enabled Flow Logs for the VPC, sending data to **CloudWatch Logs**.
*   **Analysis:** Used CloudWatch Log Insights to query traffic:
    *   Identified rejected traffic (Security Group blocks).
    *   Monitored SSH connection attempts.
    *   Analyzed internal traffic flow between subnets.

---

## 4. Achievements

By the end of Week 7, the following outcomes were accomplished:

### ✔ Functional Successes
*   Understood the High Availability model and how to maintain system uptime during failures.
*   Successfully implemented **Auto Scaling Group + Load Balancer** to automatically scale EC2 capacity.
*   Configured **SQS/SNS** for reliable message queuing and fan-out notifications.
*   Enabled and interpreted **VPC Flow Logs** to audit network security and connectivity.

### ✔ Skill Development
*   Mastered the relationship between Load Balancers and Auto Scaling Groups.
*   Learned to simulate load (using `stress` tool) to trigger scaling events.
*   Gained experience in "Loose Coupling" architecture design.
*   Improved network troubleshooting skills using log analysis.

---

## 5. Challenges Encountered & Resolutions

**Challenge 1: Unhealthy Targets in ALB**
*   **Issue:** EC2 instances in the Target Group showed status "Unhealthy".
*   **Fix:** The Security Group on the EC2 instances did not allow traffic from the Load Balancer's Security Group. Updated the Inbound Rules to allow HTTP from the ALB SG.

**Challenge 2: ASG Not Scaling Down**
*   **Issue:** After load testing, instances remained running longer than expected.
*   **Fix:** Understood the **Cooldown Period** concept. The ASG was waiting for the default cooldown (300 seconds) before terminating instances to prevent "thrashing".

**Challenge 3: SQS Message Visibility**
*   **Issue:** Messages were processed but reappeared in the queue.
*   **Fix:** Adjusted the **Visibility Timeout** to match the processing time of the consumer application.

---
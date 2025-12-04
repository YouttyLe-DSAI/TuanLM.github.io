---
title: "Week 8 Worklog"
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---
# 📘 Week 8 Worklog – AWS Journey

## 1. Weekly Objectives

**Week 8** served as a comprehensive review and consolidation period. The primary goal was to synthesize all knowledge gained over the past 7 weeks through the lens of the **AWS Well-Architected Framework**. Key objectives included:

*   **Well-Architected Framework**: Deep understanding of the 5 pillars (Operational Excellence, Security, Reliability, Performance Efficiency, Cost Optimization).
*   **Architecture Consolidation**: Reviewing best practices for Security (IAM, KMS), Resilience (Multi-AZ, DR), and Optimization.
*   **Holistic Design**: Designing a complete infrastructure integrating core services (EC2, S3, RDS, VPC, Lambda, CloudFront) and evaluating it against AWS standards.

This week transitions from learning individual services to designing robust, production-ready systems.

---

## 2. Detailed Work Summary

### 🗂 Table of Activities

| Day | Tasks | Start Date | Completion Date | Reference |
| :--- | :--- | :--- | :--- | :--- |
| **Monday** | - Overview of AWS Well-Architected Framework & 5 Pillars<br>- Identify the role and importance of each pillar in system design | 27/10/2025 | 27/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Tuesday** | - Review Secure Architecture Design<br>- Deep dive: IAM, MFA, SCP, KMS, WAF, Shield, GuardDuty, Security Groups vs NACLs | 28/10/2025 | 28/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Wednesday** | - Review Resilient Architecture Design<br>- Topics: Multi-AZ, Multi-Region, DR Strategies, Route 53, Backup & Restore | 29/10/2025 | 29/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thursday** | - Review Performance and Cost Optimization<br>- Topics: Auto Scaling, Global Accelerator, S3 Tiering, Savings Plans | 30/10/2025 | 30/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Friday** | - Comprehensive Practice: Build a sample full-stack architecture<br>- Evaluate according to 5 Well-Architected Framework criteria<br>- Write weekly summary report | 31/10/2025 | 31/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |

---

## 3. Technical Implementation Details

### 3.1 Security Architecture Review (The Security Pillar)
*   **Defense in Depth:** Designed a multi-layer security model:
    *   **Edge:** AWS WAF & Shield (DDoS protection).
    *   **VPC:** Public/Private subnets, NACLs (Stateless), Security Groups (Stateful).
    *   **Identity:** IAM Users with MFA, Roles for service access, Principle of Least Privilege.
    *   **Data:** KMS for encryption at rest (EBS/S3/RDS), TLS/ACM for encryption in transit.

### 3.2 Reliability & Resilience (The Reliability Pillar)
*   **High Availability (HA):** Architected a Multi-AZ deployment for EC2 (via ASG) and RDS (Primary/Standby).
*   **Disaster Recovery (DR):** Reviewed the 4 DR strategies:
    *   Backup & Restore (Cheapest, highest RTO).
    *   Pilot Light.
    *   Warm Standby.
    *   Multi-Site Active/Active (Most expensive, lowest RTO).

### 3.3 Performance & Cost (Efficiency & Optimization Pillars)
*   **Performance:** Implemented CloudFront for edge caching and Global Accelerator for optimized routing to minimize latency.
*   **Cost:**
    *   Analyzed **S3 Lifecycle Policies** (Standard -> IA -> Glacier) to automate storage savings.
    *   Evaluated **Compute Savings Plans** vs. **Reserved Instances** for long-term workloads.
    *   Used **AWS Cost Explorer** to identify "zombie" resources (unattached EIPs, idle ELBs).

### 3.4 Capstone Architecture Practice
*   Designed a 3-Tier Web Application:
    1.  **Presentation Tier:** CloudFront + S3 (Static assets) / ALB (Dynamic requests).
    2.  **Logic Tier:** EC2 Auto Scaling Group in Private Subnets.
    3.  **Data Tier:** RDS Multi-AZ + DynamoDB.
*   Conducted a self-assessment using the **AWS Well-Architected Tool** to identify risks (High/Medium Risk Issues).

---

## 4. Achievements

By the end of Week 8, the following outcomes were accomplished:

### ✔ Conceptual Mastery
*   Gained deep understanding and systematized knowledge of the **AWS Well-Architected Framework**.
*   Able to articulate trade-offs between Cost, Performance, and Reliability.

### ✔ Technical Consolidation
*   Consolidated 4 core architecture domains: Security, Resilience, Performance, and Cost Optimization.
*   Mastered the interaction between core services (e.g., how CloudWatch triggers Lambda for remediation).

### ✔ Practical Application
*   Practiced designing a complete, industry-standard infrastructure from scratch.
*   Learned to perform self-evaluation and architectural reviews.

---

## 5. Challenges Encountered & Resolutions

**Challenge 1: Trade-off Analysis**
*   **Issue:** Difficulty choosing between "Maximum Performance" and "Lowest Cost" (e.g., DynamoDB Provisioned vs. On-Demand).
*   **Resolution:** Used the Well-Architected Framework to prioritize business requirements (e.g., if traffic is unpredictable, On-Demand is better despite potentially higher unit cost).

**Challenge 2: Complexity of DR Strategies**
*   **Issue:** Confusing the nuances between "Pilot Light" and "Warm Standby".
*   **Resolution:** Created a comparison matrix focusing on RTO/RPO targets and active resource count to distinguish them clearly.

**Challenge 3: Security Group vs. NACL Conflicts**
*   **Issue:** Troubleshooting connectivity issues when NACLs blocked return traffic (ephemeral ports).
*   **Resolution:** Reinforced the understanding that NACLs are stateless and require explicit allow rules for both inbound and outbound traffic.

---

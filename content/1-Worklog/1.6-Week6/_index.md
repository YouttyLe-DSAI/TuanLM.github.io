---
title: "Week 6 Worklog"
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---
# 📘 Week 6 Worklog – AWS Journey

## 1. Weekly Objectives

During **Week 6**, the focus shifted to the critical pillars of the Well-Architected Framework: **Security** and **Cost Optimization**. Key objectives included:

*   **Identity & Access Management (IAM)** – Mastering advanced policy structures to enforce the Principle of Least Privilege.
*   **Data Security** – Implementing encryption using AWS KMS and managing credentials with Secrets Manager.
*   **Cost Management** – Analyzing spending patterns via Cost Explorer and setting up automated alerts with AWS Budgets.

This week ensures that the infrastructure built in previous weeks is not only functional but also secure and financially efficient.

---

## 2. Detailed Work Summary

### 🗂 Table of Activities

| Day | Tasks | Start Date | Completion Date | Reference |
| :--- | :--- | :--- | :--- | :--- |
| **Monday** | - Review basic IAM knowledge<br>- Learn advanced IAM Policy (JSON structure, Conditions)<br>- Create custom policies and attach to users/groups | 13/10/2025 | 13/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Tuesday** | - Introduction to AWS Key Management Service (KMS)<br>- Create a Customer Managed Key (CMK)<br>- Apply KMS to encrypt an S3 bucket or an EBS volume | 14/10/2025 | 14/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Wednesday** | - Get familiar with AWS Secrets Manager<br>- Create a secret to store Database connection info<br>- Write a small Lambda script to read the secret | 15/10/2025 | 15/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thursday** | - Explore AWS Billing Dashboard and Cost Explorer<br>- View costs by service, region, and usage type<br>- Set up Cost Anomaly Detection | 16/10/2025 | 16/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Friday** | - Create an AWS Budget and configure email alerts<br>- Write a weekly cost summary report with optimization proposals (stop EC2, cleanup EBS)<br>- Wrap up Week 6 learnings | 17/10/2025 | 17/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |

---

## 3. Technical Implementation Details

### 3.1 Advanced IAM Policies
*   Analyzed the JSON structure: `Version`, `Statement`, `Effect`, `Action`, `Resource`.
*   Created a **Condition-based policy** to restrict access based on source IP or tags:
    ```json
    {
        "Effect": "Allow",
        "Action": "s3:*",
        "Resource": "arn:aws:s3:::my-secure-bucket/*",
        "Condition": {
            "IpAddress": {"aws:SourceIp": "203.0.113.0/24"}
        }
    }
    ```
*   Attached inline policies to specific IAM Groups to enforce separation of duties.

### 3.2 Data Encryption with AWS KMS
*   Created a **Customer Managed Key (CMK)** (Symmetric).
*   Configured **Key Policy** to define Key Administrators and Key Users.
*   Enabled default encryption on an S3 bucket using the new CMK.
*   Tested manual encryption via CLI:
    ```bash
    aws kms encrypt --key-id <key-id> --plaintext fileb://data.txt --output text --query CiphertextBlob
    ```

### 3.3 AWS Secrets Manager Integration
*   Stored RDS credentials (username/password) securely in Secrets Manager.
*   Configured automatic rotation settings (explored concept).
*   Developed a Python (Boto3) script for Lambda to retrieve the secret programmatically, avoiding hardcoded credentials in code.

### 3.4 Cost Management & Optimization
*   **Cost Explorer:** Activated tags (e.g., `Project: WebApp`) to filter costs by specific workloads.
*   **AWS Budgets:** Set up a monthly budget of $10.00 with an alert triggering at 80% usage ($8.00).
*   **Anomaly Detection:** Enabled AWS Cost Anomaly Detection to identify spikes in service usage (e.g., unintended Lambda loops).

---

## 4. Achievements

By the end of Week 6, the following outcomes were accomplished:

### ✔ Functional Successes
*   Mastered creating and applying granular IAM Policies to strictly control resource access.
*   Successfully implemented encryption at rest for S3 and EBS using KMS.
*   Replaced hardcoded database credentials with dynamic retrieval from Secrets Manager.
*   Established a cost governance framework using Budgets and Alerts.

### ✔ Skill Development
*   Deepened understanding of **Shared Responsibility Model** regarding security.
*   Learned to balance security stringency with operational usability.
*   Gained "FinOps" awareness: how to analyze costs, propose optimization measures (e.g., stopping idle EC2, deleting unattached EBS), and maintain efficiency.

---

## 5. Challenges Encountered & Resolutions

**Challenge 1: Access Denied due to KMS Key Policy**
*   **Issue:** An IAM user with Admin permissions could not decrypt a file.
*   **Fix:** Learned that KMS Key Policies are separate from IAM policies. Added the user ARN to the "Key Users" section of the KMS policy.

**Challenge 2: Secrets Manager Caching**
*   **Issue:** Frequent calls to Secrets Manager increased costs/latency.
*   **Fix:** Implemented caching in the Lambda function code to store the secret temporarily during the execution context.

**Challenge 3: Interpreting Cost Explorer Data**
*   **Issue:** Costs for "EC2-Other" were high and unclear.
*   **Fix:** Drilled down by "Usage Type" to identify that the costs were from NAT Gateway data transfer, leading to an architectural review.

---
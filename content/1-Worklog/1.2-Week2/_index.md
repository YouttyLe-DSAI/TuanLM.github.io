---
title: "Week 2 Worklog"
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---


# 📘 Week 2 Worklog – AWS Journey

## 1. Weekly Objectives

During **Week 2**, the primary goal was to gain foundational hands-on experience with core AWS infrastructure services, including:

*   **Amazon S3** – Hosting a static website and managing bucket permissions.
*   **Amazon RDS (MySQL)** – Provisioning a managed relational database and configuring connectivity.
*   **Amazon EC2** – Using an EC2 instance as a secure bastion host to access RDS.
*   **Amazon Route53** – Managing domains and mapping DNS records to AWS services.

This week focuses on building fundamental cloud architecture components that serve as prerequisites for Week 3 tasks involving CloudFront, DynamoDB, and ElastiCache.

---

## 2. Detailed Work Summary

### 🗂 Table of Activities

| Day | Tasks | Start Date | Completion Date | Reference |
| :--- | :--- | :--- | :--- | :--- |
| **Monday** | - Created an S3 bucket for static website content<br>- Uploaded initial HTML/CSS demo files | 15/09/2025 | 15/09/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Tuesday** | - Enabled Static Website Hosting on S3<br>- Configured Bucket Policy to allow public read access<br>- Tested website accessibility via S3 endpoint | 16/09/2025 | 16/09/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Wednesday** | - Created an RDS MySQL instance (Free Tier)<br>- Configured VPC Security Groups for inbound traffic<br>- Recorded DB endpoint & credentials | 17/09/2025 | 17/09/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thursday** | - Launched an EC2 instance and installed MySQL client<br>- Connected from EC2 → RDS using command line<br>- Executed test queries and created sample tables | 18/09/2025 | 18/09/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Friday** | - Explored Route53 functionality<br>- Created a Hosted Zone and DNS records (A/CNAME)<br>- Configured routing from custom domain → S3 static site<br>- Validated website accessibility using domain name | 19/09/2025 | 19/09/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |

---

## 3. Technical Implementation Details

### 3.1 AWS S3 – Static Website Setup
*   Created a new S3 bucket following naming conventions and regional placement.
*   Uploaded static assets (HTML/CSS/Images).
*   Enabled the **Static Website Hosting** feature.
*   Configured `index.html` and `error.html`.
*   Added a **public-read Bucket Policy** to serve content globally.
*   Verified accessibility through the website endpoint:
    ```
    http://<bucket-name>.s3-website-<region>.amazonaws.com
    ```

### 3.2 Amazon RDS – Database Provisioning
*   Launched **RDS MySQL 8.0** instance under Free Tier.
*   Applied secure **Security Group rules** (EC2 → RDS, port 3306).
*   Stored the generated endpoint for later connection.
*   Ensured DB subnet group and VPC configuration were valid for private access.

### 3.3 Amazon EC2 – Secure DB Connectivity
*   Created a `t2.micro` EC2 instance in the same VPC as the RDS instance.
*   Installed MySQL Client:
    ```bash
    sudo yum install mysql -y
    ```
*   Successfully connected to RDS:
    ```bash
    mysql -h <rds-endpoint> -u admin -p
    ```
*   Created a sample database and table for validation purposes.

### 3.4 Amazon Route53 – DNS Configuration
*   Set up a new **Hosted Zone**.
*   Added DNS records:
    *   **A Record** → S3 static website.
    *   **CNAME Record** for testing aliases.
*   Waited for DNS propagation (typically 1–5 minutes).
*   Successfully accessed the static site using a custom domain.

---

## 4. Achievements

By the end of Week 2, the following outcomes were accomplished:

### ✔ Functional Successes
*   Completed a fully operational S3-hosted static website.
*   Enabled access through both S3 website endpoint and Route53 domain.
*   Successfully deployed and connected an RDS MySQL database.
*   Verified secure communication between **EC2 ↔ RDS**.

### ✔ Skill Development
*   Demonstrated understanding of:
    *   IAM roles & permissions.
    *   S3 access control.
    *   VPC networking & Security Groups.
    *   DNS routing concepts.
*   Gained foundational experience with AWS core services.
*   Strengthened understanding of end-to-end cloud application flow.
*   Built confidence working with CLI-based operations (EC2 → RDS).
*   Improved troubleshooting skills (DNS propagation, SG configuration, and public access policies).

---

## 5. Challenges Encountered & Resolutions

**Challenge 1: S3 Public Access Block**
*   **Issue:** Website not accessible due to default S3 public access block.
*   **Fix:** Disabled “Block Public Access” settings and added a correct bucket policy.

**Challenge 2: EC2 -> RDS Connection Timeout**
*   **Issue:** Security Group did not allow inbound MySQL traffic.
*   **Fix:** Modified RDS Security Group to accept traffic specifically from the EC2 Security Group on port 3306.

**Challenge 3: DNS Not Resolving Immediately**
*   **Issue:** Domain took time to propagate in Route53.
*   **Fix:** Waited for TTL window and revalidated using `dig` / `nslookup`.

---

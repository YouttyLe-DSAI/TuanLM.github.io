---
title: "Week 12 Worklog"
weight: 2
chapter: false
pre: " <b> 1.12. </b> "
---
# 📘 Week 12 Worklog – AWS Journey

## 1. Weekly Objectives

**Week 12** marked the conclusion of the AWS learning roadmap. The primary objective was to **synthesize and apply** all skills acquired over the past 11 weeks into a comprehensive **Capstone Project**. Key objectives included:

*   **Holistic Review** – Revisiting core services (EC2, VPC, S3, RDS, Lambda) to ensure deep understanding.
*   **Capstone Project** – Designing, building, and deploying a production-ready "E-Commerce Order Processing System" from scratch.
*   **Operational Excellence** – Implementing CI/CD, Monitoring, and Security best practices.
*   **Self-Assessment** – Evaluating the architecture against the Well-Architected Framework and preparing for certification.

This week transitions the status from "Learner" to "Cloud Practitioner/Architect" ready for real-world challenges.

---

## 2. Detailed Work Summary

### 🗂 Table of Activities

| Day | Tasks | Start Date | Completion Date | Reference |
| :--- | :--- | :--- | :--- | :--- |
| **Monday** | - Review all core services: EC2, S3, RDS, DynamoDB, IAM, VPC, Lambda, CloudFront<br>- Define requirements and architecture for the final project | 24/11/2025 | 24/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Tuesday** | - Start project deployment:<br>- Design VPC (Public/Private subnets), Security Groups<br>- Configure S3 for static assets, CloudFront for CDN | 25/11/2025 | 25/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Wednesday** | - Backend implementation:<br>- Build Lambda functions and API Gateway resources<br>- Connect to DynamoDB/RDS and implement business logic<br>- Integrate CloudWatch Logs & Alarms | 26/11/2025 | 26/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thursday** | - Complete the project:<br>- Add Cognito authentication (SignUp/SignIn)<br>- Finalize CI/CD pipeline (CodePipeline/CodeBuild)<br>- Perform End-to-end system testing | 27/11/2025 | 27/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Friday** | - Write final report and documentation<br>- Prepare presentation (Architecture diagram, Cost analysis, Security review)<br>- Summarize the entire journey and self-evaluate | 28/11/2025 | 28/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |

---

## 3. Technical Implementation Details (Capstone Project)

### 3.1 Project Scope: "Serverless E-Commerce Backend"
*   **Architecture Overview:** A 3-tier serverless web application.
    *   **Frontend:** Hosted on **S3** + **CloudFront**.
    *   **Backend:** **API Gateway** + **Lambda**.
    *   **Database:** **DynamoDB** (Product Catalog) + **RDS MySQL** (Order History).
    *   **Auth:** **Amazon Cognito**.

### 3.2 Infrastructure Setup
*   **VPC Design:** Created a custom VPC with 2 Public Subnets (NAT Gateway, Load Balancer) and 2 Private Subnets (Lambda, RDS).
*   **Security Groups:** Strictly defined rules:
    *   RDS only accepts traffic from Lambda SG on port 3306.
    *   Lambda only accepts traffic from internal VPC endpoints.

### 3.3 Application Logic & Data
*   **Lambda Functions:** Developed Python functions for `CreateOrder`, `GetProducts`, and `ProcessPayment`.
*   **Database Integration:**
    *   Used `Boto3` to scan DynamoDB for product availability.
    *   Used `PyMySQL` to transact SQL commands to RDS for order recording.
*   **Monitoring:** Created a CloudWatch Dashboard to visualize API Latency and Error Rates (4xx/5xx).

### 3.4 Automation & Operations
*   **CI/CD:** Built a pipeline using **AWS CodePipeline**:
    *   Source: GitHub.
    *   Build: AWS CodeBuild (Runs unit tests).
    *   Deploy: CloudFormation/SAM deploy.
*   **Cost Optimization:** Implemented S3 Lifecycle policies for logs and set up an AWS Budget alert for the project.

---

## 4. Achievements

By the end of Week 12 (and the entire course), the following outcomes were accomplished:

### ✔ Project Success
*   Successfully delivered a **production-grade cloud application** combining 10+ AWS services.
*   Demonstrated ability to integrate **Relational (RDS)** and **Non-Relational (DynamoDB)** data stores in a single system.
*   Achieved a **Secure** (Cognito/IAM), **Reliable** (Multi-AZ), and **Performant** (CloudFront/Caching) architecture.

### ✔ Professional Growth
*   Mastered the process of building Cloud applications from **Requirement Analysis** → **Design** → **Implementation** → **Operation**.
*   Developed strong troubleshooting skills for complex distributed systems.
*   Completed the learning roadmap and fully prepared for the **AWS Certified Solutions Architect – Associate** exam.

---

## 5. Challenges Encountered & Resolutions

**Challenge 1: Lambda in VPC Connectivity**
*   **Issue:** Lambda function in Private Subnet lost internet access (could not reach public APIs or DynamoDB).
*   **Fix:** Configured a **NAT Gateway** in the Public Subnet and updated Route Tables. Also used a **VPC Endpoint for DynamoDB** to keep traffic internal and reduce NAT costs.

**Challenge 2: CodePipeline Build Errors**
*   **Issue:** `buildspec.yml` failed due to missing Python dependencies.
*   **Fix:** Updated the `install` phase in the buildspec file to execute `pip install -r requirements.txt`.

**Challenge 3: CORS with Cognito**
*   **Issue:** API Gateway rejected requests with valid tokens due to CORS headers missing on 401 responses.
*   **Fix:** Configured "Gateway Responses" in API Gateway to include CORS headers even for Unauthorized errors.

---

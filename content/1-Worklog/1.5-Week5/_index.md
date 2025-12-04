---
title: "Week 5 Worklog"
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---
# 📘 Week 5 Worklog – AWS Journey

## 1. Weekly Objectives

During **Week 5**, the focus shifted from manual operations ("ClickOps") to **Infrastructure as Code (IaC)** and **Systems Operations**. The goal was to automate resource provisioning and management to ensure consistency and speed. Key objectives included:

*   **Infrastructure as Code (IaC)** – Learning AWS CloudFormation and AWS Cloud Development Kit (CDK).
*   **Automation** – Writing templates and code to deploy S3 buckets and EC2 instances programmatically.
*   **AWS Systems Manager (SSM)** – Centralizing operational data and managing instances without SSH keys.
*   **Operational Excellence** – Implementing automated start/stop workflows for cost saving.

This week marks the transition towards DevOps practices, preparing for scalable infrastructure management.

---

## 2. Detailed Work Summary

### 🗂 Table of Activities

| Day | Tasks | Start Date | Completion Date | Reference |
| :--- | :--- | :--- | :--- | :--- |
| **Monday** | - Introduction to IaC concepts and benefits compared to manual deployment<br>- Get familiar with AWS CloudFormation: template, stack, parameter | 06/10/2025 | 06/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Tuesday** | - Write CloudFormation template to deploy S3 bucket and EC2 instance<br>- Create, update, and delete stack via AWS Console | 07/10/2025 | 07/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Wednesday** | - Introduction to AWS CDK (Cloud Development Kit)<br>- Install AWS CDK, create CDK project using Python or TypeScript<br>- Write CDK code to deploy EC2 instance | 08/10/2025 | 08/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thursday** | - Introduction to AWS Systems Manager (SSM) and key features<br>- Create Parameter Store to store configuration variables | 09/10/2025 | 09/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Friday** | - Practice creating Automation Document in SSM to automatically start/stop EC2<br>- Test Session Manager (access EC2 without SSH key)<br>- Week summary: IaC + SSM demo | 10/10/2025 | 10/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |

---

## 3. Technical Implementation Details

### 3.1 AWS CloudFormation
*   **Template Design:** Created a YAML template defining an `AWS::S3::Bucket` and `AWS::EC2::Instance`.
*   **Parameters:** Used `Parameters` to allow inputting `InstanceType` (e.g., t2.micro) at deployment time.
*   **Stack Operations:**
    *   **Create Stack:** Uploaded the template to CloudFormation Designer.
    *   **Update Stack:** Modified the template (added tags) and applied a changeset.
    *   **Drift Detection:** Checked if resources were modified manually outside the stack.

### 3.2 AWS CDK (Cloud Development Kit)
*   **Setup:** Installed Node.js and the CDK CLI (`npm install -g aws-cdk`).
*   **Initialization:** Created a new project: `cdk init app --language python`.
*   **Coding:** Defined resources using high-level constructs (L2 constructs) in Python.
*   **Deployment:**
    *   `cdk synth`: Generated the CloudFormation template.
    *   `cdk deploy`: Provisioned resources to the AWS account.

### 3.3 AWS Systems Manager (SSM)
*   **Parameter Store:** Created hierarchical parameters (e.g., `/dev/db/password`) as `SecureString` to store sensitive config.
*   **Session Manager:**
    *   Attached the `AmazonSSMManagedInstanceCore` IAM role to the EC2 instance.
    *   Successfully connected to the instance shell via the AWS Console (browser) without opening port 22 (SSH).
*   **Automation:** Executed an SSM Document (`AWS-StopEC2Instance`) to test automated operational tasks.

---

## 4. Achievements

By the end of Week 5, the following outcomes were accomplished:

### ✔ Functional Successes
*   Successfully replaced manual resource creation with repeatable CloudFormation templates.
*   Deployed a functional infrastructure stack using imperative code (CDK).
*   Eliminated the need for SSH keys management using SSM Session Manager.
*   Centralized configuration management using SSM Parameter Store.

### ✔ Skill Development
*   Understood the difference between **Declarative** (CloudFormation) and **Imperative** (CDK) IaC approaches.
*   Learned the importance of **Idempotency** in infrastructure deployment.
*   Gained experience in **Agent-based management** (SSM Agent).
*   Improved security posture by removing the need for public SSH access.

---

## 5. Challenges Encountered & Resolutions

**Challenge 1: CloudFormation YAML Indentation**
*   **Issue:** Stack creation failed due to parsing errors in the YAML file.
*   **Fix:** Used a YAML Linter and VS Code extension "CloudFormation Linter" to validate syntax before uploading.

**Challenge 2: CDK Bootstrapping**
*   **Issue:** `cdk deploy` failed with an error about missing toolkit stack.
*   **Fix:** Learned that the environment must be bootstrapped once per region using `cdk bootstrap aws://<account-id>/<region>`.

**Challenge 3: SSM Agent Not Connecting**
*   **Issue:** EC2 instance did not appear in the Systems Manager Fleet Manager.
*   **Fix:** Discovered that the EC2 instance was missing the necessary IAM Role (`AmazonSSMManagedInstanceCore`). Attached the role and rebooted the instance.

---
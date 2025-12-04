---
title: "Week 1 Worklog"
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---
# 📘 Week 1 Worklog – AWS Journey 

## 1. Weekly Objectives

The primary goals for **Week 1** were to establish the foundational environment for the AWS journey and understand the core operational principles. Key objectives included:

*   **Onboarding:** Familiarize with FCJ internship processes, communication channels, and regulations.
*   **Account Setup:** Complete **AWS Free Tier** registration, configure **AWS CLI**, and enable security baselines (MFA, IAM).
*   **Core Services:** Gain an overview of the AWS ecosystem (Compute, Storage, Networking, Database, Security).
*   **Hands-on Practice:** proficiently use the **AWS Management Console** & **AWS CLI v2**.
*   **Infrastructure:** Deploy and operate an **EC2 t2.micro** instance and perform basic **EBS** operations.
*   **Cost Control:** Establish **AWS Budgets** to monitor spending.

---

## 2. Detailed Work Summary

### 🗂 Implementation Plan vs. Actual

| Category | Plan | Actual | Status |
| :--- | :--- | :--- | :--- |
| **Onboarding & Rules** | Introduction, grasp communication channels | Introduced, noted report standards | ✅ Done |
| **AWS Overview** | Systematize service groups + Mindmap | Completed, categorized notes taken | ✅ Done |
| **Free Tier & Security** | Create account, enable MFA, create IAM user | Enabled MFA; created user + Viewer group | ✅ Done |
| **AWS CLI** | Install CLI, configure profile | Profile `acj-student` set, `sts` test OK | ✅ Done |
| **EC2/EBS/SSH** | Create EC2, SSH, attach EBS | EC2 t2.micro + EBS 8GB gp3, SSH successful | ✅ Done |
| **Cost Management** | Set Budgets $5/month | Received test email alert | ✅ Done |

### 📅 Daily Activities Log

| Day | Task | Start Date | Completion Date | Reference Material |
| :--- | :--- | :--- | :--- | :--- |
| **Monday** | **Onboarding:** FCJ orientation, read regulations, learn report standards | 08/09 | 08/09 | [AWS Journey](https://cloudjourney.awsstudygroup.com) |
| **Tuesday** | **Research:** Explore AWS ecosystem (Compute/Storage/Networking/DB/Security), create mindmap | 09/09 | 09/09 | [AWS Journey](https://cloudjourney.awsstudygroup.com) |
| **Wednesday** | **Account Setup:** Create **AWS Free Tier**, enable **MFA** for root, create **IAM user** + Viewer group | 10/09 | 10/09 | [AWS Journey](https://cloudjourney.awsstudygroup.com) |
| **Thursday** | **CLI Setup:** Install **AWS CLI v2** (Windows), run `aws configure` (profile `acj-student`), check `sts` identity | 11/09 | 11/09 | [AWS Journey](https://cloudjourney.awsstudygroup.com) |
| **Friday** | **Theory:** Study **EC2** (instance types, AMI, EBS, SG, Elastic IP) + Free Tier checklist | 12/09 | 12/09 | [AWS Journey](https://cloudjourney.awsstudygroup.com) |
| **Saturday** | **Practice:** Create **EC2 t2.micro (AL2023)**, create/use **key pair (.pem)**, **SSH**; **attach EBS 8GB**, format & mount | 13/09 | 13/09 | [AWS Journey](https://cloudjourney.awsstudygroup.com) |

---

## 3. Results & Evidence

### 3.1 Resources Created
*   **IAM**: 01 Daily working user (Group: Viewer), **MFA** enabled for root account.
*   **EC2**: `t2.micro` (Free Tier), AMI: Amazon Linux 2023.
*   **Security Group**: Inbound rule opening `22/tcp` restricted to **My IP** only.
*   **EBS**: 8GB `gp3` volume, formatted (`xfs`) and mounted to `/data`.
*   **Budgets**: Monthly budget set to **$5 USD** with email alerts.
*   **CLI Region**: Defaulted to `ap-southeast-1` (Singapore).

### 3.2 CLI Commands Executed
```bash
aws sts get-caller-identity --profile acj-student
aws ec2 describe-regions --profile acj-student --output table
aws ec2 describe-instances --profile acj-student --region ap-southeast-1
aws ec2 create-key-pair --key-name fcj-key --query "KeyMaterial" --output text > fcj-key.pem
```

### 3.3 Evidence Captured
*   Screenshots saved: **MFA enabled** status, **IAM user & group** configuration, **Budgets alert** email, **EC2 instance details**, **EBS volume** attachment, and mount point verification.

---

## 4. Issues & Troubleshooting

| Issue | Cause | Resolution | Result |
| :--- | :--- | :--- | :--- |
| **SSH Connection Failed** | Security Group did not authorize the correct IP | Updated inbound rule -> **My IP** | SSH OK |
| **CLI Missing Credentials** | Wrong profile or region selected | Standardized profile `acj-student`, set default region `ap-southeast-1` | CLI OK |
| **Console Navigation Difficulty** | Unfamiliar User Interface | Used Search bar + Pinned frequent services (EC2, IAM, S3, Budgets) | Faster navigation |

---

## 5. Key Takeaways

*   **Security First**: Always adhere to the **Least-privilege** principle; use IAM users/roles instead of the Root account for daily tasks.
*   **Operations**: Mastered the standard procedure for EC2 creation and **EBS attach/format/mount** lifecycle.
*   **Management**: Understood the synchronization between **Console ↔ CLI** and the importance of **Tagging** (`Project=FCJ, Owner=The Liems, Env=Dev`) for resource tracking.
*   **Cost**: Proactively using **Budgets** is essential to avoid billing surprises.

---

## 6. Cost & Security Summary

*   **Budgets:** Limit set to $5 USD/month (Test email received).
*   **Security:**
    *   Root MFA Enabled.
    *   `.pem` key stored securely.
    *   SSH access restricted to specific IP.
*   **Tagging Strategy:** `Project=FCJ`, `Owner=The Liems`, `Env=Dev`.

## 7. Risks & Mitigation Strategies

*   **Risk:** Exceeding Free Tier limits by forgetting to terminate resources.
    *   *Mitigation:* Set **AWS Budgets** + Perform weekly tag reviews to clean up resources.
*   **Risk:** Leaking Key Pairs/Credentials.
    *   *Mitigation:* Store keys in a secure local directory, add to `.gitignore`, never commit to public repositories.

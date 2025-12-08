---
title: "Event 5"
weight: 5
chapter: false
pre: " <b> 4.5. </b> "
---

# AWS Cloud Mastery Series #3: AWS Well-Architected Security Pillar

> **Time:** Saturday, November 29, 2025, 8:30 – 12:00 <br>
> **Location:** AWS Vietnam Office, Bitexco Financial Tower, District 1, Ho Chi Minh City <br>
> **Role:** Attendee (Learner)

### Event Objectives

- Deeply understand the **Security Pillar** of the AWS Well-Architected Framework, shifting mindset from Perimeter Security to **Zero Trust**.
- Master **Modern IAM** architecture for managing identity and access at scale.
- Learn to build an "immune system" with **Detection-as-Code** and **Automated Remediation**.
- Practice Infrastructure Protection and Data Protection strategies against common attack vectors.

### Speakers

- **Tran Duc Anh** - Cloud Security Engineer Trainee, AWS Cloud Club Captain SGU.
- **Nguyen Tuan Thanh** - Cloud Engineer Trainee.
- **Nguyen Do Thanh Dat** - Cloud Engineer Trainee.
(Featuring the technical team from AWS Cloud Clubs and First Cloud Journey)

### Key Highlights

The workshop deep-dived into the 5 core pillars of security on AWS:

1.  **Identity & Access Management (IAM):**
    - "Kill long-lived credentials" principle: Replace permanent Access Keys with IAM Roles and Temporary Tokens.
    - Using **IAM Access Analyzer** to detect overly permissive policies (like `Principal: *`).
    - Demo on configuring **SSO (Single Sign-On)** for centralized access management across multiple AWS accounts.

2.  **Detection & Continuous Monitoring:**
    - Implementing **Detection-as-Code**: Using CloudFormation/Terraform to enable GuardDuty and Security Hub organization-wide instead of manual clicking.
    - **Runtime Monitoring**: GuardDuty Agent installed deep within EC2/EKS to detect strange processes (process injection) or anomalous file access.

3.  **Infrastructure Protection:**
    - **Defense in Depth** strategy: Layering WAF, Shield at the Edge -> Network Firewall in VPC -> Security Groups at the Instance level.
    - Clearly distinguishing the roles of Security Groups (Stateful) and NACLs (Stateless) in defending against DDoS or Lateral Movement attacks.

4.  **Incident Response (IR):**
    - Automating the incident response process: CloudTrail logs -> EventBridge filter -> Lambda function to automatically isolate malware-infected EC2s or rotate exposed credentials.

### Key Takeaways

- **"No ClickOps" Mindset:** In security, manual configuration is the enemy. Every security rule, from Security Groups to GuardDuty detectors, must be defined by Code (IaC) and version controlled.
- **Shared Responsibility Model:** Clearly understanding what AWS handles (Security *of* the Cloud) and what we must handle (Security *in* the Cloud), especially regarding Data Encryption (at rest/in transit).
- **Power of EventBridge:** It's not just a message bus but the "central nervous system" connecting Detection to Remediation in real-time.
- **Micro-segmentation:** Never trust the internal network. Segmenting VPCs into public/private subnets and tightening them with Security Groups is mandatory.

### Applying to Work

- **Immediate IAM Review:** Audit all IAM Users in company projects, delete unused Access Keys, and enable MFA for 100% of accounts, especially Root accounts.
- **Deploy GuardDuty:** Propose enabling GuardDuty at the Organization level to instantly detect basic threats (like crypto mining, port scanning) with minimal configuration effort.
- **Secret Management:** Stop hardcoding passwords in code or `.env` files immediately. Switch to **AWS Secrets Manager** and configure Automatic Rotation for DB credentials.

### Personal Experience

Honestly, it was a "brain-stretching" but incredibly high-quality morning. Although the speakers were Trainees/Students, the knowledge was deep and battle-tested:

- I was very impressed with the **"Prevention - Nobody has time for incidents"** slide. The quote "Public buckets = your data on the evening news" was both funny and poignant regarding the importance of blocking S3 public access.
- The **Automated Remediation** demo opened my eyes. I used to think Incident Response required someone monitoring screens 24/7, but it turns out Lambda can be written to "neutralize" threats the moment they appear.
- The **Network Attack Vectors** slide visually mapped out a Hacker's path from the Internet through protection layers, helping me clearly visualize a secure network architecture.

### Event Photos

![aws-mastery-1](/images/4-event/event5-1.png)
![aws-mastery-2](/images/4-event/event5-2.png)
![aws-mastery-3](/images/4-event/event5-3.png)

> Summary: Security is not a blocker, but a key enabler for businesses to move faster and safer. This event gave me significant confidence to propose security solutions for upcoming projects.
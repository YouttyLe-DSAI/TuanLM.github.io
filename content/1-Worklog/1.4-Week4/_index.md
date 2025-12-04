---
title: "Week 4 Worklog"
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---
# 📘 Week 4 Worklog – AWS Journey

## 1. Weekly Objectives

During **Week 4**, the primary focus shifted towards **Migration strategies** and **Business Continuity**. The goal was to understand how to move on-premise workloads to the cloud and ensure system resilience against failures. Key objectives included:

*   **Migration Processes** – Understanding the "6 Rs" of migration (Rehost, Replatform, Refactor, etc.).
*   **AWS Database Migration Service (DMS)** – Moving data from a source database to Amazon RDS with minimal downtime.
*   **Elastic Disaster Recovery (EDR)** – Implementing replication and recovery strategies to minimize data loss.
*   **Disaster Recovery (DR) Planning** – Defining RTO (Recovery Time Objective) and RPO (Recovery Point Objective).

This week establishes the critical skills needed for enterprise-grade infrastructure reliability and modernization.

---

## 2. Detailed Work Summary

### 🗂 Table of Activities

| Day | Tasks | Start Date | Completion Date | Reference |
| :--- | :--- | :--- | :--- | :--- |
| **Monday** | - Learn Migration concepts (Lift & Shift, Replatform, Refactor)<br>- Introduction to AWS Database Migration Service (DMS) | 29/09/2025 | 29/09/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Tuesday** | - Practice creating Replication Instance in DMS<br>- Configure source data (simulated on-prem) and target (RDS)<br>- Perform test data migration | 30/09/2025 | 30/09/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Wednesday** | - Introduction to Elastic Disaster Recovery (EDR)<br>- Learn how to set up replication server and recovery instance | 01/10/2025 | 01/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thursday** | - Practice simulating failures: shut down main EC2 and start recovery instance from EDR<br>- Evaluate recovery time (RTO/RPO) | 02/10/2025 | 02/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Friday** | - Create basic Disaster Recovery plan (backup, restore, failover)<br>- Write documentation summarizing Migration + DR processes | 03/10/2025 | 03/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |

---

## 3. Technical Implementation Details

### 3.1 AWS Database Migration Service (DMS)
*   **Replication Instance:** Provisioned a `dms.t2.micro` instance in the VPC to handle the migration workload.
*   **Endpoints Configuration:**
    *   **Source:** Configured an EC2-hosted MySQL database (simulating on-premise) with public access.
    *   **Target:** Connected to the RDS MySQL instance created in Week 2.
*   **Migration Task:** Created a "Full Load" task to migrate existing tables.
*   **Mapping Rules:** Configured schema selection rules to include specific tables (e.g., `Users`, `Products`).

### 3.2 Elastic Disaster Recovery (EDR) Setup
*   Initialized the EDR service in the specific AWS Region.
*   **Agent Installation:** Downloaded and installed the AWS Replication Agent on the source EC2 instance (`Linux`).
*   **Staging Area:** Verified that the replication server was automatically launched in the staging subnet.
*   **Data Replication:** Monitored the initial sync progress until the status reached "Healthy" and "Data replicated".

### 3.3 Failover Simulation (Drill)
*   **Scenario:** Simulating a critical failure by stopping the Source EC2 instance.
*   **Recovery Action:** Initiated a "Recovery Drill" in the EDR console.
*   **Launch Settings:** Configured the launch template (instance type, security groups) for the recovery instance.
*   **Validation:** Successfully SSH'd into the launched Recovery Instance and verified application data integrity.

### 3.4 DR Planning & Documentation
*   Drafted a basic DR plan outlining:
    *   **Backup Strategy:** Automated snapshots vs. Continuous Replication.
    *   **Failover Steps:** The sequence of actions to switch to the recovery site.
    *   **RTO/RPO Analysis:** Measured how long the recovery took (RTO) and how much data was potential lag (RPO).

---

## 4. Achievements

By the end of Week 4, the following outcomes were accomplished:

### ✔ Functional Successes
*   Successfully migrated data between two database endpoints using AWS DMS.
*   Configured continuous block-level replication using Elastic Disaster Recovery.
*   Executed a successful failover drill, bringing up a recovery server within minutes.
*   Verified data consistency between Source and Target systems.

### ✔ Skill Development
*   Understood the complete **Migration lifecycle** (Assess → Mobilize → Migrate & Modernize).
*   Gained practical experience with **Hybrid Cloud** networking concepts (Source → AWS).
*   Deepened knowledge of **Business Continuity Planning (BCP)**.
*   Learned to differentiate between Backup strategies and Disaster Recovery solutions.

---

## 5. Challenges Encountered & Resolutions

**Challenge 1: DMS Connection Errors**
*   **Issue:** The Replication Instance could not connect to the Source EC2 database.
*   **Fix:** Updated the Source Security Group to allow inbound traffic on port 3306 specifically from the Private IP of the DMS Replication Instance.

**Challenge 2: EDR Agent Installation Failure**
*   **Issue:** The replication agent failed to install due to missing IAM permissions.
*   **Fix:** Created an IAM user with the specific programmatic access keys required for the AWS Replication Agent and re-ran the installer.

**Challenge 3: High RTO during Drill**
*   **Issue:** The recovery instance took longer than expected to become available.
*   **Fix:** Optimized the Launch Template to use a pre-warmed AMI or appropriate instance type to speed up the boot process.

---

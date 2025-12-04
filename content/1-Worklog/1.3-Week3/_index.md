---
title: "Week 3 Worklog"
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---
# 📘 Week 3 Worklog – AWS Journey

## 1. Weekly Objectives

During **Week 3**, the primary goal was to optimize application performance and expand data management skills beyond relational databases. Key objectives included:

*   **Amazon CloudFront** – Understanding Content Delivery Networks (CDN) and optimizing static site delivery.
*   **Amazon DynamoDB** – gaining hands-on experience with NoSQL database modeling and operations.
*   **Amazon ElastiCache (Redis)** – Implementing in-memory caching to improve read performance.
*   **AWS CLI Integration** – Advanced interaction with AWS services using command-line scripts.

This week focuses on shifting from a basic architecture to a high-performance, scalable model using caching layers and managed NoSQL services.

---

## 2. Detailed Work Summary

### 🗂 Table of Activities

| Day | Tasks | Start Date | Completion Date | Reference |
| :--- | :--- | :--- | :--- | :--- |
| **Monday** | - Introduction to CDN concepts and CloudFront benefits<br>- Created CloudFront Distribution to serve S3 website content | 22/09/2025 | 22/09/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Tuesday** | - Configured CloudFront behaviors and cache policies<br>- Tested website access via CloudFront URL<br>- Performed Cache Invalidation to update content | 23/09/2025 | 23/09/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Wednesday** | - Introduction to DynamoDB (NoSQL Architecture)<br>- Created DynamoDB tables (Users, Products)<br>- Practiced CRUD operations via AWS Console | 24/09/2025 | 24/09/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thursday** | - Connected and queried DynamoDB using AWS CLI<br>- Wrote scripts to `put-item` and `scan` data programmatically | 25/09/2025 | 25/09/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Friday** | - Explored ElastiCache (Redis & Memcached)<br>- Provisioned a basic Redis cluster<br>- Tested connection from EC2 to store/read cache keys | 26/09/2025 | 26/09/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |

---

## 3. Technical Implementation Details

### 3.1 Amazon CloudFront – CDN Integration
*   Created a distribution pointing to the S3 bucket created in Week 2.
*   Configured **Origin Access Control (OAC)** to restrict S3 access to CloudFront only.
*   Enabled **HTTPS** using the default CloudFront certificate.
*   Tested performance improvement (reduced latency) compared to direct S3 access.
*   Executed manual invalidation for `index.html`:
    ```bash
    aws cloudfront create-invalidation --distribution-id <ID> --paths "/*"
    ```

### 3.2 Amazon DynamoDB – NoSQL Implementation
*   Created a `Users` table with `UserId` as the Partition Key.
*   Performed **CRUD operations** (Create, Read, Update, Delete) via the Management Console.
*   Interacted via AWS CLI to insert data:
    ```bash
    aws dynamodb put-item \
        --table-name Users \
        --item '{"UserId": {"S": "u-101"}, "Name": {"S": "Alice"}, "Role": {"S": "Admin"}}'
    ```
*   Validated data insertion using the `scan` command.

### 3.3 Amazon ElastiCache – Redis Setup
*   Launched an **ElastiCache for Redis** cluster (cache.t2.micro/t3.micro).
*   Configured Security Groups to allow inbound traffic on port `6379` from the EC2 instance.
*   Connected from EC2 using `redis-cli` (installed via `amazon-linux-extras` or `yum`).
*   Tested caching logic:
    ```bash
    set mykey "Hello AWS"
    get mykey
    # Output: "Hello AWS"
    ```

---

## 4. Achievements

By the end of Week 3, the following outcomes were accomplished:

### ✔ Functional Successes
*   Successfully accelerated the S3 static website using CloudFront globally.
*   Demonstrated working knowledge of NoSQL data structures.
*   Established a functional Redis cache cluster accessible from private VPC resources.
*   Integrated AWS CLI for database management, moving beyond Console-only operations.

### ✔ Skill Development
*   Understood the role of edge locations and caching strategies.
*   Mastered the difference between Relational (RDS) and NoSQL (DynamoDB) models.
*   Learned to perform Cache Invalidation when updating static content.
*   Gained experience in securing internal cache layers (ElastiCache) via Security Groups.

---

## 5. Challenges Encountered & Resolutions

**Challenge 1: CloudFront Content Not Updating**
*   **Issue:** Updates to `index.html` on S3 were not reflecting immediately on the website.
*   **Fix:** Learned about TTL (Time To Live) and performed a **CloudFront Invalidation** to force a refresh.

**Challenge 2: DynamoDB CLI Syntax Complexity**
*   **Issue:** Difficulty formatting JSON payloads correctly for CLI commands.
*   **Fix:** Used a JSON generator tool and referred to AWS CLI documentation for correct `AttributeValue` syntax (S, N, etc.).

**Challenge 3: Connecting to Redis from Local Machine**
*   **Issue:** Attempted to connect to ElastiCache from outside the VPC (failed).
*   **Fix:** Understood that ElastiCache is VPC-internal only; utilized the EC2 bastion host established in Week 2 as a jump box.

---

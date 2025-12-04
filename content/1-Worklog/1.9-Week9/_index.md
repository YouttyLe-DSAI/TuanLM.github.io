---
title: "Week 9 Worklog"
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---
# 📘 Week 9 Worklog – AWS Journey

## 1. Weekly Objectives

During **Week 9**, the focus expanded into the **Data & Analytics** domain. The primary goal was to understand the end-to-end data pipeline on AWS, from ingestion to visualization. Key objectives included:

*   **Data Lake Architecture** – Building a scalable storage repository using Amazon S3.
*   **ETL & Data Cataloging** – Using AWS Glue to discover and catalog metadata.
*   **Serverless Querying** – Analyzing data directly in S3 using Amazon Athena (SQL).
*   **Business Intelligence (BI)** – Visualizing insights using Amazon QuickSight.

This week demonstrates how to turn raw data into actionable business intelligence using serverless analytics tools.

---

## 2. Detailed Work Summary

### 🗂 Table of Activities

| Day | Tasks | Start Date | Completion Date | Reference |
| :--- | :--- | :--- | :--- | :--- |
| **Monday** | - Introduction to Data & Analytics ecosystem on AWS<br>- Understand Data Lake concepts, ETL pipeline, and how to connect data sources | 03/11/2025 | 03/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Tuesday** | - Create Data Lake on Amazon S3<br>- Configure directory structure, access permissions<br>- Set up AWS Glue Crawler to identify data schema | 04/11/2025 | 04/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Wednesday** | - Practice AWS Athena to query data in Data Lake<br>- Write basic SQL queries and export results to S3 | 05/11/2025 | 05/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thursday** | - Introduction and practice with Amazon QuickSight<br>- Connect QuickSight with Athena<br>- Create simple dashboard with charts and tables | 06/11/2025 | 06/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Friday** | - Review & consolidate weekly knowledge (Data collection → processing → analysis)<br>- Compare Glue/Athena vs traditional tools<br>- Write summary report | 07/11/2025 | 07/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |

---

## 3. Technical Implementation Details

### 3.1 Data Lake Setup (Amazon S3)
*   **Storage Strategy:** Created an S3 bucket with a logical folder structure (e.g., `raw-data/`, `processed-data/`).
*   **Data Ingestion:** Uploaded sample datasets (CSV/JSON files representing sales logs) to the `raw-data` folder.
*   **Security:** Applied "Block Public Access" and ensured IAM roles were ready for Glue and Athena access.

### 3.2 Metadata Discovery (AWS Glue)
*   **Glue Crawler:** Configured a Crawler to scan the S3 bucket.
*   **IAM Role:** Created a service role granting Glue permissions to read S3 and write to the Glue Data Catalog.
*   **Data Catalog:** Successfully ran the crawler, which automatically detected the schema (columns, data types) and created a table definition in the Glue Database.

### 3.3 Serverless Querying (Amazon Athena)
*   **Configuration:** Set up a query result location in S3 (`s3://my-bucket/athena-results/`).
*   **SQL Operations:** Executed standard SQL queries against the Glue table:
    ```sql
    SELECT product_category, SUM(amount) as total_sales
    FROM sales_data
    GROUP BY product_category;
    ```
*   **Verification:** Verified that Athena could query the CSV data directly without loading it into a database server.

### 3.4 Data Visualization (Amazon QuickSight)
*   **Dataset Creation:** Selected Athena as the data source and imported the table created in the previous steps.
*   **SPICE:** Imported data into SPICE (Super-fast, Parallel, In-memory Calculation Engine) for faster rendering.
*   **Dashboarding:** Built a dashboard containing:
    *   **Bar Chart:** Sales by Region.
    *   **Pie Chart:** Customer Demographics.
    *   **KPI:** Total Revenue.

---

## 4. Achievements

By the end of Week 9, the following outcomes were accomplished:

### ✔ Functional Successes
*   Successfully built a **Serverless Data Lake** using S3.
*   Automated schema discovery using **AWS Glue Crawlers**.
*   Performed ad-hoc SQL analysis using **Athena** without provisioning servers.
*   Created a visual **BI Dashboard** in QuickSight to present data insights.

### ✔ Skill Development
*   Understood the separation of Compute (Athena) and Storage (S3).
*   Gained experience with **Schema-on-Read** concepts vs. traditional Schema-on-Write.
*   Learned IAM permission management between Analytics services (QuickSight <-> Athena <-> S3).

---

## 5. Challenges Encountered & Resolutions

**Challenge 1: Athena Output Location Error**
*   **Issue:** Query failed with "No output location provided".
*   **Fix:** Configured the "Query Result Location" in Athena settings to point to a valid S3 bucket folder.

**Challenge 2: QuickSight Permissions**
*   **Issue:** QuickSight could not access the S3 bucket data.
*   **Fix:** Went to QuickSight "Manage QuickSight" > "Security & Permissions" and explicitly ticked the checkbox for the S3 bucket containing the data.

**Challenge 3: Glue Crawler Classification**
*   **Issue:** Crawler classified CSV data incorrectly due to header issues.
*   **Fix:** Edited the custom classifier in Glue to properly recognize the CSV header row.

---

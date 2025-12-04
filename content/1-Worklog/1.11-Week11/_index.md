---
title: "Week 11 Worklog"
weight: 2
chapter: false
pre: " <b> 1.11. </b> "
---
# 📘 Week 11 Worklog – AWS Journey

## 1. Weekly Objectives

**Week 11** focused on **Application Modernization** via **Serverless Architecture**. The primary goal was to shift from managing infrastructure (EC2) to focusing on code and business logic using event-driven services. Key objectives included:

*   **Serverless Paradigm** – Understanding the shift from Monolithic to Microservices and the benefits of "No-Ops".
*   **Core Serverless Stack** – Mastering AWS Lambda (Compute), API Gateway (Interface), and DynamoDB (NoSQL Data).
*   **Security & Auth** – Implementing user identity management with Amazon Cognito.
*   **Infrastructure as Code** – Using the AWS Serverless Application Model (SAM) to define and deploy serverless resources.

This week provides the skillset to build highly scalable, cost-effective applications that scale to zero when not in use.

---

## 2. Detailed Work Summary

### 🗂 Table of Activities

| Day | Tasks | Start Date | Completion Date | Reference |
| :--- | :--- | :--- | :--- | :--- |
| **Monday** | - Introduction to Modernization and Serverless concepts<br>- Compare Monolithic vs. Microservices architectures<br>- Analyze benefits: Cost, Scalability, Operational overhead | 17/11/2025 | 17/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Tuesday** | - Practice AWS Lambda: create functions, configure triggers (S3/APIGW)<br>- Deploy basic API processing logic<br>- Monitor logs via CloudWatch Logs | 18/11/2025 | 18/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Wednesday** | - Integrate API Gateway with Lambda (REST API)<br>- Connect logic to DynamoDB (CRUD operations)<br>- Test API endpoints using Postman | 19/11/2025 | 19/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thursday** | - Configure Cognito for user authentication (User Pool)<br>- Integrate Cognito Authorizer into API Gateway<br>- Manage access permissions via IAM Roles | 20/11/2025 | 20/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Friday** | - Practice deploying a complete Serverless App using AWS SAM<br>- Testing, logging, and performance optimization<br>- Summarize knowledge and weekly report | 21/11/2025 | 21/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |

---

## 3. Technical Implementation Details

### 3.1 AWS Lambda & Logic
*   **Runtime:** Created Python 3.9 Lambda functions.
*   **Handler:** Implemented the `lambda_handler(event, context)` function to parse JSON input.
*   **Triggers:** Configured API Gateway as the event source.
*   **Logging:** Used `print()` statements to send structured logs to CloudWatch for debugging execution errors.

### 3.2 API Gateway & DynamoDB Integration
*   **API Type:** Built a REST API.
*   **Integration:** Used **Lambda Proxy Integration** to pass the full HTTP request object to the function.
*   **Database:**
    *   Created a DynamoDB table (`Items`) with `ItemId` as the Partition Key.
    *   Used `boto3` in Lambda to perform `put_item`, `get_item`, and `scan` operations based on HTTP methods (POST, GET).

### 3.3 Security with Amazon Cognito
*   **User Pool:** Created a User Pool to handle sign-up and sign-in.
*   **App Client:** Generated a client ID for the application.
*   **Authorizer:** Configured a **Cognito User Pool Authorizer** in API Gateway.
*   **Validation:** Verified that API requests without a valid `Authorization` (JWT) token were rejected with `401 Unauthorized`.

### 3.4 AWS SAM (Serverless Application Model)
*   **Template:** Defined resources (Function, API, Table) in `template.yaml`.
*   **Build:** Ran `sam build` to compile dependencies.
*   **Deploy:** executed `sam deploy --guided` to package code to S3 and create the CloudFormation stack automatically.
*   **Local Testing:** Used `sam local invoke` to test functions before deployment.

---

## 4. Achievements

By the end of Week 11, the following outcomes were accomplished:

### ✔ Functional Successes
*   Transitioned from managing servers to deploying functions.
*   Built a fully functional **Serverless CRUD API**.
*   Secured API endpoints using **JWT Tokens** from Cognito.
*   Automated deployment using **AWS SAM**, replacing manual console actions.

### ✔ Skill Development
*   Thoroughly understood the **Event-Driven Architecture** model.
*   Learned to handle **Stateless** compute limitations.
*   Mastered the process of decomposing a problem into microservices (Auth service, Data service, Logic service).

---

## 5. Challenges Encountered & Resolutions

**Challenge 1: CORS Errors**
*   **Issue:** Calling the API from a browser frontend resulted in Cross-Origin Resource Sharing errors.
*   **Fix:** Enabled CORS in API Gateway settings and ensured the Lambda function returned the `Access-Control-Allow-Origin: *` header in the response object.

**Challenge 2: Lambda Permissions**
*   **Issue:** `AccessDeniedException` when Lambda tried to write to DynamoDB.
*   **Fix:** Updated the Lambda Execution Role (IAM) to include `dynamodb:PutItem` and `dynamodb:GetItem` permissions for the specific table ARN.

**Challenge 3: Cold Starts**
*   **Issue:** The first API call after a period of inactivity took 2-3 seconds.
*   **Fix:** Acknowledged this as a trade-off of Serverless. Optimized imports in the Python code to reduce initialization time.

---

## 6. Plan for Next Week (Preview of Week 12)

*   [ ] **Comprehensive Review**: Consolidate all 11 weeks of knowledge.
*   [ ] **Real-world Project**: Design and implementation of a final Capstone Project.
*   [ ] **Final Report**: Documentation and presentation of the AWS Journey.
*   [ ] **Certification Prep**: Roadmap for AWS Certified Solutions Architect Associate (SAA).

## 5. Challenges Encountered & Resolutions

**Challenge 1: SageMaker Cost Management**
*   **Issue:** SageMaker Notebooks and Endpoints charge per hour even when idle.
*   **Fix:** Created a "Cleanup Script" to delete Endpoints and Stop Notebook instances immediately after lab completion to avoid unexpected bills.

**Challenge 2: IAM Permissions for Rekognition**
*   **Issue:** `AccessDeniedException` when Rekognition tried to read images from the S3 bucket.
*   **Fix:** Updated the Bucket Policy and IAM Role to explicitly grant `s3:GetObject` permission to the user/role calling the Rekognition API.

**Challenge 3: Kendra Indexing Time**
*   **Issue:** Kendra took significant time (30+ minutes) to create an index and sync data.
*   **Fix:** Learned that Kendra is an enterprise-grade service with provisioning time; planned tasks to allow for "waiting time" or worked on Comprehend while Kendra was initializing.

---

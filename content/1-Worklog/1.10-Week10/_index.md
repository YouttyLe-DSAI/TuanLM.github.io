---
title: "Week 10 Worklog"
weight: 2
chapter: false
pre: " <b> 1.10. </b> "
---
# 📘 Week 10 Worklog – AWS Journey

## 1. Weekly Objectives

During **Week 10**, the exploration extended into the **Artificial Intelligence (AI) and Machine Learning (ML)** domain of AWS. The primary goal was to distinguish between building custom models and using pre-trained AI services. Key objectives included:

*   **AWS AI Ecosystem** – Understanding the landscape of ML services (SageMaker) vs. AI Services (Rekognition, Comprehend, Kendra).
*   **Amazon SageMaker** – Experiencing the full ML lifecycle: Build, Train, and Deploy.
*   **Computer Vision & NLP** – Implementing image analysis and natural language processing without deep data science expertise using AWS APIs.
*   **Intelligent Search** – Setting up enterprise search capabilities with Amazon Kendra.

This week highlights how AWS democratizes AI, allowing developers to add intelligence to applications via API calls or build custom models with managed infrastructure.

---

## 2. Detailed Work Summary

### 🗂 Table of Activities

| Day | Tasks | Start Date | Completion Date | Reference |
| :--- | :--- | :--- | :--- | :--- |
| **Monday** | - Overview of AI/ML on AWS<br>- Learn about ML support services: SageMaker, Rekognition, Comprehend, Kendra, Translate, Polly | 10/11/2025 | 10/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Tuesday** | - Practice with Amazon SageMaker:<br>- Create Notebook Instance<br>- Train simple models (Linear Regression/Image Classification)<br>- Deploy endpoint and test predictions | 11/11/2025 | 11/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Wednesday** | - Get familiar with Amazon Rekognition<br>- Demo face and object recognition in images/videos<br>- Integrate Rekognition API into a small web application | 12/11/2025 | 12/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thursday** | - Practice Amazon Comprehend (NLP)<br>- Experiment with Amazon Kendra (contextual intelligent search)<br>- Compare advantages and limitations of each service | 13/11/2025 | 13/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Friday** | - Summarize Week 10 knowledge (AI/ML development process)<br>- Real-world applications of AI/ML in business<br>- Write practice results report and expansion directions | 14/11/2025 | 14/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |

---

## 3. Technical Implementation Details

### 3.1 Amazon SageMaker (Custom ML)
*   **Notebook Instance:** Launched a `ml.t2.medium` Jupyter Notebook instance.
*   **Training:** Used the built-in XGBoost algorithm to train a model on a sample dataset (e.g., predicting house prices or MNIST).
*   **Deployment:** Deployed the trained model to a real-time HTTPS Endpoint.
*   **Inference:** Invoked the endpoint using Python (Boto3) to generate predictions from new data.

### 3.2 Amazon Rekognition (Computer Vision)
*   **Image Analysis:** Uploaded photos to S3 and used the `DetectLabels` API to identify objects (e.g., "Car", "Tree", "Person") with confidence scores.
*   **Facial Analysis:** Used `DetectFaces` to estimate age range, emotion, and gender.
*   **Integration:** Wrote a simple script that triggers a Lambda function when an image is uploaded to S3 to tag it automatically using Rekognition.

### 3.3 Amazon Comprehend (NLP)
*   **Sentiment Analysis:** Processed customer review text to determine sentiment (Positive, Negative, Neutral).
*   **Entity Recognition:** Extracted specific entities (Dates, Locations, Names) from unstructured text documents.

### 3.4 Amazon Kendra (Intelligent Search)
*   **Index Creation:** Created a Kendra Index (Developer Edition).
*   **Data Source:** Connected an S3 bucket containing PDF manuals as the knowledge base.
*   **Querying:** Tested natural language queries (e.g., "How do I reset my device?") in the search console and received precise answers extracted from the documents.

---

## 4. Achievements

By the end of Week 10, the following outcomes were accomplished:

### ✔ Functional Successes
*   Successfully trained and hosted a Machine Learning model using **Amazon SageMaker**.
*   Implemented **Computer Vision** features (Face/Object detection) via API calls.
*    extracted insights from text using **Amazon Comprehend**.
*   Set up a functional document search engine using **Amazon Kendra**.

### ✔ Skill Development
*   Understood the distinction between **AI Services** (High-level APIs for developers) and **ML Services** (SageMaker for Data Scientists).
*   Gained experience in **Model Inference** costs and endpoint management.
*   Learned how to integrate AI capabilities into existing applications using AWS SDKs.

---

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

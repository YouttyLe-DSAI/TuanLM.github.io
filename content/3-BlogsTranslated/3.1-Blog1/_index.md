---
title: "Blog 1"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# **Model Customization, RAG, or Both: A Case Study with Amazon Nova**

by Flora Wang, Anila Joshi, Baishali Chaudhury, Sungmin Hong, Jae Oh Woo, and Rahul Ghosh on 10 APR 2025 in [Advanced (300)](https://aws.amazon.com/blogs/machine-learning/category/learning-levels/advanced-300/), [Amazon Bedrock](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/amazon-machine-learning/amazon-bedrock/), [Amazon Machine Learning](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/amazon-machine-learning/), [Amazon Nova](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/amazon-machine-learning/amazon-bedrock/amazon-nova/), [Amazon SageMaker](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/sagemaker/), [Generative AI](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/generative-ai/), [Technical How-to](https://aws.amazon.com/blogs/machine-learning/category/post-types/technical-how-to/)

As enterprises and developers increasingly seek to optimize their language models for specific tasks, the decision between model customization and Retrieval Augmented Generation (RAG) becomes critical. In this post, we aim to address this growing need by providing clear, actionable guidance and best practices on when to use each approach, helping you make informed decisions tailored to your unique requirements and goals.

The introduction of [Amazon Nova](https://aws.amazon.com/ai/generative-ai/nova/) models represents a significant advancement in the AI landscape, offering new opportunities for Large Language Model (LLM) optimization. In this post, we demonstrate how to effectively implement model customization and RAG using Amazon Nova models as a base. We conducted a comprehensive comparative study between model customization and RAG using the latest Amazon Nova models and share these valuable insights.

## **Approach and Foundation Model Overview**

In this section, we discuss the differences between fine-tuning and RAG, present common use cases for each approach, and provide an overview of the foundation model used for our experiments.

### **Demystifying RAG and Model Customization**

RAG is a technique to enhance the capabilities of pre-trained models by allowing them to access external, domain-specific data sources. It combines two components: external knowledge retrieval and response generation. This allows pre-trained language models to dynamically incorporate external data during the response generation process, enabling more contextually accurate and updated outputs. Unlike fine-tuning, in RAG, the model does not undergo any training, and model weights are not updated to learn domain knowledge. While fine-tuning implicitly uses domain-specific information by embedding necessary knowledge directly into the model, RAG explicitly utilizes domain-specific information through external retrieval.

Model customization refers to adjusting a pre-trained language model to better suit specific tasks, domains, or datasets. Fine-tuning is one such technique that helps introduce task-specific or domain-specific knowledge to improve model performance. It adjusts model parameters to better align with the nuances of the target task while leveraging its general knowledge.

### **Common Use Cases for Each Approach**

RAG is optimal for use cases requiring dynamic or frequently updated data (such as customer support FAQs and e-commerce catalogs), domain-specific insights (such as legal or medical Q&A), scalable solutions for broad applications (such as software-as-a-service (SaaS) platforms), multimodal data retrieval (such as document summarization), and strict adherence to secure or sensitive data (such as financial and regulatory systems).

In contrast, fine-tuning thrives in scenarios requiring precise customization (such as personalized chatbots or creative writing), high accuracy for narrow tasks (such as code generation or specialized summarization), ultra-low latency (such as real-time customer interactions), stability with static datasets (such as domain-specific glossaries), and cost-effective scaling for high-volume tasks (such as call center automation).

While RAG excels in real-time grounding in external data and fine-tuning specializes in static, structured, and personalized workflows, the choice between them often depends on nuanced factors. This post provides a comprehensive comparison of RAG and fine-tuning, clarifying the strengths, limitations, and contexts where each approach delivers the best performance.

### **Introduction to Amazon Nova Models**

[Amazon Nova](https://aws.amazon.com/ai/generative-ai/nova/) is a new generation of foundation models (FMs) providing state-of-the-art intelligence and industry-leading price performance. Amazon Nova Pro and Amazon Nova Lite are multimodal models excelling in accuracy and speed, with Amazon Nova Lite optimized for fast processing and low cost. Amazon Nova Micro focuses on ultra-low latency text tasks. They provide fast inference, support agentic workflows with [Amazon Bedrock Knowledge Bases](https://aws.amazon.com/bedrock/knowledge-bases/) and RAG, and enable fine-tuning on text and multimodal data. Optimized for cost-efficient performance, they are trained on data in over 200 languages.

## **Solution Overview**

To evaluate the effectiveness of RAG versus model customization, we designed a comprehensive experimental framework using a set of AWS-specific questions. Our study utilized Amazon Nova Micro and Amazon Nova Lite as the base FMs and examined their performance across different configurations.

We structured our evaluation as follows:

* **Base Model:**
  * Used Amazon Nova Micro and Amazon Nova Lite.
  * Generated answers for AWS-specific questions without additional context.
* **Base Model with RAG:**
  * Connected base models to Amazon Bedrock Knowledge Bases.
  * Provided access to relevant AWS documentation and blogs.
* **Model Customization:**
  * Fine-tuned both Amazon Nova models using 1,000 AWS-specific question-answer pairs generated from the same set of AWS articles.
  * Deployed customized models via provisioned throughput.
  * Generated answers for AWS-specific questions with the fine-tuned models.
* **Hybrid Approach (Model Customization + RAG):**
  * Connected fine-tuned models to Amazon Bedrock Knowledge Bases.
  * Provided fine-tuned models access to relevant AWS articles at inference time.

In the following sections, we guide you through setting up the second and third approaches (base model with RAG and model customization with fine-tuning) in Amazon Bedrock.

## **Prerequisites**

To follow this post, you need:

* An AWS account and appropriate permissions.
* An [Amazon Simple Storage Service](http://aws.amazon.com/s3) (Amazon S3) bucket with two folders: one for your training data and one for your model output and training metrics.

## **Implementing RAG with Base Amazon Nova Model**

In this section, we walk through the steps to implement RAG with a base model. To do so, we create a knowledge base. Complete the following steps:

1. On the Amazon Bedrock console, select **Knowledge Bases** in the navigation pane.
2. In Knowledge Bases, select **Create**.

![01](/images/3-BlogsTranslated/ML-18029-image001.jpg)

3. On the **Configure data source** page, provide the following:
   * Specify the Amazon S3 location of the documents.
   * Specify the chunking strategy.
4. Select **Next**.

![configure_kb](/images/3-BlogsTranslated/ML-18029-image002.jpg)

5. On the **Select embedding model and configure vector store** page, provide the following:
   * In the **Embedding model** section, select the embedding model used to embed the chunks.
   * In the **Vector database** section, create a new vector store or use an existing one where embeddings will be stored for retrieval.
6. Select **Next**.

![select_embedding_models](/images/3-BlogsTranslated/ML-18029-image003.jpg)

7. On the **Review and create** page, review the settings and select **Create knowledge base**.

![kb_confirmation](/images/3-BlogsTranslated/ML-18029-image004.jpg)

## **Fine-tuning Amazon Nova Models via Amazon Bedrock API**

In this section, we provide detailed instructions on how to fine-tune and host custom Amazon Nova models using Amazon Bedrock. The following diagram illustrates the solution architecture.

![ft_diagram](/images/3-BlogsTranslated/ML-18029-image005.png) 

### **Creating a Fine-Tuning Job**

Fine-tuning Amazon Nova models through the Amazon Bedrock API is a streamlined process:

1. On the Amazon Bedrock console, select **us-east-1** as your AWS Region. At the time of writing, Amazon Nova fine-tuning is only available in us-east-1.
2. Select **Custom Models** under **Foundation Models** in the navigation pane.
3. Under **Customize models**, select **Create fine-tuning job**.

![ft_job_creation](/images/3-BlogsTranslated/ML-18029-image006.jpg)

4. For **Source model**, select **Select model**.
5. Select **Amazon** as the provider and choose your preferred Amazon Nova model.
6. Select **Apply**.

![ft_model_selection](/images/3-BlogsTranslated/ML-18029-image007.jpg)

7. For **Fine-tuned model name**, enter a unique name for the fine-tuned model.
8. For **Job name**, enter a name for the fine-tuning job.
9. In **Input data**, enter the S3 bucket locations for source (training data) and destination (model output and training metrics) and optionally your validation dataset location.

![ft_input_data](/images/3-BlogsTranslated/ML-18029-image008.jpg)

### **Configuring Hyperparameters**

For Amazon Nova models, you can customize the following hyperparameters:

| Parameter | Range/Constraints |
| :---: | :---: |
| Epochs | 1–5 |
| Batch Size | Fixed at 1 |
| Learning Rate | 0.000001–0.0001 |
| Learning Rate Warmup Steps | 0–100 |

### **Preparing Dataset for Compatibility with Amazon Nova Models**

Similar to other LLMs, Amazon Nova requires prompt-completion pairs, also known as Q&A pairs, for Supervised Fine-Tuning (SFT). This dataset must contain the ideal results you want the language model to generate for specific tasks or prompts. Refer to the [Amazon Nova Data Preparation Guide](https://docs.aws.amazon.com/nova/latest/userguide/customize-fine-tune-prepare.html) for best practices and example formatting.

### **Checking Fine-Tuning Job Status**

After creating the fine-tuning job, select **Custom Models** in the navigation pane. You will find the current fine-tuning job listed under **Jobs**. You can use this page to track the status.

![examine_ft_status](/images/3-BlogsTranslated/ML-18029-image009.png)

When the status changes to **Completed**, you can select the job name to navigate to the **Training job overview** page to find specifications, S3 locations, and hyperparameters used.

![ft_job_overview](/images/3-BlogsTranslated/ML-18029-image010.png)

### **Hosting the Fine-Tuned Model with Provisioned Throughput**

Once the job is successful:

1. Go to **Custom Models** > **Models** and select your model.
2. Select **Purchase Provisioned Throughput**.
3. Choose a commitment term (no commitment, 1 month, or 6 months).

![select_custom_models](/images/3-BlogsTranslated/ML-18029-image011.jpg)

---

## **Evaluation Framework and Results**

### **Multi-LLM Judge to Reduce Bias**

![multi-llm-judge](/images/3-BlogsTranslated/ML-18029-image013.png)

We used a scoring system (0-10) with two judges: **Claude 3.5 Sonnet** and **Llama 3.1 70B**.

### **Response Quality Comparison**

Fine-tuning and RAG both improved response quality by ~30% for Nova Lite. The hybrid approach (Fine-tuning + RAG) improved quality by **83%**.

![nova_lite](/images/3-BlogsTranslated/ML-18029-image014.jpg)

Notably, Nova Micro (smaller model) with the hybrid approach performed nearly as well as larger models.

![nova_micro_lite](/images/3-BlogsTranslated/ML-18029-image015.jpg)

### **Latency and Token Usage**

Fine-tuning reduced base model latency by ~50%, while RAG reduced it by ~30%.

![latency](/images/3-BlogsTranslated/ML-18029-image016.jpg)

Fine-tuning reduced average total tokens by over 60%, whereas RAG doubled token usage due to context switching.

![tokens](/images/3-BlogsTranslated/ML-18029-image017.jpg)

---

## **Conclusion**

We recommend combining **Model Customization** and **RAG** for Q&A tasks to maximize performance. Fine-tuning is superior for tone/style adjustment and latency-sensitive tasks, while RAG is essential for dynamic data.

---

**About the Authors**

| Photo | Introduction |
| :---: | :--- |
| <img src="/images/3-BlogsTranslated/florawan.jpg" width="220" alt="Mengdie (Flora) Wang"> | **Mengdie (Flora) Wang** is a Data Scientist at the AWS Generative AI Innovation Center, helping customers architect scalable AI solutions. She specializes in agent-based AI systems and model customization. |
| <img src="/images/3-BlogsTranslated/SungminHong.jpg" width="220" alt="Sungmin Hong"> | **Sungmin Hong** is a Senior Applied Scientist at Amazon's Generative AI Innovation Center. He holds a PhD from NYU and was a postdoc at Harvard Medical School. |
| <img src="/images/3-BlogsTranslated/jae.jpg" width="220" alt="Jae Oh Woo"> | **Jae Oh Woo** is a Senior Applied Scientist at AWS, specializing in custom model solutions. He holds a PhD in Applied Mathematics from Yale. |
| <img src="/images/3-BlogsTranslated/rahul.png" width="220" alt="Rahul Ghosh"> | **Rahul Ghosh** is an Applied Scientist at Amazon. He works with AWS customers to accelerate GenAI adoption and holds a PhD from the University of Minnesota. |
| <img src="/images/3-BlogsTranslated/baishali.jpeg" width="220" alt="Baishali Chaudhury"> | **Baishali Chaudhury** is an Applied Scientist at AWS focusing on real-world GenAI applications. She has a background in computer vision and healthcare AI. |
| <img src="/images/3-BlogsTranslated/anilajo.jpg" width="220" alt="Anila Joshi"> | **Anila Joshi** is an AWSI Geo Leader with over a decade of experience building AI solutions, helping customers implement secure GenAI strategies. |
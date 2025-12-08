---
title: "Blog 2"
weight: 1
chapter: false
pre: " <b> 3.2 </b> "
---
# **Migrating CDK Version 1 Applications to CDK Version 2 with Amazon Q Developer**

by Dr. Rahul Sharad Gaikwad, Tamilselvan P, and Vinodkumar Mandalapu on April 30, 2025 on [Amazon Q](https://aws.amazon.com/blogs/devops/category/amazon-q/).

## **Introduction:**

[AWS Cloud Development Kit (AWS CDK)](https://aws.amazon.com/cdk/) is an open-source software development framework to define cloud infrastructure in code and provision it through [AWS CloudFormation](https://aws.amazon.com/cdk/). As of June 1, 2023, AWS CDK version 1 is no longer supported. To avoid potential issues using an outdated version and to take advantage of the latest features and improvements, we recommend upgrading to AWS CDK version 2.

[Amazon Q Developer](https://aws.amazon.com/q/developer/), a generative AI-powered assistant for software development, enhances the efficiency of software development teams. It facilitates the creation of deployment-ready Infrastructure as Code (IaC) for AWS CloudFormation, AWS CDK, and Terraform. By using Amazon Q, developers can accelerate IaC development, enhance code quality, and reduce the likelihood of configuration errors.

This post demonstrates how [Amazon Q Developer](https://aws.amazon.com/q/developer/) supports upgrading an existing [AWS CDK v1](https://docs.aws.amazon.com/cdk/v1/guide/home.html) application to [AWS CDK v2](https://docs.aws.amazon.com/cdk/v1/guide/home.html).

## **Prerequisites**

*   [AWS Builder ID](https://docs.aws.amazon.com/signin/latest/userguide/sign-in-aws_builder_id.html) or [AWS IAM Identity Center](https://aws.amazon.com/iam/identity-center/) credentials controlled by your organization

*   Supported IDE, such as Visual Studio Code

*   [AWS Toolkit](https://aws.amazon.com/visualstudiocode/) IDE extension

*   [Authentication and connection](https://docs.aws.amazon.com/toolkit-for-vscode/latest/userguide/connect.html#whisperer)

*   Node.js

*   AWS CDK version 1

*   AWS CDK version 2

## **Plan**

In this blog post, I will explore a code example where I created a VPC, Subnet, and ECS Fargate cluster using AWS CDK version 1. Then, I will explain how you can use Amazon Q to convert the code from CDK v1 to CDK v2.

1\. To start this process, I began by asking Amazon Q Developer to provide the necessary steps to migrate from CDK version 1 to version 2, as outlined below.

Can you provide the steps to migrate from cdk version 1 to version 2?

![Amazon Q Developer outlines a comprehensive process for upgrading an AWS CDK application from version 1 to version 2.](/images/3-BlogsTranslated/step1-b2.gif)

2\. In the screenshot above, Amazon Q Developer outlined several steps we can take to make the necessary changes. The first step is to update dependencies. If I need guidance on how to update dependencies, I can ask Amazon Q Developer for help again by requesting steps related to updating dependencies as shown below.

Can you provide the steps to update dependencies?

![Amazon Q Developer provides detailed, AI-powered guidance for upgrading project dependencies by analyzing the existing codebase, identifying outdated or deprecated libraries and frameworks, and recommending precise updates to ensure compatibility with newer language versions.](/images/3-BlogsTranslated/step2-b2.gif)

3\. After updating the dependencies, the next step is to update the import statements. For guidance on how to update import statements, I can ask the Amazon Q Developer assistant for help again by asking for steps related to how to import statements as shown below.

@workspace Can you provide the steps to update import statements?

![Amazon Q Developer advises on updating import statements by analyzing the current code context and guiding developers to replace old or outdated import paths with the latest ones.](/images/3-BlogsTranslated/step3-b3.gif)

In the screenshot above, if you notice, I prefixed the prompt with `@workspace`, which automatically includes the most relevant parts of my workspace code as context.

4\. If any errors occur while updating the code according to Amazon Q Developer's recommendations, I can use Amazon Q Developer to debug the issue and provide the necessary input to resolve it.

![](/images/3-BlogsTranslated/step4-1-b2.gif)

5\. After completing the required steps, I can deploy the application using AWS CDK version 2 by running the `cdk deploy` command.

![Deploying the updated AWS CDK version 2 application, which involves synthesizing CDK stacks to generate CloudFormation templates and deployment artifacts, bootstrapping the AWS environment to provision necessary resources.](/images/3-BlogsTranslated/step5-b2.gif)

6\. In addition to other capabilities, Amazon Q also offers code review functionality. To start a code review, simply select Amazon Q and use the `/review` command. Then, I will have the option to review active files or the entire open workspace. Select your preference and Amazon Q will analyze your project and provide comprehensive review results.

![](/images/3-BlogsTranslated/review-b2.gif)

7\. Amazon Q Developer can also generate documentation, including README files. To generate documentation, select Amazon Q and enter the `/doc` command. Amazon Q will automatically generate a README file for your project. I can then review the generated documentation, accept the changes, or provide specific instructions for further modifications.

![](/images/3-BlogsTranslated/readme-b2.gif)

## **Conclusion**

In this blog, I demonstrated how Amazon Q Developer can simplify and accelerate the process of upgrading from AWS CDK version 1 to version 2, ensuring your cloud infrastructure remains secure, efficient, and aligned with the latest AWS innovations. AWS CDK version 2 offers a unified, streamlined library with improved performance and ongoing support, making infrastructure management easier and more reliable.

By leveraging Amazon Q Developer, a generative AI-powered assistant, teams can automate Infrastructure as Code development, enhance code quality, and minimize configuration errors. Together, these tools empower development teams to confidently modernize and scale their AWS environments, turning the upgrade process into a seamless opportunity for innovation and growth.

## **Resources**

To learn more about [Amazon Q Developer](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/what-is.html), check out the following resources:

*   [Amazon Q Developer Workshop](https://catalog.workshops.aws/qwords/en-US)

*   [Amazon Q Developer User Guide](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/what-is.html)

To learn more about AWS CDK, check out the following resources:

*   [AWS CDK Workshop](https://workshops.aws/categories/CDK)

*   [How to use Amazon Q Developer to deploy a serverless web application with AWS CDK](https://aws.amazon.com/blogs/devops/how-to-use-amazon-q-developer-to-deploy-a-serverless-web-application-with-aws-cdk/)

About the authors:

| Profile Photo | About the authors |
| :---: | :--- |
| <img src="/images/3-BlogsTranslated/Profile-Photo-10.jpg" width="220" alt="Dr. Rahul Sharad Gaikwad"> | **Dr. Rahul Sharad Gaikwad** is a Solutions Architect at AWS, driving cloud innovation through customer workload migration and modernization. As a Generative AI and DevOps enthusiast, he architects cutting-edge solutions and is recognized as an APJC HashiCorp Ambassador. He holds a PhD in AIOps and has received the Man of Excellence Award, Indian Achiever Award, Best PhD Thesis Award, Research Scholar of the Year Award, and Young Researcher Award. |
| <img src="/images/3-BlogsTranslated/Vinod-123.jpg" width="220" alt="Vinodkumar Mandalapu"> | **Vinodkumar Mandalapu** is a DevOps Consultant at AWS, specializing in designing and deploying cloud-based infrastructure and deployment pipelines on AWS. With extensive experience in automating and streamlining software delivery, he has helped organizations of all sizes leverage the power of the cloud to drive innovation, improve scalability, and enhance operational efficiency. In his free time, he enjoys traveling and spending quality time with his son. |
| <img src="/images/3-BlogsTranslated/Tamil-123.jpg" width="220" alt="Tamilselvan P"> | **Tamilselvan P** is a DevOps Consultant at AWS, focused on architecting and implementing cloud-native systems as well as continuous delivery within the ecosystem. Leveraging his comprehensive expertise in orchestrating and refining software release processes, he has assisted customers across various industries and scales in harnessing cloud technology to innovate faster, increase scalability, and enhance operational performance. In his free time, he enjoys playing cricket. |
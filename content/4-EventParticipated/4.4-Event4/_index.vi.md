---
title: "Event 4"
weight: 4
chapter: false
pre: " <b> 4.4. </b> "
---

# AWS Cloud Mastery Series #2: DevOps on AWS

> **Thời gian:** Thứ Hai, ngày 17/11/2025, 8:30 – 17:00 <br>
> **Địa điểm:** AWS Vietnam Office, Tòa nhà Bitexco Financial Tower, Quận 1, TP.HCM <br>
> **Vai trò:** Người tham dự (Learner)

### Mục Đích Của Sự Kiện

- Chuyển đổi tư duy từ quản trị hệ thống truyền thống sang **DevOps Mindset** và văn hóa CI/CD.
- Làm chủ bộ công cụ **AWS Developer Tools** (CodeCommit, CodeBuild, CodeDeploy, CodePipeline) để tự động hóa quy trình phát triển.
- Tiếp cận kỹ thuật **Infrastructure as Code (IaC)** với CloudFormation và AWS CDK.
- Hiểu sâu về công nghệ **Containerization** (Docker, ECR, ECS/EKS) và cách vận hành Microservices trên AWS.
- Nắm vững kiến thức về **Monitoring & Observability** để giám sát hệ thống full-stack.

### Danh Sách Diễn Giả

- **Đội ngũ chuyên gia kỹ thuật từ AWS (AWS Technical Team):**
    - Các Solutions Architect (SA) chuyên sâu về DevOps và Modern Application Development.
    - Chuyên gia về Container và Serverless computing.

### Nội Dung Nổi Bật

Sự kiện diễn ra cả ngày với lộ trình từ tư duy đến thực hành chi tiết:

1.  **CI/CD Pipeline trên AWS:**
    - Demo luồng quy trình đầy đủ: Source Control (CodeCommit) -> Build & Test (CodeBuild) -> Deploy (CodeDeploy) -> Orchestration (CodePipeline).
    - Các chiến lược triển khai an toàn như **Blue/Green Deployment** và **Canary Release** để giảm thiểu rủi ro downtime.

2.  **Infrastructure as Code (IaC):**
    - Sự khác biệt giữa việc click chuột trên Console (ClickOps) và viết code định nghĩa hạ tầng.
    - Giới thiệu **AWS CDK (Cloud Development Kit)**: Cho phép dùng ngôn ngữ lập trình quen thuộc (Python, TS, Java) để tạo hạ tầng thay vì viết YAML dài ngoằng trong CloudFormation.

3.  **Container Services:**
    - Kiến trúc tham chiếu cho Microservices sử dụng **Amazon ECS** và **Fargate** (Serverless compute for containers).
    - Quy trình đóng gói Docker Image, lưu trữ trên **ECR** và scan bảo mật tự động.

4.  **Observability:**
    - Không chỉ là log và metric cơ bản, mà là khả năng "thấu hiểu" hệ thống qua **Distributed Tracing** với AWS X-Ray.

### Những Gì Học Được

- **DevOps Metrics:** Hiểu về các chỉ số DORA (Deployment Frequency, Lead Time for Changes...) để đo lường hiệu quả của team.
- **Chiến lược Git:** Biết cách chọn mô hình phân nhánh phù hợp (GitFlow vs Trunk-based development) cho từng quy mô dự án.
- **Container Workflow:** Nắm vững vòng đời của một container từ lúc viết Dockerfile đến khi chạy trên môi trường Production với Auto Scaling.
- **Drift Detection:** Cách phát hiện và xử lý khi cấu hình thực tế trên Cloud bị lệch so với code IaC đã định nghĩa.

### Ứng Dụng Vào Công Việc

- **Tự động hóa Build & Deploy:** Đề xuất team chuyển từ deploy thủ công (copy paste file) sang sử dụng **AWS CodePipeline** kết hợp với Github Actions hiện tại để giảm lỗi con người.
- **Triển khai IaC:** Bắt đầu sử dụng **AWS CDK** cho các dự án mới để dễ dàng quản lý version của hạ tầng và tái sử dụng code (Constructs).
- **Cải thiện giám sát:** Tích hợp **CloudWatch Alarms** và **X-Ray** vào các service quan trọng để nhận cảnh báo sớm trước khi khách hàng phàn nàn về lỗi.

### Trải Nghiệm Cá Nhân

Tham gia trọn vẹn một ngày về DevOps giúp em "vỡ" ra nhiều điều về quy trình làm phần mềm chuyên nghiệp:

- Phần Demo về **CI/CD Pipeline** thực sự "đã mắt". Chỉ cần push code lên repo, hệ thống tự động chạy test, build docker image và update lên server mà không cần đụng tay vào.
- Em rất thích phần chia sẻ về **AWS CDK**. Trước đây nhìn file CloudFormation template dài cả nghìn dòng em rất ngại, nhưng với CDK thì việc định nghĩa VPC, Subnet, EC2 chỉ tốn vài dòng code Python ngắn gọn, logic như viết app vậy.
- Kiến trúc **ECS** được vẽ trên bảng (như trong ảnh chụp) giúp em hình dung rõ ràng luồng đi của request từ Internet Gateway -> ALB -> Target Group -> Container, và cách chia Public/Private subnet để bảo mật.

### Một số hình ảnh tại sự kiện

![aws-mastery-1](/images/4-event/event4-1.png)
![aws-mastery-2](/images/4-event/event4-2.png)
![aws-mastery-3](/images/4-event/event4-3.png)


> Tổng kết: "Automation is King". Sự kiện giúp em nhận ra rằng mọi thao tác lặp lại quá 2 lần đều nên được tự động hóa. DevOps không chỉ là tool, nó là văn hóa làm việc hiệu quả.
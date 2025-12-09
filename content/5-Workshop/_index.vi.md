---
title: "Tong quan "
weight: 5
chapter: false
pre: " <b> 5. </b> "
---
# Xây dựng Trợ lý Hợp đồng Thông minh (Smart Contract Assistant) trên AWS

#### Giới thiệu

Trong kỷ nguyên số, việc xử lý và phân tích các văn bản pháp lý phức tạp là một thách thức lớn đối với nhiều doanh nghiệp. Workshop này sẽ hướng dẫn bạn xây dựng **"Smart Contract Assistant"** - một ứng dụng web hiện đại tích hợp Trí tuệ nhân tạo tạo sinh (Generative AI) để giải quyết vấn đề này.

Ứng dụng cho phép người dùng tương tác với các tài liệu hợp đồng thông qua ngôn ngữ tự nhiên. Bạn có thể đặt câu hỏi về các điều khoản, yêu cầu tóm tắt nội dung, hoặc thậm chí yêu cầu AI soạn thảo một hợp đồng mới dựa trên các mẫu có sẵn.

#### Kiến trúc giải pháp

Giải pháp được xây dựng hoàn toàn trên kiến trúc **Serverless** (Không máy chủ) của AWS, giúp tối ưu hóa chi phí vận hành và khả năng mở rộng. Điểm nhấn của kiến trúc là việc áp dụng kỹ thuật **RAG (Retrieval-Augmented Generation)**, cho phép AI truy xuất thông tin chính xác từ kho dữ liệu riêng của bạn thay vì chỉ dựa vào kiến thức đã được huấn luyện trước.

Các thành phần chính của hệ thống bao gồm:

1.  **AI & LLM (Amazon Bedrock):**
    *   Đây là "trái tim" của ứng dụng. Chúng ta sử dụng Amazon Bedrock để truy cập các mô hình ngôn ngữ lớn (LLM) tiên tiến như Claude 3 (Haiku/Sonnet) thông qua API.
    *   Bedrock chịu trách nhiệm hiểu ngữ cảnh câu hỏi, tổng hợp thông tin từ tài liệu và sinh ra câu trả lời tự nhiên.

2.  **Backend & Computing (AWS Lambda & API Gateway):**
    *   Sử dụng **AWS Lambda** để chạy các đoạn code Python xử lý logic nghiệp vụ (tìm kiếm vector, gọi API Bedrock, xử lý dữ liệu đầu vào) mà không cần quản lý máy chủ.
    *   **Amazon API Gateway** đóng vai trò là cửa ngõ, tiếp nhận các yêu cầu từ phía người dùng (Frontend) và định tuyến chúng đến các hàm Lambda tương ứng.

3.  **Database & Storage (Amazon S3 & DynamoDB):**
    *   **Amazon S3:** Đóng vai trò là kho lưu trữ ("Data Lake") chứa các file hợp đồng mẫu (.docx, .pdf), các file metadata và dữ liệu vector đã được nhúng (embeddings) phục vụ cho việc tìm kiếm ngữ nghĩa.
    *   **Amazon DynamoDB:** Cơ sở dữ liệu NoSQL hiệu năng cao dùng để lưu trữ thông tin người dùng, quản lý phiên làm việc (Sessions) và lịch sử tin nhắn chat, đảm bảo độ trễ thấp nhất khi truy xuất.

4.  **Frontend & Authentication (AWS Amplify & Cognito):**
    *   Giao diện người dùng được xây dựng bằng React/VueJS và được deploy tự động thông qua **AWS Amplify**.
    *   **Amazon Cognito** cung cấp cơ chế đăng ký, đăng nhập và bảo mật, đảm bảo chỉ những người dùng được ủy quyền mới có thể truy cập ứng dụng.

#### Mục tiêu học tập

Sau khi hoàn thành workshop này, bạn sẽ nắm vững:
*   Cách triển khai một ứng dụng **Full-stack** trên AWS từ con số 0.
*   Hiểu và ứng dụng mô hình **RAG** để kết hợp dữ liệu doanh nghiệp với sức mạnh của LLM.
*   Kỹ năng làm việc với **Infrastructure as Code** thông qua Serverless Framework.
*   Cấu hình và tích hợp các dịch vụ AWS cốt lõi: S3, DynamoDB, Lambda, API Gateway và Bedrock.

#### Nội dung thực hành

1. [Tổng quan về workshop](5.1-Workshop-overview/)
2. [Các bước chuẩn bị](5.2-Prerequiste/)
3. [Thiết lập cơ sở hạ tầng (S3, DynamoDB)](5.3-Infrastructure/)
4. [Xây dựng Backend (Lambda, IAM)](5.4-Backend/)
5. [Triển khai Fullstack (Amplify)](5.5-Fullstack/)
6. [Dọn dẹp tài nguyên](5.6-Cleanup/)
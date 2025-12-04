---
title: "Worklog Tuần 12"
weight: 2
chapter: false
pre: " <b> 1.12 </b> "
---
# 📘 Báo cáo công việc Tuần 12 – Hành trình AWS

## 1. Mục tiêu hàng tuần

**Tuần 12** đánh dấu sự kết thúc của lộ trình học tập AWS. Mục tiêu chính là **tổng hợp và ứng dụng** tất cả các kỹ năng đã học trong 11 tuần qua vào một **Dự án Cuối khóa (Capstone Project)** toàn diện. Các mục tiêu chính bao gồm:

*   **Ôn tập tổng thể** – Rà soát lại các dịch vụ cốt lõi (EC2, VPC, S3, RDS, Lambda) để đảm bảo hiểu sâu.
*   **Dự án Capstone** – Thiết kế, xây dựng và triển khai một "Hệ thống Xử lý Đơn hàng E-Commerce" hoàn chỉnh từ con số không.
*   **Vận hành xuất sắc** – Triển khai CI/CD, Giám sát và các phương pháp bảo mật tốt nhất.
*   **Tự đánh giá** – Đánh giá kiến trúc dựa trên Well-Architected Framework và chuẩn bị cho kỳ thi chứng chỉ.

Tuần này chuyển đổi vị thế từ "Người học" sang "Kỹ sư/Kiến trúc sư đám mây" sẵn sàng cho các thách thức thực tế.

---

## 2. Tóm tắt công việc chi tiết

### 🗂 Bảng hoạt động

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| **Thứ Hai** | - Ôn tập dịch vụ cốt lõi: EC2, S3, RDS, DynamoDB, IAM, VPC, Lambda, CloudFront<br>- Xác định yêu cầu và kiến trúc cho dự án cuối khóa | 24/11/2025 | 24/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Ba** | - Bắt đầu triển khai dự án:<br>- Thiết kế VPC (Subnet Public/Private), Security Groups<br>- Cấu hình S3 cho tài nguyên tĩnh, CloudFront cho CDN | 25/11/2025 | 25/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Tư** | - Triển khai Backend:<br>- Xây dựng Lambda functions và API Gateway<br>- Kết nối Database (RDS/DynamoDB) và xử lý logic<br>- Tích hợp CloudWatch Logs & Alarms | 26/11/2025 | 26/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Năm** | - Hoàn thiện dự án:<br>- Thêm xác thực Cognito (Đăng ký/Đăng nhập)<br>- Hoàn tất pipeline CI/CD (CodePipeline/CodeBuild)<br>- Kiểm thử hệ thống đầu cuối (End-to-end) | 27/11/2025 | 27/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Sáu** | - Viết báo cáo và tài liệu cuối kỳ<br>- Chuẩn bị bài thuyết trình (Sơ đồ kiến trúc, phân tích chi phí, bảo mật)<br>- Tổng kết toàn bộ hành trình và tự đánh giá năng lực | 28/11/2025 | 28/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |

---

## 3. Chi tiết triển khai kỹ thuật (Dự án Capstone)

### 3.1 Phạm vi dự án: "Serverless E-Commerce Backend"
*   **Tổng quan kiến trúc:** Ứng dụng web 3 tầng (3-tier) sử dụng công nghệ serverless.
    *   **Frontend:** Lưu trữ trên **S3** + phân phối qua **CloudFront**.
    *   **Backend:** **API Gateway** + **Lambda**.
    *   **Cơ sở dữ liệu:** **DynamoDB** (Danh mục sản phẩm) + **RDS MySQL** (Lịch sử đơn hàng).
    *   **Xác thực:** **Amazon Cognito**.

### 3.2 Thiết lập cơ sở hạ tầng
*   **Thiết kế VPC:** Tạo VPC tùy chỉnh với 2 Public Subnets (NAT Gateway, Load Balancer) và 2 Private Subnets (Lambda, RDS).
*   **Security Groups:** Định nghĩa quy tắc nghiêm ngặt:
    *   RDS chỉ chấp nhận traffic từ Lambda SG trên cổng 3306.
    *   Lambda chỉ chấp nhận traffic từ các VPC endpoints nội bộ.

### 3.3 Logic ứng dụng & Dữ liệu
*   **Hàm Lambda:** Phát triển các hàm Python cho `CreateOrder`, `GetProducts`, và `ProcessPayment`.
*   **Tích hợp Database:**
    *   Sử dụng `Boto3` để quét (scan) DynamoDB lấy thông tin sản phẩm.
    *   Sử dụng `PyMySQL` để thực hiện giao dịch SQL ghi đơn hàng vào RDS.
*   **Giám sát:** Tạo CloudWatch Dashboard để trực quan hóa Độ trễ API và Tỷ lệ lỗi (4xx/5xx).

### 3.4 Tự động hóa & Vận hành
*   **CI/CD:** Xây dựng đường ống bằng **AWS CodePipeline**:
    *   Nguồn (Source): GitHub.
    *   Build: AWS CodeBuild (Chạy unit tests).
    *   Deploy: CloudFormation/SAM deploy.
*   **Tối ưu chi phí:** Thiết lập chính sách vòng đời S3 cho logs và cài đặt cảnh báo ngân sách (AWS Budget) cho dự án.

---

## 4. Thành tựu

Đến cuối Tuần 12 (và toàn bộ khóa học), các kết quả sau đã đạt được:

### ✔ Thành công dự án
*   Hoàn thành và bàn giao một **ứng dụng đám mây chuẩn production** kết hợp hơn 10 dịch vụ AWS.
*   Chứng minh khả năng tích hợp kho dữ liệu **Quan hệ (RDS)** và **Phi quan hệ (DynamoDB)** trong cùng một hệ thống.
*   Đạt được kiến trúc **Bảo mật** (Cognito/IAM), **Tin cậy** (Multi-AZ) và **Hiệu năng cao** (CloudFront/Caching).

### ✔ Phát triển chuyên môn
*   Làm chủ quy trình xây dựng ứng dụng đám mây từ **Phân tích yêu cầu** → **Thiết kế** → **Triển khai** → **Vận hành**.
*   Phát triển kỹ năng khắc phục sự cố (troubleshooting) mạnh mẽ cho các hệ thống phân tán phức tạp.
*   Hoàn thành lộ trình học tập và hoàn toàn sẵn sàng cho kỳ thi **AWS Certified Solutions Architect – Associate**.

---

## 5. Thách thức gặp phải & Giải pháp

**Thách thức 1: Kết nối Lambda trong VPC**
*   **Vấn đề:** Hàm Lambda trong Private Subnet mất kết nối internet (không thể gọi API công khai hoặc DynamoDB).
*   **Giải pháp:** Cấu hình **NAT Gateway** trong Public Subnet và cập nhật Route Tables. Đồng thời sử dụng **VPC Endpoint cho DynamoDB** để giữ lưu lượng nội bộ và giảm chi phí NAT.

**Thách thức 2: Lỗi Build trong CodePipeline**
*   **Vấn đề:** File `buildspec.yml` thất bại do thiếu thư viện Python phụ thuộc.
*   **Giải pháp:** Cập nhật pha `install` trong file buildspec để thực thi lệnh `pip install -r requirements.txt`.

**Thách thức 3: CORS với Cognito**
*   **Vấn đề:** API Gateway từ chối các yêu cầu có token hợp lệ do thiếu header CORS trên phản hồi lỗi 401.
*   **Giải pháp:** Cấu hình "Gateway Responses" trong API Gateway để bao gồm header CORS ngay cả đối với các lỗi Unauthorized.

---

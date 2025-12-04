---
title: "Worklog Tuần 11"
weight: 2
chapter: false
pre: " <b> 1.11. </b> "
---
# 📘 Báo cáo công việc Tuần 11 – AWS Journey  

## 1. Mục tiêu hàng tuần

**Tuần 11** tập trung vào **Hiện đại hóa Ứng dụng** thông qua **Kiến trúc Serverless (Không máy chủ)**. Mục tiêu chính là chuyển đổi từ việc quản lý cơ sở hạ tầng (EC2) sang tập trung vào mã nguồn và logic nghiệp vụ bằng cách sử dụng các dịch vụ hướng sự kiện. Các mục tiêu chính bao gồm:

*   **Mô hình Serverless** – Hiểu sự chuyển dịch từ kiến trúc Nguyên khối (Monolithic) sang Vi dịch vụ (Microservices) và lợi ích của "No-Ops".
*   **Bộ công cụ Serverless cốt lõi** – Làm chủ AWS Lambda (Tính toán), API Gateway (Giao diện) và DynamoDB (Dữ liệu NoSQL).
*   **Bảo mật & Xác thực** – Triển khai quản lý danh tính người dùng với Amazon Cognito.
*   **Cơ sở hạ tầng dưới dạng mã** – Sử dụng AWS Serverless Application Model (SAM) để định nghĩa và triển khai tài nguyên serverless.

Tuần này cung cấp bộ kỹ năng để xây dựng các ứng dụng có khả năng mở rộng cao, tiết kiệm chi phí và "thu nhỏ về 0" khi không sử dụng.

---

## 2. Tóm tắt công việc chi tiết

### 🗂 Bảng hoạt động

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| **Thứ Hai** | - Giới thiệu về khái niệm Hiện đại hóa và Serverless<br>- So sánh kiến trúc Nguyên khối và Vi dịch vụ<br>- Phân tích lợi ích: Chi phí, Khả năng mở rộng, Vận hành | 17/11/2025 | 17/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Ba** | - Thực hành AWS Lambda: tạo hàm, cấu hình triggers (S3/APIGW)<br>- Xem nhật ký log trong CloudWatch<br>- Triển khai logic xử lý API cơ bản | 18/11/2025 | 18/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Tư** | - Tích hợp API Gateway với Lambda (tạo REST API)<br>- Kết nối dữ liệu với DynamoDB (Thao tác CRUD)<br>- Test API sử dụng Postman | 19/11/2025 | 19/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Năm** | - Cấu hình Cognito để xác thực người dùng (User Pool)<br>- Tích hợp xác thực Cognito vào API Gateway<br>- Quản lý quyền truy cập qua IAM Role | 20/11/2025 | 20/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Sáu** | - Thực hành triển khai Serverless App hoàn chỉnh dùng AWS SAM<br>- Kiểm thử, ghi nhật ký và tối ưu hóa hiệu năng<br>- Tổng hợp kiến thức và báo cáo tuần | 21/11/2025 | 21/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |

---

## 3. Chi tiết triển khai kỹ thuật

### 3.1 AWS Lambda & Logic
*   **Runtime:** Tạo hàm Lambda sử dụng Python 3.9.
*   **Handler:** Triển khai hàm `lambda_handler(event, context)` để phân tích dữ liệu đầu vào JSON.
*   **Triggers:** Cấu hình API Gateway làm nguồn sự kiện kích hoạt hàm.
*   **Logging:** Sử dụng lệnh `print()` để gửi nhật ký có cấu trúc đến CloudWatch phục vụ gỡ lỗi.

### 3.2 Tích hợp API Gateway & DynamoDB
*   **Loại API:** Xây dựng REST API.
*   **Tích hợp:** Sử dụng **Lambda Proxy Integration** để chuyển toàn bộ đối tượng yêu cầu HTTP sang hàm xử lý.
*   **Cơ sở dữ liệu:**
    *   Tạo bảng DynamoDB (`Items`) với `ItemId` làm Khóa phân vùng (Partition Key).
    *   Sử dụng thư viện `boto3` trong Lambda để thực hiện các lệnh `put_item`, `get_item` và `scan` dựa trên phương thức HTTP (POST, GET).

### 3.3 Bảo mật với Amazon Cognito
*   **User Pool:** Tạo User Pool để xử lý đăng ký và đăng nhập.
*   **App Client:** Tạo client ID cho ứng dụng.
*   **Authorizer:** Cấu hình **Cognito User Pool Authorizer** trong API Gateway.
*   **Xác thực:** Xác minh rằng các yêu cầu API không có mã thông báo (token) `Authorization` (JWT) hợp lệ sẽ bị từ chối với lỗi `401 Unauthorized`.

### 3.4 AWS SAM (Mô hình Ứng dụng Serverless)
*   **Template:** Định nghĩa tài nguyên (Hàm, API, Bảng) trong tệp `template.yaml`.
*   **Build:** Chạy `sam build` để biên dịch các gói phụ thuộc.
*   **Deploy:** Thực hiện `sam deploy --guided` để đóng gói mã lên S3 và tự động tạo CloudFormation stack.
*   **Kiểm thử cục bộ:** Sử dụng `sam local invoke` để kiểm tra hàm trên máy cá nhân trước khi triển khai.

---

## 4. Thành tựu

Đến cuối Tuần 11, các kết quả sau đã đạt được:

### ✔ Thành công về mặt chức năng
*   Chuyển đổi thành công từ quản lý máy chủ sang triển khai các hàm (functions).
*   Xây dựng một **Serverless CRUD API** hoạt động hoàn chỉnh.
*   Bảo mật các endpoint API bằng **JWT Tokens** từ Cognito.
*   Tự động hóa triển khai bằng **AWS SAM**, thay thế các thao tác thủ công trên console.

### ✔ Phát triển kỹ năng
*   Hiểu thấu đáo mô hình **Kiến trúc Hướng sự kiện (Event-Driven Architecture)**.
*   Học cách xử lý các hạn chế của tính toán **Phi trạng thái (Stateless)**.
*   Làm chủ quy trình phân rã vấn đề thành các vi dịch vụ (Dịch vụ xác thực, Dịch vụ dữ liệu, Dịch vụ logic).

---

## 5. Thách thức gặp phải & Giải pháp

**Thách thức 1: Lỗi CORS**
*   **Vấn đề:** Gọi API từ trình duyệt web (frontend) dẫn đến lỗi Chia sẻ tài nguyên chéo nguồn (CORS).
*   **Giải pháp:** Bật CORS trong cài đặt API Gateway và đảm bảo hàm Lambda trả về header `Access-Control-Allow-Origin: *` trong đối tượng phản hồi.

**Thách thức 2: Quyền hạn Lambda**
*   **Vấn đề:** Lỗi `AccessDeniedException` khi Lambda cố gắng ghi dữ liệu vào DynamoDB.
*   **Giải pháp:** Cập nhật IAM Execution Role của Lambda để bao gồm quyền `dynamodb:PutItem` và `dynamodb:GetItem` cho ARN của bảng cụ thể.

**Thách thức 3: Khởi động lạnh (Cold Starts)**
*   **Vấn đề:** Cuộc gọi API đầu tiên sau một thời gian không hoạt động mất 2-3 giây để phản hồi.
*   **Giải pháp:** Chấp nhận đây là sự đánh đổi của Serverless. Tối ưu hóa các thư viện import trong mã Python để giảm thời gian khởi tạo.

---


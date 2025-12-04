---
title: "Worklog Tuần 3"
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---
# 📘 Báo cáo công việc Tuần 3 – Hành trình AWS

## 1. Mục tiêu hàng tuần

Trong **Tuần 3**, mục tiêu chính là tối ưu hóa hiệu suất ứng dụng và mở rộng kỹ năng quản lý dữ liệu ngoài cơ sở dữ liệu quan hệ. Các mục tiêu cụ thể bao gồm:

*   **Amazon CloudFront** – Hiểu về Mạng phân phối nội dung (CDN) và tối ưu hóa việc phân phối trang web tĩnh.
*   **Amazon DynamoDB** – Có kinh nghiệm thực tế với mô hình hóa và vận hành cơ sở dữ liệu NoSQL.
*   **Amazon ElastiCache (Redis)** – Triển khai bộ nhớ đệm (caching) để cải thiện tốc độ đọc dữ liệu.
*   **Tích hợp AWS CLI** – Tương tác nâng cao với các dịch vụ AWS bằng các tập lệnh dòng lệnh.

Tuần này tập trung vào việc chuyển đổi từ kiến trúc cơ bản sang mô hình hiệu suất cao, có khả năng mở rộng bằng cách sử dụng các lớp caching và dịch vụ NoSQL được quản lý.

---

## 2. Tóm tắt công việc chi tiết

### 🗂 Bảng hoạt động

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| **Thứ Hai** | - Giới thiệu khái niệm CDN và lợi ích của CloudFront<br>- Tạo CloudFront Distribution để phân phối nội dung web từ S3 | 22/09/2025 | 22/09/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Ba** | - Cấu hình hành vi (behaviors) và chính sách cache cho CloudFront<br>- Kiểm tra truy cập web qua URL CloudFront<br>- Thực hiện Invalidation (làm mới cache) để cập nhật nội dung mới | 23/09/2025 | 23/09/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Tư** | - Giới thiệu DynamoDB (Kiến trúc NoSQL)<br>- Tạo các bảng DynamoDB (Users, Products)<br>- Thực hành các thao tác CRUD trên Console | 24/09/2025 | 24/09/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Năm** | - Kết nối và truy vấn DynamoDB bằng AWS CLI<br>- Viết các script nhỏ để thêm (`put-item`) và đọc dữ liệu | 25/09/2025 | 25/09/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Sáu** | - Tìm hiểu về ElastiCache (Redis & Memcached)<br>- Khởi tạo cụm Redis cơ bản<br>- Kiểm tra kết nối từ EC2 để lưu/đọc dữ liệu cache | 26/09/2025 | 26/09/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |

---

## 3. Chi tiết triển khai kỹ thuật

### 3.1 Amazon CloudFront – Tích hợp CDN
*   Tạo distribution trỏ đến S3 bucket đã tạo trong Tuần 2.
*   Cấu hình **Origin Access Control (OAC)** để chỉ cho phép truy cập S3 thông qua CloudFront.
*   Bật **HTTPS** sử dụng chứng chỉ mặc định của CloudFront.
*   Kiểm tra sự cải thiện hiệu suất (giảm độ trễ) so với truy cập trực tiếp S3.
*   Thực hiện invalidation thủ công cho tệp `index.html`:
    ```bash
    aws cloudfront create-invalidation --distribution-id <ID> --paths "/*"
    ```

### 3.2 Amazon DynamoDB – Triển khai NoSQL
*   Tạo bảng `Users` với `UserId` làm Khóa phân vùng (Partition Key).
*   Thực hiện các thao tác **CRUD** (Tạo, Đọc, Cập nhật, Xóa) thông qua Giao diện quản lý (Console).
*   Tương tác qua AWS CLI để chèn dữ liệu:
    ```bash
    aws dynamodb put-item \
        --table-name Users \
        --item '{"UserId": {"S": "u-101"}, "Name": {"S": "Alice"}, "Role": {"S": "Admin"}}'
    ```
*   Xác thực dữ liệu đã chèn bằng lệnh `scan`.

### 3.3 Amazon ElastiCache – Thiết lập Redis
*   Khởi chạy cụm **ElastiCache for Redis** (cache.t2.micro hoặc t3.micro).
*   Cấu hình Security Groups để cho phép lưu lượng vào cổng `6379` từ EC2 instance.
*   Kết nối từ EC2 bằng `redis-cli` (cài đặt qua `amazon-linux-extras` hoặc `yum`).
*   Kiểm tra logic lưu bộ nhớ đệm:
    ```bash
    set mykey "Hello AWS"
    get mykey
    # Kết quả: "Hello AWS"
    ```

---

## 4. Thành tựu

Đến cuối Tuần 3, các kết quả sau đã đạt được:

### ✔ Thành công về mặt chức năng
*   Tăng tốc thành công trang web tĩnh S3 trên phạm vi toàn cầu bằng CloudFront.
*   Thể hiện kiến thức làm việc với cấu trúc dữ liệu NoSQL.
*   Thiết lập cụm Redis cache hoạt động tốt, có thể truy cập từ tài nguyên VPC riêng tư.
*   Tích hợp AWS CLI để quản lý cơ sở dữ liệu, vượt ra khỏi các thao tác chỉ dùng Console.

### ✔ Phát triển kỹ năng
*   Hiểu rõ vai trò của các vị trí biên (edge locations) và chiến lược caching.
*   Nắm vững sự khác biệt giữa mô hình Quan hệ (RDS) và NoSQL (DynamoDB).
*   Học cách thực hiện Cache Invalidation khi cập nhật nội dung tĩnh.
*   Có kinh nghiệm trong việc bảo mật các lớp cache nội bộ (ElastiCache) thông qua Security Groups.

---

## 5. Thách thức gặp phải & Giải pháp

**Thách thức 1: Nội dung CloudFront không cập nhật**
*   **Vấn đề:** Các cập nhật cho `index.html` trên S3 không phản ánh ngay lập tức trên trang web.
*   **Giải pháp:** Tìm hiểu về TTL (Time To Live) và thực hiện **CloudFront Invalidation** để buộc làm mới dữ liệu.

**Thách thức 2: Cú pháp phức tạp của DynamoDB CLI**
*   **Vấn đề:** Gặp khó khăn khi định dạng JSON chính xác cho các lệnh CLI.
*   **Giải pháp:** Sử dụng công cụ tạo JSON và tham khảo tài liệu AWS CLI để biết cú pháp `AttributeValue` chính xác (S, N, v.v.).

**Thách thức 3: Kết nối Redis từ máy cá nhân**
*   **Vấn đề:** Cố gắng kết nối với ElastiCache từ bên ngoài VPC (thất bại).
*   **Giải pháp:** Hiểu rằng ElastiCache chỉ dành cho mạng nội bộ VPC; sử dụng EC2 bastion host đã thiết lập ở Tuần 2 làm máy trung gian (jump box).

---

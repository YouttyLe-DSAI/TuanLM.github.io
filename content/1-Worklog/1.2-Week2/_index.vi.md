---
title: "Worklog Tuần 2"
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---
# 📘 Báo cáo công việc Tuần 2 – Hành trình AWS

## 1. Mục tiêu hàng tuần

Trong **Tuần 2**, mục tiêu chính là đạt được kinh nghiệm thực tế nền tảng với các dịch vụ cơ sở hạ tầng cốt lõi của AWS, bao gồm:

*   **Amazon S3** – Lưu trữ trang web tĩnh và quản lý quyền truy cập bucket.
*   **Amazon RDS (MySQL)** – Cấp phát cơ sở dữ liệu quan hệ được quản lý và cấu hình kết nối.
*   **Amazon EC2** – Sử dụng EC2 instance như một máy chủ trung gian (bastion host) bảo mật để truy cập RDS.
*   **Amazon Route53** – Quản lý tên miền và ánh xạ bản ghi DNS tới các dịch vụ AWS.

Tuần này tập trung vào việc xây dựng các thành phần kiến trúc đám mây cơ bản, đóng vai trò là tiền đề cho các nhiệm vụ của Tuần 3 liên quan đến CloudFront, DynamoDB và ElastiCache.

---

## 2. Tóm tắt công việc chi tiết

### 🗂 Bảng hoạt động

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| **Thứ Hai** | - Tạo S3 bucket cho nội dung web tĩnh<br>- Tải lên các tệp demo HTML/CSS ban đầu | 15/09/2025 | 15/09/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Ba** | - Bật tính năng Static Website Hosting trên S3<br>- Cấu hình Bucket Policy cho phép quyền đọc công khai (public read)<br>- Kiểm tra truy cập website qua endpoint S3 | 16/09/2025 | 16/09/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Tư** | - Tạo RDS MySQL instance (Gói Free Tier)<br>- Cấu hình VPC Security Groups cho lưu lượng truy cập vào<br>- Ghi lại endpoint DB & thông tin đăng nhập | 17/09/2025 | 17/09/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Năm** | - Khởi chạy EC2 instance và cài đặt MySQL client<br>- Kết nối từ EC2 → RDS bằng dòng lệnh<br>- Thực thi các truy vấn thử nghiệm và tạo bảng mẫu | 18/09/2025 | 18/09/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Sáu** | - Tìm hiểu chức năng Route53<br>- Tạo Hosted Zone và các bản ghi DNS (A/CNAME)<br>- Cấu hình định tuyến từ tên miền tùy chỉnh → trang web tĩnh S3<br>- Xác thực truy cập website bằng tên miền | 19/09/2025 | 19/09/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |

---

## 3. Chi tiết triển khai kỹ thuật

### 3.1 AWS S3 – Thiết lập Website tĩnh
*   Tạo S3 bucket mới tuân theo quy ước đặt tên và vị trí vùng (region).
*   Tải lên tài nguyên tĩnh (HTML/CSS/Hình ảnh).
*   Bật tính năng **Static Website Hosting**.
*   Cấu hình `index.html` và `error.html`.
*   Thêm **Bucket Policy** (quyền public-read) để phục vụ nội dung toàn cầu.
*   Xác minh khả năng truy cập qua endpoint của website:
    ```
    http://<bucket-name>.s3-website-<region>.amazonaws.com
    ```

### 3.2 Amazon RDS – Cấp phát Cơ sở dữ liệu
*   Khởi chạy instance **RDS MySQL 8.0** thuộc gói Free Tier.
*   Áp dụng các quy tắc **Security Group** bảo mật (EC2 → RDS, cổng 3306).
*   Lưu trữ endpoint được tạo để kết nối sau này.
*   Đảm bảo DB subnet group và cấu hình VPC hợp lệ cho truy cập riêng tư.

### 3.3 Amazon EC2 – Kết nối DB bảo mật
*   Tạo một instance EC2 `t2.micro` trong cùng VPC với RDS instance.
*   Cài đặt MySQL Client:
    ```bash
    sudo yum install mysql -y
    ```
*   Kết nối thành công đến RDS:
    ```bash
    mysql -h <rds-endpoint> -u admin -p
    ```
*   Tạo cơ sở dữ liệu mẫu và bảng để kiểm tra.

### 3.4 Amazon Route53 – Cấu hình DNS
*   Thiết lập một **Hosted Zone** mới.
*   Thêm các bản ghi DNS:
    *   **A Record** → Trang web tĩnh S3.
    *   **CNAME Record** cho các bí danh thử nghiệm.
*   Chờ DNS lan truyền (thường từ 1–5 phút).
*   Truy cập thành công trang web tĩnh bằng tên miền tùy chỉnh.

---

## 4. Thành tựu

Đến cuối Tuần 2, các kết quả sau đã đạt được:

### ✔ Thành công về mặt chức năng
*   Hoàn thành một trang web tĩnh được lưu trữ trên S3 hoạt động hoàn chỉnh.
*   Cho phép truy cập qua cả endpoint S3 và tên miền Route53.
*   Triển khai và kết nối thành công cơ sở dữ liệu RDS MySQL.
*   Xác minh giao tiếp bảo mật giữa **EC2 ↔ RDS**.

### ✔ Phát triển kỹ năng
*   Thể hiện sự hiểu biết về:
    *   IAM roles & quyền hạn.
    *   Kiểm soát truy cập S3.
    *   Mạng VPC & Security Groups.
    *   Các khái niệm định tuyến DNS.
*   Có được kinh nghiệm nền tảng với các dịch vụ cốt lõi của AWS.
*   Củng cố hiểu biết về luồng ứng dụng đám mây đầu cuối (end-to-end).
*   Xây dựng sự tự tin khi làm việc với các thao tác dòng lệnh (CLI).
*   Cải thiện kỹ năng khắc phục sự cố (lan truyền DNS, cấu hình SG và chính sách truy cập công khai).

---

## 5. Thách thức gặp phải & Giải pháp

**Thách thức 1: S3 Public Access Block (Chặn truy cập công khai)**
*   **Vấn đề:** Website không thể truy cập do cài đặt chặn truy cập công khai mặc định của S3.
*   **Giải pháp:** Tắt cài đặt “Block Public Access” và thêm bucket policy chính xác.

**Thách thức 2: Lỗi kết nối EC2 -> RDS (Timeout)**
*   **Vấn đề:** Security Group không cho phép lưu lượng MySQL đi vào.
*   **Giải pháp:** Sửa đổi Security Group của RDS để chấp nhận lưu lượng cụ thể từ Security Group của EC2 trên cổng 3306.

**Thách thức 3: DNS không phân giải ngay lập tức**
*   **Vấn đề:** Tên miền mất thời gian để cập nhật trong Route53.
*   **Giải pháp:** Chờ hết thời gian TTL và kiểm tra lại bằng lệnh `dig` / `nslookup`.


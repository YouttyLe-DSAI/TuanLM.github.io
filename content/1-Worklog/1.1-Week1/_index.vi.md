---
title: "Worklog Tuần 1"
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---
# 📘 Báo cáo công việc Tuần 1 – AWS Journey

## 1. Mục tiêu hàng tuần

Mục tiêu chính của **Tuần 1** là thiết lập môi trường nền tảng cho hành trình AWS và hiểu các nguyên tắc vận hành cốt lõi. Các mục tiêu cụ thể bao gồm:

*   **Onboarding (Nhập môn):** Làm quen với quy trình thực tập FCJ, các kênh liên lạc và nội quy.
*   **Thiết lập tài khoản:** Hoàn tất đăng ký **AWS Free Tier**, cấu hình **AWS CLI**, và kích hoạt các chuẩn bảo mật cơ bản (MFA, IAM).
*   **Dịch vụ cốt lõi:** Có cái nhìn tổng quan về hệ sinh thái AWS (Tính toán, Lưu trữ, Mạng, Cơ sở dữ liệu, Bảo mật).
*   **Thực hành:** Sử dụng thành thạo **AWS Management Console** & **AWS CLI v2**.
*   **Cơ sở hạ tầng:** Triển khai và vận hành một instance **EC2 t2.micro** và thực hiện các thao tác **EBS** cơ bản.
*   **Kiểm soát chi phí:** Thiết lập **AWS Budgets** để giám sát chi tiêu.

---

## 2. Tóm tắt công việc chi tiết

### 🗂 Kế hoạch thực hiện so với Thực tế

| Hạng mục | Kế hoạch | Thực tế | Trạng thái |
| :--- | :--- | :--- | :--- |
| **Onboarding & Nội quy** | Giới thiệu, nắm bắt kênh liên lạc | Đã được giới thiệu, ghi chú chuẩn báo cáo | ✅ Hoàn thành |
| **Tổng quan AWS** | Hệ thống hóa nhóm dịch vụ + Mindmap | Hoàn tất, đã ghi chú theo phân loại | ✅ Hoàn thành |
| **Free Tier & Bảo mật** | Tạo tài khoản, bật MFA, tạo IAM user | Đã bật MFA; tạo user + nhóm Viewer | ✅ Hoàn thành |
| **AWS CLI** | Cài đặt CLI, cấu hình profile | Đã set profile `acj-student`, test `sts` OK | ✅ Hoàn thành |
| **EC2/EBS/SSH** | Tạo EC2, SSH, gắn EBS | EC2 t2.micro + EBS 8GB gp3, SSH thành công | ✅ Hoàn thành |
| **Quản lý chi phí** | Đặt ngân sách $5/tháng | Đã nhận email cảnh báo thử nghiệm | ✅ Hoàn thành |

### 📅 Nhật ký hoạt động theo ngày

| Thứ | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| **Thứ Hai** | **Onboarding:** Định hướng FCJ, đọc nội quy, học chuẩn báo cáo | 08/09 | 08/09 | [AWS Journey](https://cloudjourney.awsstudygroup.com) |
| **Thứ Ba** | **Nghiên cứu:** Khám phá hệ sinh thái AWS (Compute/Storage/Networking/DB/Security), tạo mindmap | 09/09 | 09/09 | [AWS Journey](https://cloudjourney.awsstudygroup.com) |
| **Thứ Tư** | **Thiết lập tài khoản:** Tạo **AWS Free Tier**, bật **MFA** cho root, tạo **IAM user** + nhóm Viewer | 10/09 | 10/09 | [AWS Journey](https://cloudjourney.awsstudygroup.com) |
| **Thứ Năm** | **Cài đặt CLI:** Cài **AWS CLI v2** (Windows), chạy `aws configure` (profile `acj-student`), kiểm tra danh tính `sts` | 11/09 | 11/09 | [AWS Journey](https://cloudjourney.awsstudygroup.com) |
| **Thứ Sáu** | **Lý thuyết:** Học về **EC2** (loại instance, AMI, EBS, SG, Elastic IP) + checklist Free Tier | 12/09 | 12/09 | [AWS Journey](https://cloudjourney.awsstudygroup.com) |
| **Thứ Bảy** | **Thực hành:** Tạo **EC2 t2.micro (AL2023)**, tạo/dùng **key pair (.pem)**, **SSH**; **gắn EBS 8GB**, định dạng & mount | 13/09 | 13/09 | [AWS Journey](https://cloudjourney.awsstudygroup.com) |

---

## 3. Kết quả & Minh chứng

### 3.1 Tài nguyên đã tạo
*   **IAM**: 01 User làm việc hàng ngày (Nhóm: Viewer), đã bật **MFA** cho tài khoản root.
*   **EC2**: `t2.micro` (Free Tier), AMI: Amazon Linux 2023.
*   **Security Group**: Quy tắc Inbound mở cổng `22/tcp` chỉ giới hạn cho **My IP**.
*   **EBS**: Volume 8GB `gp3`, đã định dạng (`xfs`) và mount vào thư mục `/data`.
*   **Budgets**: Ngân sách hàng tháng đặt mức **$5 USD** với cảnh báo qua email.
*   **CLI Region**: Mặc định là `ap-southeast-1` (Singapore).

### 3.2 Các lệnh CLI đã thực thi
```bash
aws sts get-caller-identity --profile acj-student
aws ec2 describe-regions --profile acj-student --output table
aws ec2 describe-instances --profile acj-student --region ap-southeast-1
aws ec2 create-key-pair --key-name fcj-key --query "KeyMaterial" --output text > fcj-key.pem


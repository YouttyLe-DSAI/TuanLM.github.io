---
title: "Worklog Tuần 7"
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---
# 📘 Báo cáo công việc Tuần 7 – AWS Journey 
## 1. Mục tiêu hàng tuần

Trong **Tuần 7**, trọng tâm là xây dựng **Tính sẵn sàng cao (High Availability - HA)** và **Khả năng mở rộng (Scalability)** cho kiến trúc. Các mục tiêu chính bao gồm:

*   **Tự động mở rộng & Cân bằng tải** – Cấu hình hệ thống để xử lý tải lưu lượng thay đổi tự động bằng ASG và ALB.
*   **Kiến trúc Decoupling (Tách rời)** – Sử dụng SQS và SNS để cho phép giao tiếp không đồng bộ giữa các vi dịch vụ.
*   **Giám sát mạng** – Tăng cường khả năng quan sát bằng cách ghi lại và phân tích lưu lượng mạng với VPC Flow Logs.

Tuần này biến đổi cơ sở hạ tầng tĩnh thành một hệ thống động, bền vững, có khả năng tự phục hồi và mở rộng theo nhu cầu.

---

## 2. Tóm tắt công việc chi tiết

### 🗂 Bảng hoạt động

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| **Thứ Hai** | - Tìm hiểu về các khái niệm High Availability, Fault Tolerance và Elasticity<br>- Giới thiệu về Auto Scaling Group (ASG) và Elastic Load Balancer (ELB) | 20/10/2025 | 20/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Ba** | - Thực hành tạo Auto Scaling Group cho EC2 instance<br>- Thiết lập launch template, scaling policy và theo dõi mục tiêu (target tracking) | 21/10/2025 | 21/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Tư** | - Tạo và cấu hình Application Load Balancer (ALB)<br>- Kết nối ALB với ASG để phân phối tải<br>- Kiểm tra truy cập website qua ALB DNS | 22/10/2025 | 22/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Năm** | - Làm quen với dịch vụ Amazon SQS và SNS<br>- Tạo SQS queue, SNS topic và subscription<br>- Gửi và nhận thông báo giữa các thành phần | 23/10/2025 | 23/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Sáu** | - Bật VPC Flow Logs để giám sát lưu lượng mạng<br>- Phân tích nhật ký trong CloudWatch Logs<br>- Tổng hợp kiến thức về độ tin cậy & mở rộng | 24/10/2025 | 24/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |

---

## 3. Chi tiết triển khai kỹ thuật

### 3.1 Auto Scaling Group (ASG)
*   **Launch Template:** Tạo mẫu định nghĩa AMI, Loại instance (t2.micro) và Security Groups.
*   **Chính sách mở rộng (Scaling Policies):** Triển khai **Target Tracking Scaling Policy** để duy trì mức sử dụng CPU trung bình ở 50%.
*   **Dung lượng:** Cấu hình Min: 2, Max: 4, Desired: 2 để đảm bảo tính sẵn sàng cao trên nhiều Availability Zones.

### 3.2 Application Load Balancer (ALB)
*   **Target Group:** Tạo nhóm đích cho lưu lượng HTTP (Cổng 80).
*   **Quy tắc Listener:** Cấu hình ALB để lắng nghe HTTP và chuyển tiếp lưu lượng đến Target Group của ASG.
*   **Kiểm tra sức khỏe (Health Checks):** Cấu hình đường dẫn `/index.html` để đảm bảo chỉ các instance khỏe mạnh mới nhận được lưu lượng.
*   **DNS:** Xác thực quyền truy cập bằng tên DNS tự tạo của ALB (`my-loadbalancer-123.region.elb.amazonaws.com`).

### 3.3 Tách rời với SQS & SNS
*   **SNS (Simple Notification Service):** Tạo Topic (`OrderAlerts`) và đăng ký địa chỉ email để nhận thông báo.
*   **SQS (Simple Queue Service):** Tạo Hàng đợi tiêu chuẩn (`OrderQueue`).
*   **Mô hình Fan-out:** Đăng ký SQS queue vào SNS topic. Xuất bản một tin nhắn lên SNS và xác minh nó xuất hiện trong cả hộp thư Email và hàng đợi SQS.

### 3.4 VPC Flow Logs & Giám sát
*   **Thiết lập:** Bật Flow Logs cho VPC, gửi dữ liệu đến **CloudWatch Logs**.
*   **Phân tích:** Sử dụng CloudWatch Log Insights để truy vấn lưu lượng:
    *   Xác định lưu lượng bị từ chối (REJECT) do chặn Security Group.
    *   Theo dõi các nỗ lực kết nối SSH.
    *   Phân tích luồng lưu lượng nội bộ giữa các subnets.

---

## 4. Thành tựu

Đến cuối Tuần 7, các kết quả sau đã đạt được:

### ✔ Thành công về mặt chức năng
*   Hiểu rõ mô hình Tính sẵn sàng cao và cách duy trì thời gian hoạt động của hệ thống khi gặp sự cố.
*   Triển khai thành công **Auto Scaling Group + Load Balancer** để tự động mở rộng dung lượng EC2.
*   Cấu hình **SQS/SNS** để giao tiếp hàng đợi và thông báo tin cậy.
*   Bật và đọc hiểu **VPC Flow Logs**, phân tích lưu lượng mạng trong CloudWatch.

### ✔ Phát triển kỹ năng
*   Nắm vững mối quan hệ giữa Load Balancers và Auto Scaling Groups.
*   Học cách giả lập tải (sử dụng công cụ `stress`) để kích hoạt sự kiện mở rộng (scaling events).
*   Có kinh nghiệm trong thiết kế kiến trúc "Loose Coupling" (Kết nối lỏng lẻo).
*   Cải thiện kỹ năng khắc phục sự cố mạng thông qua phân tích nhật ký (log).

---

## 5. Thách thức gặp phải & Giải pháp

**Thách thức 1: Unhealthy Targets trong ALB**
*   **Vấn đề:** Các instance EC2 trong Target Group hiển thị trạng thái "Unhealthy".
*   **Giải pháp:** Security Group trên EC2 không cho phép lưu lượng từ Security Group của Load Balancer. Đã cập nhật quy tắc Inbound để cho phép HTTP từ SG của ALB.

**Thách thức 2: ASG không thu hẹp (Scale Down)**
*   **Vấn đề:** Sau khi test tải, các instances vẫn chạy lâu hơn dự kiến.
*   **Giải pháp:** Hiểu về khái niệm **Cooldown Period** (Thời gian hạ nhiệt). ASG đang chờ hết thời gian cooldown mặc định (300 giây) trước khi chấm dứt instances để tránh hiện tượng "dao động" (thrashing).

**Thách thức 3: Khả năng hiển thị tin nhắn SQS**
*   **Vấn đề:** Tin nhắn đã được xử lý nhưng lại xuất hiện lại trong hàng đợi.
*   **Giải pháp:** Điều chỉnh **Visibility Timeout** để khớp với thời gian xử lý của ứng dụng tiêu thụ (consumer).

---

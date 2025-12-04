---
title: "Worklog Tuần 8"
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---
# 📘 Báo cáo công việc Tuần 8 – AWS Journey 

## 1. Mục tiêu hàng tuần

**Tuần 8** đóng vai trò là giai đoạn tổng kết và củng cố toàn diện. Mục tiêu chính là hệ thống hóa tất cả kiến thức đã học trong 7 tuần qua dưới góc nhìn của **AWS Well-Architected Framework** (Khung kiến trúc tốt). Các mục tiêu chính bao gồm:

*   **Well-Architected Framework**: Hiểu sâu về 5 trụ cột (Vận hành xuất sắc, Bảo mật, Tin cậy, Hiệu quả hiệu suất, Tối ưu hóa chi phí).
*   **Củng cố kiến trúc**: Ôn tập các phương pháp hay nhất về Bảo mật (IAM, KMS), Khả năng phục hồi (Multi-AZ, DR) và Tối ưu hóa.
*   **Thiết kế tổng thể**: Thiết kế một cơ sở hạ tầng hoàn chỉnh tích hợp các dịch vụ cốt lõi (EC2, S3, RDS, VPC, Lambda, CloudFront) và đánh giá theo tiêu chuẩn AWS.

Tuần này chuyển tiếp từ việc học các dịch vụ riêng lẻ sang thiết kế các hệ thống mạnh mẽ, sẵn sàng cho môi trường thực tế (production).

---

## 2. Tóm tắt công việc chi tiết

### 🗂 Bảng hoạt động

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| **Thứ Hai** | - Tổng quan về AWS Well-Architected Framework & 5 trụ cột<br>- Xác định vai trò và tầm quan trọng của từng trụ cột trong thiết kế hệ thống | 27/10/2025 | 27/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Ba** | - Ôn tập Thiết kế Kiến trúc Bảo mật<br>- Chuyên sâu: IAM, MFA, SCP, KMS, WAF, Shield, GuardDuty, Security Groups so với NACLs | 28/10/2025 | 28/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Tư** | - Ôn tập Thiết kế Kiến trúc Bền vững (Resilient)<br>- Chủ đề: Multi-AZ, Multi-Region, Chiến lược DR, Route 53, Sao lưu & Khôi phục | 29/10/2025 | 29/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Năm** | - Ôn tập Tối ưu hóa Hiệu suất và Chi phí<br>- Chủ đề: Auto Scaling, Global Accelerator, Phân cấp S3, Savings Plans | 30/10/2025 | 30/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Sáu** | - Thực hành tổng hợp: Xây dựng kiến trúc mẫu full-stack<br>- Đánh giá theo 5 tiêu chí của Well-Architected Framework<br>- Viết báo cáo tổng kết tuần | 31/10/2025 | 31/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |

---

## 3. Chi tiết triển khai kỹ thuật

### 3.1 Đánh giá Kiến trúc Bảo mật (Trụ cột Security)
*   **Phòng thủ theo chiều sâu (Defense in Depth):** Thiết kế mô hình bảo mật đa lớp:
    *   **Biên (Edge):** AWS WAF & Shield (chống DDoS).
    *   **VPC:** Subnet Public/Private, NACLs (Stateless), Security Groups (Stateful).
    *   **Danh tính:** IAM Users với MFA, Roles cho dịch vụ, Nguyên tắc đặc quyền tối thiểu.
    *   **Dữ liệu:** KMS để mã hóa khi nghỉ (EBS/S3/RDS), TLS/ACM để mã hóa đường truyền.

### 3.2 Độ tin cậy & Khả năng phục hồi (Trụ cột Reliability)
*   **Tính sẵn sàng cao (HA):** Thiết kế triển khai Multi-AZ cho EC2 (qua ASG) và RDS (Primary/Standby).
*   **Khôi phục thảm họa (DR):** Rà soát 4 chiến lược DR:
    *   Backup & Restore (Rẻ nhất, RTO cao nhất).
    *   Pilot Light.
    *   Warm Standby.
    *   Multi-Site Active/Active (Đắt nhất, RTO thấp nhất).

### 3.3 Hiệu suất & Chi phí (Trụ cột Efficiency & Optimization)
*   **Hiệu suất:** Triển khai CloudFront để lưu đệm tại biên (edge caching) và Global Accelerator để tối ưu hóa định tuyến giảm độ trễ.
*   **Chi phí:**
    *   Phân tích **S3 Lifecycle Policies** (Standard -> IA -> Glacier) để tự động tiết kiệm lưu trữ.
    *   Đánh giá **Compute Savings Plans** so với **Reserved Instances** cho khối lượng công việc dài hạn.
    *   Sử dụng **AWS Cost Explorer** để xác định tài nguyên "zombie" (EIP không gắn kết, ELB nhàn rỗi).

### 3.4 Thực hành Kiến trúc Capstone
*   Thiết kế Ứng dụng Web 3 tầng (3-Tier Web App):
    1.  **Tầng trình bày:** CloudFront + S3 (tài sản tĩnh) / ALB (yêu cầu động).
    2.  **Tầng logic:** EC2 Auto Scaling Group trong Private Subnets.
    3.  **Tầng dữ liệu:** RDS Multi-AZ + DynamoDB.
*   Thực hiện tự đánh giá bằng công cụ **AWS Well-Architected Tool** để xác định các rủi ro (High/Medium Risk Issues).

---

## 4. Thành tựu

Đến cuối Tuần 8, các kết quả sau đã đạt được:

### ✔ Làm chủ khái niệm
*   Hiểu sâu và hệ thống hóa kiến thức về **AWS Well-Architected Framework**.
*   Có khả năng phân tích sự đánh đổi (trade-offs) giữa Chi phí, Hiệu suất và Độ tin cậy.

### ✔ Củng cố kỹ thuật
*   Củng cố 4 nhóm kiến trúc cốt lõi: Bảo mật, Bền vững, Hiệu suất và Tối ưu hóa chi phí.
*   Nắm vững sự tương tác giữa các dịch vụ cốt lõi (ví dụ: cách CloudWatch kích hoạt Lambda để khắc phục sự cố).

### ✔ Ứng dụng thực tế
*   Thực hành thiết kế một cơ sở hạ tầng hoàn chỉnh theo tiêu chuẩn công nghiệp từ con số 0.
*   Học cách thực hiện tự đánh giá và rà soát kiến trúc.

---

## 5. Thách thức gặp phải & Giải pháp

**Thách thức 1: Phân tích sự đánh đổi (Trade-off)**
*   **Vấn đề:** Khó khăn khi chọn giữa "Hiệu suất tối đa" và "Chi phí thấp nhất" (ví dụ: DynamoDB Provisioned vs. On-Demand).
*   **Giải pháp:** Sử dụng Well-Architected Framework để ưu tiên yêu cầu nghiệp vụ (ví dụ: nếu lưu lượng không thể dự đoán, On-Demand tốt hơn dù chi phí đơn vị có thể cao hơn).

**Thách thức 2: Sự phức tạp của chiến lược DR**
*   **Vấn đề:** Nhầm lẫn sự khác biệt nhỏ giữa "Pilot Light" và "Warm Standby".
*   **Giải pháp:** Tạo bảng so sánh tập trung vào mục tiêu RTO/RPO và số lượng tài nguyên hoạt động để phân biệt rõ ràng.

**Thách thức 3: Xung đột Security Group vs. NACL**
*   **Vấn đề:** Khắc phục sự cố kết nối khi NACL chặn lưu lượng trả về (cổng ephemeral).
*   **Giải pháp:** Củng cố hiểu biết rằng NACL là phi trạng thái (stateless) và yêu cầu quy tắc cho phép rõ ràng cho cả chiều vào (inbound) và chiều ra (outbound).

---

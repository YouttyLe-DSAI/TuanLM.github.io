---
title: "Worklog Tuần 4"
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---
# 📘 Báo cáo công việc Tuần 4 – Hành trình AWS

## 1. Mục tiêu hàng tuần

Trong **Tuần 4**, trọng tâm chính chuyển sang các **Chiến lược di chuyển (Migration)** và **Đảm bảo tính liên tục trong kinh doanh (Business Continuity)**. Mục tiêu là hiểu cách chuyển khối lượng công việc từ on-premise (tại chỗ) lên đám mây và đảm bảo hệ thống có khả năng phục hồi trước các sự cố. Các mục tiêu chính bao gồm:

*   **Quy trình Migration** – Hiểu về "6 Rs" trong di chuyển (Rehost, Replatform, Refactor, v.v.).
*   **AWS Database Migration Service (DMS)** – Di chuyển dữ liệu từ cơ sở dữ liệu nguồn sang Amazon RDS với thời gian ngừng hoạt động tối thiểu.
*   **Elastic Disaster Recovery (EDR)** – Triển khai sao chép và chiến lược phục hồi để giảm thiểu mất mát dữ liệu.
*   **Lập kế hoạch Khôi phục thảm họa (DR)** – Xác định RTO (Thời gian khôi phục mục tiêu) và RPO (Điểm khôi phục mục tiêu).

Tuần này thiết lập các kỹ năng quan trọng cần thiết cho độ tin cậy và hiện đại hóa cơ sở hạ tầng cấp doanh nghiệp.

---

## 2. Tóm tắt công việc chi tiết

### 🗂 Bảng hoạt động

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| **Thứ Hai** | - Tìm hiểu các khái niệm Migration (Lift & Shift, Replatform, Refactor)<br>- Giới thiệu về AWS Database Migration Service (DMS) | 29/09/2025 | 29/09/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Ba** | - Thực hành tạo Replication Instance trong DMS<br>- Cấu hình nguồn dữ liệu (giả lập on-premise) và đích (RDS)<br>- Thực hiện di chuyển dữ liệu thử nghiệm | 30/09/2025 | 30/09/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Tư** | - Giới thiệu về Elastic Disaster Recovery (EDR)<br>- Tìm hiểu cách thiết lập máy chủ sao chép và instance khôi phục | 01/10/2025 | 01/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Năm** | - Thực hành mô phỏng sự cố: tắt EC2 chính và khởi chạy instance khôi phục từ EDR<br>- Đánh giá thời gian khôi phục (RTO/RPO) | 02/10/2025 | 02/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Sáu** | - Tạo kế hoạch DR cơ bản (sao lưu, khôi phục, chuyển đổi dự phòng)<br>- Viết tài liệu tổng hợp quy trình Migration + DR | 03/10/2025 | 03/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |

---

## 3. Chi tiết triển khai kỹ thuật

### 3.1 AWS Database Migration Service (DMS)
*   **Replication Instance:** Cấp phát một instance `dms.t2.micro` trong VPC để xử lý tác vụ di chuyển.
*   **Cấu hình Endpoints:**
    *   **Source (Nguồn):** Cấu hình cơ sở dữ liệu MySQL trên EC2 (mô phỏng máy chủ tại chỗ) với quyền truy cập phù hợp.
    *   **Target (Đích):** Kết nối với RDS MySQL instance đã tạo ở Tuần 2.
*   **Tác vụ Migration:** Tạo tác vụ "Full Load" (Tải toàn bộ) để di chuyển các bảng hiện có.
*   **Quy tắc ánh xạ:** Cấu hình quy tắc chọn lược đồ (schema) để bao gồm các bảng cụ thể (ví dụ: `Users`, `Products`).

### 3.2 Thiết lập Elastic Disaster Recovery (EDR)
*   Khởi tạo dịch vụ EDR trong Region AWS cụ thể.
*   **Cài đặt Agent:** Tải xuống và cài đặt AWS Replication Agent trên EC2 instance nguồn (`Linux`).
*   **Staging Area:** Xác minh rằng máy chủ sao chép đã tự động khởi chạy trong subnet staging.
*   **Sao chép dữ liệu:** Theo dõi tiến trình đồng bộ hóa ban đầu cho đến khi trạng thái đạt "Healthy" và "Data replicated".

### 3.3 Mô phỏng chuyển đổi dự phòng (Failover Drill)
*   **Kịch bản:** Mô phỏng sự cố nghiêm trọng bằng cách dừng (Stop) instance EC2 nguồn.
*   **Hành động khôi phục:** Khởi tạo "Recovery Drill" trong giao diện điều khiển EDR.
*   **Cài đặt khởi chạy:** Cấu hình Launch Template (loại instance, security groups) cho instance khôi phục.
*   **Xác thực:** SSH thành công vào Recovery Instance đã khởi chạy và xác minh tính toàn vẹn của dữ liệu ứng dụng.

### 3.4 Lập kế hoạch & Tài liệu DR
*   Soạn thảo kế hoạch DR cơ bản phác thảo:
    *   **Chiến lược sao lưu:** Snapshots tự động so với Sao chép liên tục.
    *   **Các bước Failover:** Trình tự các hành động để chuyển sang trang web khôi phục.
    *   **Phân tích RTO/RPO:** Đo lường thời gian khôi phục (RTO) và lượng dữ liệu có thể bị trễ (RPO).

---

## 4. Thành tựu

Đến cuối Tuần 4, các kết quả sau đã đạt được:

### ✔ Thành công về mặt chức năng
*   Di chuyển dữ liệu thành công giữa hai điểm cuối cơ sở dữ liệu bằng AWS DMS.
*   Cấu hình sao chép liên tục ở cấp độ khối (block-level) bằng Elastic Disaster Recovery.
*   Thực hiện thành công cuộc diễn tập failover, đưa máy chủ khôi phục hoạt động trong vòng vài phút.
*   Xác minh tính nhất quán dữ liệu giữa hệ thống Nguồn và Đích.

### ✔ Phát triển kỹ năng
*   Hiểu rõ trọn vẹn **Vòng đời di chuyển (Migration lifecycle)** (Đánh giá → Huy động → Di chuyển & Hiện đại hóa).
*   Có kinh nghiệm thực tế với các khái niệm mạng **Hybrid Cloud** (Nguồn → AWS).
*   Hiểu sâu hơn về **Lập kế hoạch kinh doanh liên tục (BCP)**.
*   Học cách phân biệt giữa các chiến lược Sao lưu (Backup) và giải pháp Khôi phục thảm họa (Disaster Recovery).

---

## 5. Thách thức gặp phải & Giải pháp

**Thách thức 1: Lỗi kết nối DMS**
*   **Vấn đề:** Replication Instance không thể kết nối với cơ sở dữ liệu EC2 nguồn.
*   **Giải pháp:** Cập nhật Security Group của nguồn để cho phép lưu lượng vào cổng 3306 cụ thể từ Private IP của DMS Replication Instance.

**Thách thức 2: Lỗi cài đặt EDR Agent**
*   **Vấn đề:** Agent sao chép không cài đặt được do thiếu quyền IAM.
*   **Giải pháp:** Tạo một IAM user với các access keys lập trình cụ thể cần thiết cho AWS Replication Agent và chạy lại trình cài đặt.

**Thách thức 3: RTO cao trong quá trình diễn tập**
*   **Vấn đề:** Instance khôi phục mất nhiều thời gian hơn dự kiến để sẵn sàng.
*   **Giải pháp:** Tối ưu hóa Launch Template để sử dụng AMI phù hợp hoặc loại instance tốt hơn để tăng tốc quá trình khởi động.

---

---
title: "Worklog Tuần 6"
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---
# 📘 Báo cáo công việc Tuần 6 – Hành trình AWS

## 1. Mục tiêu hàng tuần

Trong **Tuần 6**, trọng tâm chuyển sang các trụ cột quan trọng của khung kiến trúc Well-Architected: **Bảo mật (Security)** và **Tối ưu hóa chi phí (Cost Optimization)**. Các mục tiêu chính bao gồm:

*   **Quản lý danh tính & truy cập (IAM)** – Nắm vững cấu trúc chính sách nâng cao để thực thi Nguyên tắc đặc quyền tối thiểu (Least Privilege).
*   **Bảo mật dữ liệu** – Triển khai mã hóa bằng AWS KMS và quản lý thông tin xác thực với Secrets Manager.
*   **Quản lý chi phí** – Phân tích mô hình chi tiêu thông qua Cost Explorer và thiết lập cảnh báo tự động với AWS Budgets.

Tuần này đảm bảo rằng cơ sở hạ tầng được xây dựng trong các tuần trước không chỉ hoạt động tốt mà còn an toàn và hiệu quả về mặt tài chính.

---

## 2. Tóm tắt công việc chi tiết

### 🗂 Bảng hoạt động

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| **Thứ Hai** | - Ôn tập kiến thức IAM cơ bản<br>- Học IAM Policy nâng cao (Cấu trúc JSON, Điều kiện)<br>- Tạo chính sách tùy chỉnh và gắn cho users/groups | 13/10/2025 | 13/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Ba** | - Giới thiệu về AWS Key Management Service (KMS)<br>- Tạo Customer Managed Key (CMK)<br>- Áp dụng KMS để mã hóa S3 bucket hoặc EBS volume | 14/10/2025 | 14/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Tư** | - Làm quen với AWS Secrets Manager<br>- Tạo secret để lưu thông tin kết nối Database<br>- Viết script Lambda nhỏ để đọc secret từ Secrets Manager | 15/10/2025 | 15/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Năm** | - Khám phá AWS Billing Dashboard và Cost Explorer<br>- Xem chi phí theo dịch vụ, khu vực và loại sử dụng<br>- Thiết lập Cost Anomaly Detection (Phát hiện bất thường) | 16/10/2025 | 16/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Sáu** | - Tạo AWS Budget và cấu hình cảnh báo qua email<br>- Viết báo cáo tổng hợp chi phí tuần với đề xuất tối ưu hóa (tắt EC2, dọn dẹp EBS)<br>- Tổng kết kiến thức Tuần 6 | 17/10/2025 | 17/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |

---

## 3. Chi tiết triển khai kỹ thuật

### 3.1 Chính sách IAM Nâng cao
*   Phân tích cấu trúc JSON: `Version`, `Statement`, `Effect`, `Action`, `Resource`.
*   Tạo **Chính sách dựa trên điều kiện (Condition)** để hạn chế truy cập theo IP nguồn hoặc tags:
    ```json
    {
        "Effect": "Allow",
        "Action": "s3:*",
        "Resource": "arn:aws:s3:::my-secure-bucket/*",
        "Condition": {
            "IpAddress": {"aws:SourceIp": "203.0.113.0/24"}
        }
    }
    ```
*   Gắn các chính sách trực tiếp (inline) vào các IAM Group cụ thể để thực thi phân chia nhiệm vụ.

### 3.2 Mã hóa dữ liệu với AWS KMS
*   Tạo khóa **Customer Managed Key (CMK)** (Đối xứng).
*   Cấu hình **Key Policy** để xác định Quản trị viên khóa và Người dùng khóa.
*   Bật mã hóa mặc định trên một S3 bucket sử dụng CMK mới tạo.
*   Thử nghiệm mã hóa thủ công qua CLI:
    ```bash
    aws kms encrypt --key-id <key-id> --plaintext fileb://data.txt --output text --query CiphertextBlob
    ```

### 3.3 Tích hợp AWS Secrets Manager
*   Lưu trữ thông tin đăng nhập RDS (username/password) an toàn trong Secrets Manager.
*   Cấu hình cài đặt tự động xoay vòng (automatic rotation) (tìm hiểu khái niệm).
*   Phát triển script Python (Boto3) cho Lambda để lấy secret bằng lập trình, tránh việc hardcode thông tin xác thực trong mã nguồn.

### 3.4 Quản lý & Tối ưu hóa chi phí
*   **Cost Explorer:** Kích hoạt các thẻ (tags) (ví dụ: `Project: WebApp`) để lọc chi phí theo từng khối lượng công việc cụ thể.
*   **AWS Budgets:** Thiết lập ngân sách hàng tháng là $10.00 với cảnh báo kích hoạt khi sử dụng đạt 80% ($8.00).
*   **Anomaly Detection:** Bật phát hiện bất thường chi phí AWS để nhận diện các đợt tăng đột biến trong việc sử dụng dịch vụ (ví dụ: vòng lặp Lambda không mong muốn).

---

## 4. Thành tựu

Đến cuối Tuần 6, các kết quả sau đã đạt được:

### ✔ Thành công về mặt chức năng
*   Thành thạo việc tạo và áp dụng các IAM Policy chi tiết để kiểm soát chặt chẽ quyền truy cập tài nguyên.
*   Triển khai thành công mã hóa dữ liệu khi nghỉ (encryption at rest) cho S3 và EBS bằng KMS.
*   Thay thế thông tin đăng nhập database hardcode bằng việc truy xuất động từ Secrets Manager.
*   Thiết lập khung quản trị chi phí sử dụng Budgets và Alerts.

### ✔ Phát triển kỹ năng
*   Hiểu sâu hơn về **Mô hình trách nhiệm chia sẻ** liên quan đến bảo mật.
*   Học cách cân bằng giữa sự nghiêm ngặt về bảo mật và khả năng vận hành dễ dàng.
*   Có nhận thức về "FinOps": cách phân tích chi phí, đề xuất các biện pháp tối ưu hóa (ví dụ: dừng EC2 nhàn rỗi, xóa EBS không gắn kết) và duy trì hiệu quả.

---

## 5. Thách thức gặp phải & Giải pháp

**Thách thức 1: Bị từ chối truy cập do KMS Key Policy**
*   **Vấn đề:** Một IAM user có quyền Admin nhưng không thể giải mã file.
*   **Giải pháp:** Hiểu rằng KMS Key Policies tách biệt với IAM policies. Đã thêm ARN của user vào phần "Key Users" trong chính sách của KMS.

**Thách thức 2: Chi phí/Độ trễ của Secrets Manager**
*   **Vấn đề:** Việc gọi Secrets Manager quá thường xuyên làm tăng chi phí và độ trễ.
*   **Giải pháp:** Triển khai cơ chế caching trong mã nguồn Lambda để lưu secret tạm thời trong ngữ cảnh thực thi (execution context).

**Thách thức 3: Đọc hiểu dữ liệu Cost Explorer**
*   **Vấn đề:** Chi phí cho mục "EC2-Other" cao và không rõ ràng.
*   **Giải pháp:** Phân tích sâu hơn theo "Usage Type" (Loại sử dụng) để xác định chi phí đến từ truyền tải dữ liệu qua NAT Gateway, dẫn đến việc xem xét lại kiến trúc.

---

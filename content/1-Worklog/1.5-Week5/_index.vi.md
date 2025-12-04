---
title: "Worklog Tuần 5"
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---
# 📘 Báo cáo công việc Tuần 5 – Hành trình AWS

## 1. Mục tiêu hàng tuần

Trong **Tuần 5**, trọng tâm chuyển từ các thao tác thủ công ("ClickOps") sang **Cơ sở hạ tầng dưới dạng mã (IaC)** và **Vận hành hệ thống**. Mục tiêu là tự động hóa việc cấp phát và quản lý tài nguyên để đảm bảo tính nhất quán và tốc độ. Các mục tiêu chính bao gồm:

*   **Cơ sở hạ tầng dưới dạng mã (IaC)** – Tìm hiểu AWS CloudFormation và AWS Cloud Development Kit (CDK).
*   **Tự động hóa** – Viết các mẫu (templates) và mã để triển khai S3 buckets và EC2 instances bằng lập trình.
*   **AWS Systems Manager (SSM)** – Tập trung hóa dữ liệu vận hành và quản lý máy chủ mà không cần khóa SSH.
*   **Tối ưu vận hành** – Triển khai các quy trình tự động khởi động/dừng máy chủ để tiết kiệm chi phí.

Tuần này đánh dấu sự chuyển đổi sang các thực hành DevOps, chuẩn bị cho việc quản lý cơ sở hạ tầng có khả năng mở rộng.

---

## 2. Tóm tắt công việc chi tiết

### 🗂 Bảng hoạt động

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| **Thứ Hai** | - Giới thiệu về khái niệm IaC và lợi ích so với triển khai thủ công<br>- Làm quen với AWS CloudFormation: template, stack, parameter | 06/10/2025 | 06/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Ba** | - Viết CloudFormation template để triển khai S3 bucket và EC2 instance<br>- Tạo, cập nhật và xóa stack thông qua AWS Console | 07/10/2025 | 07/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Tư** | - Giới thiệu về AWS CDK (Cloud Development Kit)<br>- Cài đặt AWS CDK, tạo dự án CDK bằng Python hoặc TypeScript<br>- Viết mã CDK để triển khai EC2 instance | 08/10/2025 | 08/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Năm** | - Giới thiệu về AWS Systems Manager (SSM) và các tính năng chính<br>- Tạo Parameter Store để lưu trữ các biến cấu hình | 09/10/2025 | 09/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Sáu** | - Thực hành tạo Automation Document trong SSM để tự động Start/Stop EC2<br>- Test Session Manager (truy cập EC2 không cần khóa SSH)<br>- Tổng kết tuần: Demo IaC + SSM | 10/10/2025 | 10/10/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |

---

## 3. Chi tiết triển khai kỹ thuật

### 3.1 AWS CloudFormation
*   **Thiết kế Template:** Tạo tệp YAML định nghĩa `AWS::S3::Bucket` và `AWS::EC2::Instance`.
*   **Parameters (Tham số):** Sử dụng `Parameters` để cho phép nhập `InstanceType` (ví dụ: t2.micro) tại thời điểm triển khai.
*   **Thao tác với Stack:**
    *   **Create Stack:** Tải template lên CloudFormation Designer.
    *   **Update Stack:** Sửa đổi template (thêm tags) và áp dụng changeset.
    *   **Drift Detection:** Kiểm tra xem tài nguyên có bị thay đổi thủ công bên ngoài stack hay không.

### 3.2 AWS CDK (Cloud Development Kit)
*   **Cài đặt:** Cài đặt Node.js và CDK CLI (`npm install -g aws-cdk`).
*   **Khởi tạo:** Tạo dự án mới: `cdk init app --language python`.
*   **Viết mã:** Định nghĩa tài nguyên sử dụng các cấu trúc cấp cao (L2 constructs) bằng Python.
*   **Triển khai:**
    *   `cdk synth`: Tạo ra template CloudFormation từ mã nguồn.
    *   `cdk deploy`: Cấp phát tài nguyên vào tài khoản AWS.

### 3.3 AWS Systems Manager (SSM)
*   **Parameter Store:** Tạo các tham số phân cấp (ví dụ: `/dev/db/password`) dạng `SecureString` để lưu cấu hình nhạy cảm.
*   **Session Manager:**
    *   Gắn IAM role `AmazonSSMManagedInstanceCore` vào EC2 instance.
    *   Kết nối thành công vào shell của instance thông qua AWS Console (trình duyệt) mà không cần mở cổng 22 (SSH).
*   **Automation:** Thực thi một SSM Document (`AWS-StopEC2Instance`) để kiểm tra các tác vụ vận hành tự động.

---

## 4. Thành tựu

Đến cuối Tuần 5, các kết quả sau đã đạt được:

### ✔ Thành công về mặt chức năng
*   Thay thế thành công việc tạo tài nguyên thủ công bằng các CloudFormation templates có thể tái sử dụng.
*   Triển khai một stack cơ sở hạ tầng hoạt động tốt bằng mã lệnh (CDK).
*   Loại bỏ nhu cầu quản lý khóa SSH nhờ sử dụng SSM Session Manager.
*   Tập trung hóa việc quản lý cấu hình bằng SSM Parameter Store.

### ✔ Phát triển kỹ năng
*   Hiểu sự khác biệt giữa các phương pháp IaC **Declarative** (Khai báo - CloudFormation) và **Imperative** (Mệnh lệnh - CDK).
*   Học được tầm quan trọng của tính **Idempotency** (Tính bất biến/nhất quán) trong triển khai cơ sở hạ tầng.
*   Có kinh nghiệm quản lý dựa trên **Agent** (SSM Agent).
*   Cải thiện tư thế bảo mật bằng cách loại bỏ nhu cầu truy cập SSH công khai.

---

## 5. Thách thức gặp phải & Giải pháp

**Thách thức 1: Lỗi thụt lề (Indentation) trong CloudFormation YAML**
*   **Vấn đề:** Việc tạo Stack thất bại do lỗi phân tích cú pháp trong tệp YAML.
*   **Giải pháp:** Sử dụng YAML Linter và tiện ích mở rộng VS Code "CloudFormation Linter" để xác thực cú pháp trước khi tải lên.

**Thách thức 2: CDK Bootstrapping**
*   **Vấn đề:** Lệnh `cdk deploy` thất bại với lỗi thiếu toolkit stack.
*   **Giải pháp:** Hiểu rằng môi trường phải được bootstrap một lần cho mỗi region bằng lệnh `cdk bootstrap aws://<account-id>/<region>`.

**Thách thức 3: SSM Agent không kết nối**
*   **Vấn đề:** EC2 instance không xuất hiện trong Systems Manager Fleet Manager.
*   **Giải pháp:** Phát hiện ra EC2 instance thiếu IAM Role cần thiết (`AmazonSSMManagedInstanceCore`). Đã gắn role và khởi động lại instance.

---



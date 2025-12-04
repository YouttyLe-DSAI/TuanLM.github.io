---
title: "Worklog Tuần 10"
weight: 2
chapter: false
pre: " <b> 1.10. </b> "
---
# 📘 Báo cáo công việc Tuần 10 – AWS Journey 

## 1. Mục tiêu hàng tuần

Trong **Tuần 10**, quá trình khám phá mở rộng sang lĩnh vực **Trí tuệ nhân tạo (AI) và Học máy (ML)** của AWS. Mục tiêu chính là phân biệt giữa việc xây dựng các mô hình tùy chỉnh và sử dụng các dịch vụ AI được huấn luyện trước. Các mục tiêu chính bao gồm:

*   **Hệ sinh thái AI AWS** – Hiểu bối cảnh của các dịch vụ ML (SageMaker) so với Dịch vụ AI (Rekognition, Comprehend, Kendra).
*   **Amazon SageMaker** – Trải nghiệm vòng đời ML đầy đủ: Xây dựng (Build), Huấn luyện (Train) và Triển khai (Deploy).
*   **Thị giác máy tính & NLP** – Triển khai phân tích hình ảnh và xử lý ngôn ngữ tự nhiên mà không cần chuyên môn sâu về khoa học dữ liệu bằng cách sử dụng AWS API.
*   **Tìm kiếm thông minh** – Thiết lập khả năng tìm kiếm doanh nghiệp với Amazon Kendra.

Tuần này làm nổi bật cách AWS dân chủ hóa AI, cho phép các nhà phát triển thêm trí thông minh vào ứng dụng thông qua các lệnh gọi API hoặc xây dựng các mô hình tùy chỉnh với cơ sở hạ tầng được quản lý.

---

## 2. Tóm tắt công việc chi tiết

### 🗂 Bảng hoạt động

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| **Thứ Hai** | - Tổng quan về AI/ML trên AWS<br>- Tìm hiểu các dịch vụ hỗ trợ ML: SageMaker, Rekognition, Comprehend, Kendra, Translate, Polly | 10/11/2025 | 10/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Ba** | - Thực hành với Amazon SageMaker:<br>- Tạo Notebook Instance<br>- Huấn luyện mô hình đơn giản (Hồi quy tuyến tính / Phân loại ảnh)<br>- Triển khai endpoint và kiểm tra dự đoán | 11/11/2025 | 11/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Tư** | - Làm quen với Amazon Rekognition<br>- Demo nhận diện khuôn mặt và vật thể trong ảnh/video<br>- Tích hợp Rekognition API vào ứng dụng web nhỏ | 12/11/2025 | 12/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Năm** | - Thực hành Amazon Comprehend (xử lý ngôn ngữ tự nhiên)<br>- Thử nghiệm Amazon Kendra (tìm kiếm thông minh theo ngữ cảnh)<br>- So sánh ưu điểm và hạn chế của từng dịch vụ | 13/11/2025 | 13/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Sáu** | - Tổng hợp kiến thức Tuần 10 (Quy trình phát triển AI/ML)<br>- Ứng dụng thực tế của AI/ML trong doanh nghiệp<br>- Viết báo cáo kết quả thực hành và hướng mở rộng | 14/11/2025 | 14/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |

---

## 3. Chi tiết triển khai kỹ thuật

### 3.1 Amazon SageMaker (Custom ML)
*   **Notebook Instance:** Khởi chạy một instance Jupyter Notebook `ml.t2.medium`.
*   **Huấn luyện:** Sử dụng thuật toán tích hợp sẵn (như XGBoost) để huấn luyện mô hình trên tập dữ liệu mẫu (ví dụ: dự đoán giá nhà hoặc bộ dữ liệu MNIST).
*   **Triển khai:** Triển khai mô hình đã huấn luyện tới một HTTPS Endpoint thời gian thực.
*   **Suy luận (Inference):** Gọi endpoint bằng Python (Boto3) để tạo dự đoán từ dữ liệu mới.

### 3.2 Amazon Rekognition (Thị giác máy tính)
*   **Phân tích hình ảnh:** Tải ảnh lên S3 và sử dụng API `DetectLabels` để nhận diện vật thể (ví dụ: "Xe hơi", "Cây", "Người") với điểm tin cậy.
*   **Phân tích khuôn mặt:** Sử dụng `DetectFaces` để ước tính độ tuổi, cảm xúc và giới tính.
*   **Tích hợp:** Viết một script đơn giản kích hoạt hàm Lambda khi có ảnh được tải lên S3 để tự động gắn thẻ bằng Rekognition.

### 3.3 Amazon Comprehend (NLP)
*   **Phân tích cảm xúc:** Xử lý văn bản đánh giá của khách hàng để xác định cảm xúc (Tích cực, Tiêu cực, Trung lập).
*   **Nhận diện thực thể:** Trích xuất các thực thể cụ thể (Ngày tháng, Địa điểm, Tên riêng) từ các tài liệu văn bản phi cấu trúc.

### 3.4 Amazon Kendra (Tìm kiếm thông minh)
*   **Tạo chỉ mục:** Tạo Kendra Index (Phiên bản Developer).
*   **Nguồn dữ liệu:** Kết nối một S3 bucket chứa các file PDF hướng dẫn sử dụng làm cơ sở tri thức.
*   **Truy vấn:** Thử nghiệm các truy vấn ngôn ngữ tự nhiên (ví dụ: "Làm thế nào để reset thiết bị?") trong bảng điều khiển và nhận được câu trả lời chính xác được trích xuất từ tài liệu.

---

## 4. Thành tựu

Đến cuối Tuần 10, các kết quả sau đã đạt được:

### ✔ Thành công về mặt chức năng
*   Thành công huấn luyện và lưu trữ một mô hình Học máy sử dụng **Amazon SageMaker**.
*   Triển khai các tính năng **Thị giác máy tính** (Nhận diện khuôn mặt/Vật thể) thông qua lệnh gọi API.
*   Trích xuất thông tin chi tiết từ văn bản bằng **Amazon Comprehend**.
*   Thiết lập công cụ tìm kiếm tài liệu hoạt động tốt bằng **Amazon Kendra**.

### ✔ Phát triển kỹ năng
*   Hiểu rõ sự phân biệt giữa **Dịch vụ AI** (API cấp cao cho nhà phát triển) và **Dịch vụ ML** (SageMaker cho Nhà khoa học dữ liệu).
*   Có kinh nghiệm về chi phí **Suy luận mô hình (Inference)** và quản lý endpoint.
*   Học cách tích hợp khả năng AI vào các ứng dụng hiện có bằng AWS SDK.

---

## 5. Thách thức gặp phải & Giải pháp

**Thách thức 1: Quản lý chi phí SageMaker**
*   **Vấn đề:** SageMaker Notebooks và Endpoints tính phí theo giờ ngay cả khi nhàn rỗi.
*   **Giải pháp:** Tạo quy trình "Dọn dẹp" để xóa Endpoints và Stop Notebook instances ngay sau khi hoàn thành bài lab để tránh hóa đơn ngoài ý muốn.

**Thách thức 2: Quyền IAM cho Rekognition**
*   **Vấn đề:** Lỗi `AccessDeniedException` khi Rekognition cố gắng đọc ảnh từ S3 bucket.
*   **Giải pháp:** Cập nhật Bucket Policy và IAM Role để cấp quyền `s3:GetObject` rõ ràng cho user/role đang gọi Rekognition API.

**Thách thức 3: Thời gian lập chỉ mục Kendra**
*   **Vấn đề:** Kendra mất khá nhiều thời gian (30+ phút) để tạo chỉ mục và đồng bộ dữ liệu.
*   **Giải pháp:** Hiểu rằng Kendra là dịch vụ cấp doanh nghiệp cần thời gian cấp phát; lên kế hoạch tác vụ để làm việc với Comprehend trong khi chờ Kendra khởi tạo.

---


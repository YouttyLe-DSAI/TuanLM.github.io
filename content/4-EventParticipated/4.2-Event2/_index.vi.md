---
title: "Event 2"
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# Workshop: Data Science on AWS

> **Thời gian:** 9:30 – 11:45, Ngày 16/10/2025 <br>
> **Địa điểm:** Hall A - Đại học FPT TP.HCM (FPTU HCMC) <br>
> **Vai trò:** Người tham dự

### Mục tiêu tham dự
- Tìm hiểu về bức tranh toàn cảnh (Landscape) các dịch vụ AI/ML của AWS.
- Tiếp cận cách xây dựng, huấn luyện và triển khai mô hình Machine Learning thực tế.
- Giao lưu với các chuyên gia từ cộng đồng AWS User Group.

### Danh Sách Diễn Giả

- Van Hoang Kha - Cloud Solutions Architect, AWS User Group Leader
- Bach Doang Vuong - Cloud DevOps Engineer, AWS Community Builder

### Nội dung chính

#### 1. Hệ sinh thái AWS AI/ML Stack
Diễn giả đã giới thiệu cấu trúc 3 tầng của AWS AI/ML Stack rất rõ ràng:
- **AI Services (Top layer):** Các dịch vụ có sẵn, không cần kiến thức sâu về ML vẫn dùng được (Vision, Speech, Chatbots...).
- **ML Services (Middle layer):** Nền tảng Amazon SageMaker giúp xây dựng, huấn luyện và triển khai mô hình.
- **Frameworks & Infrastructure (Bottom layer):** Dành cho chuyên gia muốn can thiệp sâu (PyTorch, TensorFlow, EC2 GPU...).

#### 2. Các AI Services nổi bật & Demo
Phần này em thấy rất thú vị vì tính ứng dụng cao, có thể tích hợp ngay vào đồ án của sinh viên:
- **Xử lý hình ảnh (Vision):** **Amazon Rekognition** giúp nhận diện gương mặt, phân tích video, phát hiện đồ bảo hộ (PPE Detection) và kiểm duyệt nội dung (Content Moderation).
- **Xử lý âm thanh & giọng nói:** Combo **Amazon Polly** (chuyển văn bản thành giọng nói giống người thật) và **Amazon Transcribe** (chuyển giọng nói thành văn bản, hỗ trợ cả cuộc gọi thời gian thực).
- **Xử lý ngôn ngữ tự nhiên (NLP):**
    - **Amazon Translate:** Dịch thuật đa ngôn ngữ với độ trễ thấp.
    - **Amazon Textract:** Bóc tách dữ liệu từ văn bản scan/hóa đơn cực nhanh.
    - **Amazon Lex:** Xây dựng Chatbot hội thoại (Conversational Interfaces) thông minh.
- **Cá nhân hóa trải nghiệm:** **Amazon Personalize** giúp tạo ra các đề xuất sản phẩm (recommendation) theo thời gian thực mà không cần chuyên môn sâu về ML.

#### 3. Quy trình Machine Learning với SageMaker
Các diễn giả đã demo quy trình từ **Feature Engineering** (xử lý dữ liệu thô) đến Training và Tuning tham số. Đặc biệt là demo việc mang code Python (Scikit-learn, TensorFlow) có sẵn để chạy trên hạ tầng mạnh mẽ của AWS.

### Trải nghiệm cá nhân

Đây là một buổi workshop rất "sát sườn" với sinh viên tụi em.
- Em rất ấn tượng phần chia sẻ về **Amazon Personalize**. Trước giờ em cứ nghĩ làm tính năng "Gợi ý sản phẩm" (Recommendation System) rất khó và tốn công code thuật toán, nhưng với AWS thì việc này đơn giản hơn rất nhiều.
- Một điểm cộng lớn là diễn giả chia sẻ rất thực tế về vấn đề **Chi phí (Cost)**. Slide về "Monitoring Cost Daily" giúp em nhận ra rằng làm Cloud không chỉ là code chạy được, mà còn phải biết cách tối ưu để không bị "thủng ví" vào cuối tháng.
- Không khí tại FPTU rất năng lượng, được nghe các anh đi trước chia sẻ kinh nghiệm thực chiến làm em có thêm động lực để học thi chứng chỉ AWS sắp tới.

### Một số hình ảnh khi tham gia sự kiện

![event2-1](/images/4-event/event2-1.png)

![event2-2](/images/4-event/event2-2.jpg)

![event2-2](/images/4-event/event2-3.png)

> **Tóm lại:** Event này giúp em "khai sáng" rất nhiều về bộ công cụ AI Services. Thay vì tự build model từ con số 0, em đã biết cách tận dụng các API có sẵn của AWS để giải quyết bài toán nhanh hơn và xịn hơn.
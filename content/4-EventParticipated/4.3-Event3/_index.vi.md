---
title: "Event 3"
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

# AWS Cloud Mastery Series #1: AI/ML/GenAI on AWS

> **Thời gian:** Thứ Bảy, ngày 15/11/2025, 8:30 – 12:00 <br>
> **Địa điểm:** AWS Vietnam Office, Tòa nhà Bitexco Financial Tower, Quận 1, TP.HCM <br>
> **Vai trò:** Người tham dự (Learner)

### Mục Đích Của Sự Kiện

- Có cái nhìn tổng quan về bức tranh **AI/ML tại Việt Nam** và hệ sinh thái các dịch vụ AI toàn diện của AWS.
- Đi sâu vào kỹ thuật (Deep-dive) với **Amazon SageMaker** để hiểu quy trình MLOps từ chuẩn bị dữ liệu đến triển khai mô hình.
- Nắm vững các công nghệ lõi của **Generative AI** trên Amazon Bedrock, bao gồm Prompt Engineering và RAG.
- Tìm hiểu về xu hướng chuyển dịch từ Chatbot sang **Agentic AI**.

### Danh Sách Diễn Giả

- **Danh Hoàng Hiếu Nghị:** Chuyên gia về Amazon Bedrock AgentCore và hệ sinh thái Agent.
- **Đinh Lê Hoàng Anh:** Demo các dịch vụ Pre-trained AI Services và ứng dụng thực tế (AMZ Photo).
- **Lâm Tuấn Kiệt:** Chuyên gia về Generative AI, kỹ thuật Prompt Engineering và kiến trúc RAG.

### Nội Dung Nổi Bật

Sự kiện tập trung vào 3 mảng chính của AWS AI Stack:

1.  **AI Services (Pre-trained):**
    - Giới thiệu các dịch vụ "mì ăn liền" như Amazon Rekognition (xử lý ảnh), Transcribe (giọng nói sang văn bản), Polly (văn bản sang giọng nói).
    - Demo ứng dụng **AMZ Photo**: Quản lý ảnh thông minh, tích hợp tìm kiếm khuôn mặt và chatbot đa phương thức sử dụng framework Pipecat.

2.  **Generative AI với Amazon Bedrock:**
    - So sánh các Foundation Models (Claude, Llama, Titan).
    - Các kỹ thuật tối ưu hóa Prompt: Zero-shot, Few-shot và Chain-of-Thought (CoT).
    - Kiến trúc **RAG (Retrieval-Augmented Generation)**: Kết hợp mô hình ngôn ngữ với dữ liệu doanh nghiệp thông qua Vector Database.

3.  **Agentic AI & AgentCore:**
    - Sự tiến hóa từ Generative AI Assistants sang Agentic AI (có khả năng tự thực thi tác vụ).
    - Giới thiệu **AgentCore**: Các thành phần như Memory, Identity, Gateway và Code Interpreter giúp Agent vận hành ở quy mô lớn.

### Những Gì Học Được

- **Tư duy về Prompt Engineering:** Prompt không chỉ là câu lệnh đơn giản mà là một kỹ thuật lập trình ngôn ngữ tự nhiên. Việc sử dụng *Chain-of-Thought* giúp mô hình giải quyết các bài toán logic phức tạp tốt hơn nhiều so với cách hỏi thông thường.
- **Quy trình RAG chuẩn:** Hiểu rõ luồng dữ liệu (Data Ingestion -> Embeddings -> Vector Store -> Semantic Search) để giải quyết vấn đề "ảo giác" (hallucination) của AI.
- **Sức mạnh của Pre-trained Services:** Không nhất thiết phải xây dựng model từ đầu. Việc kết hợp các API có sẵn (như Rekognition, Textract) giúp giảm đáng kể thời gian đưa sản phẩm ra thị trường (Time-to-market).
- **Kiến trúc Agent:** Hiểu được sự khác biệt giữa một Chatbot thụ động và một Agent chủ động có khả năng sử dụng công cụ (Tools) và truy cập trình duyệt (Browser Viewer).

### Ứng Dụng Vào Công Việc

- **Tối ưu hóa Chatbot nội bộ:** Áp dụng ngay kiến trúc **RAG** và model **Titan Text Embeddings V2** để nâng cấp chatbot hỗ trợ tra cứu tài liệu kỹ thuật của công ty, đảm bảo câu trả lời chính xác dựa trên nguồn dữ liệu thực tế.
- **Tự động hóa xử lý tài liệu:** Đề xuất sử dụng **Amazon Textract** kết hợp với **Comprehend** để trích xuất và phân loại thông tin từ các hóa đơn/hợp đồng giấy tờ, thay thế quy trình nhập liệu thủ công.
- **Nghiên cứu Agentic Workflow:** Thử nghiệm xây dựng một Agent đơn giản bằng **LangGraph** hoặc **Amazon Bedrock Agents** để tự động hóa quy trình tổng hợp tin tức thị trường hàng ngày cho team Business.

### Trải Nghiệm Cá Nhân

Tham dự AWS Cloud Mastery Series tại văn phòng AWS Việt Nam là một trải nghiệm rất giá trị về mặt chuyên môn đối với em:

- Phần chia sẻ của anh **Lâm Tuấn Kiệt** rất thực tế, đặc biệt là các ví dụ minh họa về Prompt Engineering. Nó giúp em nhận ra những sai lầm trước đây khi tương tác với LLM và cách cải thiện chất lượng câu trả lời một cách khoa học.
- Demo của anh **Đinh Lê Hoàng Anh** với ứng dụng AMZ Photo rất ấn tượng. Việc tích hợp đa phương thức (Multimodal) và xử lý thời gian thực cho thấy tiềm năng to lớn của việc kết hợp các dịch vụ AWS lại với nhau.
- Chủ đề về Agentic AI của anh **Danh Hoàng Hiếu Nghị** mang tính định hướng cao. Dù kiến trúc AgentCore khá phức tạp, nhưng nó mở ra góc nhìn mới về việc AI không chỉ là công cụ hỗ trợ mà có thể trở thành "nhân viên ảo" thực thụ.

### Một số hình ảnh tại sự kiện

![aws-mastery-1](/images/4-event/event3-1.png)
![aws-mastery-2](/images/4-event/event3-2.png)
![aws-mastery-3](/images/4-event/event3-3.png)

> Tổng kết: Một buổi workshop chuyên sâu, kết hợp cân bằng giữa lý thuyết nền tảng và demo thực chiến. Các kiến thức về RAG và Agentic AI sẽ là trọng tâm nghiên cứu của em trong thời gian tới.
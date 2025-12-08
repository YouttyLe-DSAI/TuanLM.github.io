---
title: "Event 1"
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Vietnam Cloud Day 2025: Ho Chi Minh City Connect Edition for Builders

> **Thời gian:** Thứ Năm, ngày 18/09/2025, 9:00 – 17:30 <br>
> **Địa điểm:** Amazon Web Services Vietnam, Tầng 36, số 2 Hải Triều, Phường Bến Nghé, Quận 1, Thành phố Hồ Chí Minh <br>
> **Vai trò:** Người tham dự

### Mục Đích Của Sự Kiện

- Cập nhật xu hướng công nghệ chiến lược hàng đầu: **Agentic AI**.
- Tìm hiểu giải pháp xây dựng nền tảng dữ liệu (Data Foundation) để giải quyết vấn đề "Data Silos" mà 52% CDO đang gặp phải.
- Tiếp cận quy trình phát triển phần mềm mới **AI-Driven Development Lifecycle (AI-DLC)**.
- Nắm bắt các tiêu chuẩn bảo mật cho GenAI (MITRE ATLAS, OWASP, NIST) và các tầng rủi ro.

### Danh Sách Diễn Giả

- Eric Yeo - Country General Manager, AWS Vietnam
- Dr. Jens Lottner - CEO, Techcombank
- Ms. Trang Phung - CEO & Co-Founder, U2U Network
- Jaime Valles - VP, GM Asia Pacific and Japan, AWS
- Jeff Johnson - Managing Director, ASEAN, AWS
- Vu Van - Co-founder & CEO, ELSA Corp
- Nguyen Hoa Binh - Chairman, Nexttech Group
- Dieter Botha - CEO, TymeX
- Jun Kai Loke - AI/ML Specialist SA, AWS
- Kien Nguyen - Solutions Architect, AWS
- Tamelly Lim - Storage Specialist SA, AWS
- Binh Tran - Senior Solutions Architect, AWS
- Taiki Dang - Solutions Architect, AWS
- Michael Armentano - Principal WW GTM Specialist, AWS
- Hung Nguyen Gia - Head of Solutions Architect, AWS
- Son Do - Technical Account Manager, AWS
- Nguyen Van Hai - Director of Software Engineering, Techcombank
- Phuc Nguyen - Solutions Architect, AWS
- Alex Tran - AI Director, OCB
- Nguyen Minh Ngan - AI Specialist, OCB
- Nguyen Manh Tuyen - Head of Data Application, LPBank Securities
- Vinh Nguyen - Co-Founder & CTO, Ninety Eight
- Hung Hoang - Customer Solutions Manager, AWS
- Christal Poon - Specialist Solutions Architect, AWS

### Nội Dung Nổi Bật

#### 1. Xu hướng Agentic AI & Data Strategy
- **Thực trạng:** 88% CDO đang tiến tới với GenAI, nhưng 52% cho rằng nền tảng dữ liệu chưa sẵn sàng.
- **Thách thức:** Doanh nghiệp bị kìm hãm bởi 3 loại "Silos": Data Silos, People Silos, và Business Silos.
- **Chiến lược dữ liệu:** Mô hình End-to-end từ Producers → Foundations → Consumers.
    - **Hạ tầng:** Amazon S3 (Data Lakes), Amazon Redshift (Data Warehouses), hỗ trợ chuẩn mở Apache Iceberg.
    - **Quản trị:** Amazon DataZone giúp quản trị dữ liệu và AI (Data & AI Governance).
    - **Công cụ mới:** Giới thiệu **Unified Studio** tích hợp các công cụ analytics và AI.

#### 2. AI-Driven Development Lifecycle (AI-DLC)
Speaker **Binh Tran** đã giới thiệu sự chuyển dịch từ *AI-Assisted* sang *AI-Driven Development*.
Quy trình AI-DLC gồm 3 giai đoạn chính:
1.  **Inception:** Build Context trên code hiện có, làm rõ ý định (User Stories), lên kế hoạch (Units of Work), mô hình hóa Domain.
2.  **Construction:** AI tự sinh code & Test, bổ sung các thành phần kiến trúc.
3.  **Operation:** Triển khai với IaC & tests, quản lý sự cố.

#### 3. Bảo mật GenAI (Security for GenAI)
Speaker **Taiki Dang** nhấn mạnh bảo mật phải chạy song hành với Generative AI.
- **Phân lớp rủi ro (Risks Layers):**
    - *Top layer (Consumer):* Rủi ro về IP, pháp lý, ảo giác (Hallucination), an toàn.
    - *Middle layer (Tuner):* Rủi ro từ Managed services, chính sách lưu trữ dữ liệu.
    - *Bottom layer (Provider):* Rủi ro từ dữ liệu training.
- **Framework & Tiêu chuẩn:** Áp dụng MITRE ATLAS, OWASP Top 10 for LLM, NIST AI RMF, ISO 42001.
- **Giải pháp:** Sử dụng **Amazon Bedrock Guardrails** để ngăn chặn và giảm thiểu rủi ro (như toxicity, PII leak).

#### 4. Analytics & Business Intelligence
Speaker **Christal Poon** giới thiệu về sự chuyển đổi từ Amazon QuickSight sang **Amazon Q**.
- Tính năng tạo Dashboard, báo cáo và Data QA bằng ngôn ngữ tự nhiên.
- **Sắp ra mắt tại Việt Nam:** Amazon Agentic AI Workbench (Quick Suite) với khả năng Quick Researcher và Quick Automate, đưa con người vào vòng lặp (Human in the loop) để kiểm soát.

### Những Gì Học Được

- **Tư duy về Agent:** Hiểu rõ cấu trúc của một AI Agent gồm: Goals → Observation → Tools → Context → Action.
- **Kiến trúc Agent Core:** Cần đảm bảo đủ các thành phần: Runtime, Gateway, Memory, Observability và Identity để đưa Agent vào production một cách an toàn và mở rộng được.
- **Bảo mật đa lớp:** Không chỉ bảo mật ứng dụng mà phải kiểm soát rủi ro từ dữ liệu training, quá trình fine-tuning cho đến người dùng cuối (Consumer risks).

### Ứng Dụng Vào Công Việc

- **Triển khai AI-DLC:** Thử nghiệm áp dụng quy trình 7 bước của AI-DLC vào dự án mới, bắt đầu từ việc dùng AI để "Build Context" và "Domain Modeling".
- **Tăng cường bảo mật:** Rà soát lại ứng dụng GenAI hiện tại theo checklist của **OWASP Top 10 for LLM** và tích hợp **Bedrock Guardrails** để lọc nội dung độc hại.
- **Modernize Data Stack:** Đánh giá khả năng chuyển đổi Data Warehouse hiện tại sang kiến trúc **Lakehouse** với Apache Iceberg trên AWS để phá vỡ các Data Silos.

### Trải Nghiệm Cá Nhân

Sự kiện lần này thực sự đi sâu vào kỹ thuật (deep-dive) hơn em mong đợi, mang lại nhiều giá trị thực tiễn:
- Em rất tâm đắc với phần chia sẻ về **AI-DLC** của anh Bình Trần. Nó thay đổi hoàn toàn cách em nhìn nhận về việc coding: developer không còn chỉ viết code mà trở thành người "kiến trúc" và "review" cho AI thực thi.
- Slide về **Scoping Matrix** và các lớp rủi ro trong GenAI giúp em có cái nhìn hệ thống hơn để giải trình với bộ phận Security của công ty khi muốn triển khai dự án AI mới.
- Rất hào hứng với thông tin **Amazon Agentic AI Workbench** sắp về Việt Nam, hứa hẹn sẽ giải quyết được bài toán tự động hóa quy trình nghiên cứu thị trường (Quick Researcher) mà team business đang cần.

### Một số hình ảnh khi tham gia sự kiện

![event1-1](/images/4-event/event1-1.png)

![event1-2](/images/4-event/event1-2.png)

> Tổng kết: Một sự kiện "must-attend" cho Builders. Kiến thức về Agentic AI và AI-DLC sẽ là kim chỉ nam cho lộ trình phát triển kỹ thuật của em trong năm tới.
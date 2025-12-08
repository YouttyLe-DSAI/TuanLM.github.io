---
title: "Event 5"
weight: 5
chapter: false
pre: " <b> 4.5. </b> "
---

# AWS Cloud Mastery Series #3: AWS Well-Architected Security Pillar

> **Thời gian:** Thứ Bảy, ngày 29/11/2025, 8:30 – 12:00 <br>
> **Địa điểm:** AWS Vietnam Office, Tòa nhà Bitexco Financial Tower, Quận 1, TP.HCM <br>
> **Vai trò:** Người tham dự (Learner)

### Mục Đích Của Sự Kiện

- Hiểu sâu về **Security Pillar** trong AWS Well-Architected Framework, chuyển dịch tư duy từ bảo mật vành đai (Perimeter Security) sang **Zero Trust**.
- Nắm vững kiến trúc **Modern IAM** để quản lý định danh và truy cập quy mô lớn.
- Học cách xây dựng hệ thống "miễn dịch" tự động với **Detection-as-Code** và **Automated Remediation**.
- Thực hành các chiến lược bảo vệ hạ tầng (Infrastructure Protection) và dữ liệu (Data Protection) trước các vector tấn công phổ biến.

### Danh Sách Diễn Giả

- **Trần Đức Anh** - Cloud Security Engineer Trainee, AWS Cloud Club Captain SGU.
- **Nguyễn Tuấn Thành** - Cloud Engineer Trainee.
- **Nguyễn Đỗ Thành Đạt** - Cloud Engineer Trainee.
(Cùng đội ngũ kỹ thuật từ AWS Cloud Clubs và First Cloud Journey)

### Nội Dung Nổi Bật

Buổi workshop đi sâu vào 5 trụ cột chính của bảo mật trên AWS:

1.  **Identity & Access Management (IAM):**
    - Nguyên tắc "Kill long-lived credentials": Thay thế Access Key lâu dài bằng IAM Roles và Temporary Tokens.
    - Sử dụng **IAM Access Analyzer** để phát hiện các policy quá lỏng lẻo (như `Principal: *`).
    - Demo cấu hình **SSO (Single Sign-On)** để quản lý truy cập tập trung cho nhiều tài khoản AWS.

2.  **Detection & Continuous Monitoring:**
    - Triển khai **Detection-as-Code**: Dùng CloudFormation/Terraform để bật GuardDuty và Security Hub trên toàn bộ Organization thay vì click tay.
    - **Runtime Monitoring**: GuardDuty Agent cài sâu vào EC2/EKS để phát hiện các tiến trình lạ (process injection) hoặc file access bất thường.

3.  **Infrastructure Protection:**
    - Chiến lược **Defense in Depth** (Phòng thủ chiều sâu): Kết hợp WAF, Shield ở Edge -> Network Firewall ở VPC -> Security Group ở Instance.
    - Phân biệt rõ ràng vai trò của Security Group (Stateful) và NACL (Stateless) trong việc chống lại các cuộc tấn công DDoS hay Lateral Movement.

4.  **Incident Response (IR):**
    - Tự động hóa quy trình phản ứng sự cố: CloudTrail log -> EventBridge filter -> Lambda function tự động cách ly EC2 bị nhiễm malware hoặc xoay (rotate) credential bị lộ.

### Những Gì Học Được

- **Tư duy "No ClickOps":** Trong bảo mật, việc cấu hình thủ công là kẻ thù. Mọi rule bảo mật, từ Security Group đến GuardDuty detector, đều phải được định nghĩa bằng Code (IaC) và version control.
- **Shared Responsibility Model:** Hiểu rõ phần nào AWS lo (Security *of* the Cloud) và phần nào mình phải lo (Security *in* the Cloud), đặc biệt là việc mã hóa dữ liệu (Encryption at rest/in transit).
- **Sức mạnh của EventBridge:** Nó không chỉ là message bus mà là "hệ thần kinh trung ương" giúp kết nối việc phát hiện (Detection) với hành động khắc phục (Remediation) trong thời gian thực.
- **Micro-segmentation:** Không bao giờ tin tưởng mạng nội bộ. Việc chia nhỏ VPC thành các subnet public/private và kẹp chặt bằng Security Group là bắt buộc.

### Ứng Dụng Vào Công Việc

- **Rà soát IAM ngay lập tức:** Kiểm tra lại toàn bộ IAM User trong dự án công ty, xóa các Access Key không dùng, và bật MFA cho 100% tài khoản, đặc biệt là tài khoản Root.
- **Triển khai GuardDuty:** Đề xuất bật GuardDuty ở mức Organization để có ngay khả năng phát hiện các mối đe dọa cơ bản (như đào coin, scan port) mà không tốn nhiều công sức cấu hình.
- **Secret Management:** Dừng ngay việc lưu hardcode password trong code hay file `.env`. Chuyển sang dùng **AWS Secrets Manager** và thiết lập tự động xoay vòng (Automatic Rotation) cho DB credentials.

### Trải Nghiệm Cá Nhân

Thực sự là một buổi sáng "căng não" nhưng cực kỳ chất lượng. Dù diễn giả là các bạn Trainee/Student nhưng kiến thức rất sâu và thực chiến:

- Em rất ấn tượng với slide **"Prevention - Nobody has time for incidents"**. Câu nói "Public buckets = your data on the evening news" nghe vừa hài hước vừa thấm thía về tầm quan trọng của việc chặn S3 public access.
- Phần demo về **Automated Remediation** làm em mở mang tầm mắt. Trước giờ cứ nghĩ Incident Response là phải có người ngồi trực monitor, nhưng hóa ra có thể viết Lambda để tự động "xử đẹp" các mối nguy ngay khi nó vừa xuất hiện.
- Slide về **Network Attack Vectors** vẽ rất trực quan đường đi của Hacker từ Internet qua các lớp bảo vệ, giúp em hình dung rõ hơn về kiến trúc mạng an toàn.

### Một số hình ảnh tại sự kiện

![aws-mastery-1](/images/4-event/event5-1.png)
![aws-mastery-2](/images/4-event/event5-2.png)
![aws-mastery-3](/images/4-event/event5-3.png)

> Tổng kết: Bảo mật không phải là rào cản, mà là yếu tố then chốt để doanh nghiệp đi nhanh và an toàn hơn. Sự kiện giúp em tự tin hơn hẳn khi đề xuất các giải pháp security cho dự án sắp tới.
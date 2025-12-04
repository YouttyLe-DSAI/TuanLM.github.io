---
title: "Worklog Tuần 1"
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---
### Mục tiêu tuần 1:
- Làm quen quy trình, kênh liên lạc và nội quy thực tập FCJ.  
- Hoàn tất **AWS Free Tier**, cấu hình **AWS CLI**, hiểu các nhóm dịch vụ cốt lõi.  
- Thực hành EC2/EBS/SSH và thiết lập **AWS Budgets** để kiểm soát chi phí.
- Nắm tổng quan hệ sinh thái AWS (Compute, Storage, Networking, Database, Security).  
- Sử dụng thành thạo bước đầu **AWS Management Console** & **AWS CLI v2**.  
- Tạo và vận hành một **EC2 t2.micro** trong Free Tier; thao tác **EBS** cơ bản.  
- Bật **MFA**, tạo **IAM user** làm việc hằng ngày và đặt **Budgets**.

---

### Kết hoạch thực hiện 
| Hạng mục | Kế hoạch | Thực tế | Trạng thái |
|---|---|---|---|
| Onboarding & nội quy | Giới thiệu, nắm kênh liên lạc | Đã giới thiệu, ghi chú chuẩn báo cáo | ✅ Done |
| AWS overview | Hệ thống nhóm dịch vụ + mindmap | Hoàn tất, có ghi chú theo nhóm | ✅ Done |
| Free Tier & bảo mật | Tạo account, bật MFA, tạo IAM user | Đã bật MFA; tạo user + group Viewer | ✅ Done |
| AWS CLI | Cài CLI, cấu hình profile | Profile `acj-student`, test `sts` OK | ✅ Done |
| EC2/EBS/SSH | Tạo EC2, SSH, attach EBS | EC2 t2.micro + EBS 8GB gp3, SSH ok | ✅ Done |
| Quản lý chi phí | Đặt Budgets 5 USD/tháng | Nhận email alert thử nghiệm | ✅ Done |

---

### Nhật ký theo ngày 
| Thứ | Nội dung công việc | Bắt đầu | Hoàn thành | Tài liệu/Link |
|---|---|---|---|---|
| 2 | Onboarding FCJ, đọc nội quy, chuẩn báo cáo | 08/09 | 08/09 | https://cloudjourney.awsstudygroup.com |
| 3 | Tìm hiểu AWS (Compute/Storage/Networking/DB/Security), tạo mindmap | 09/09 | 09/09 | https://cloudjourney.awsstudygroup.com |
| 4 | Tạo **AWS Free Tier**, bật **MFA** cho root, tạo **IAM user** + group Viewer | 10/09 | 10/09 | https://cloudjourney.awsstudygroup.com |
| 5 | Cài **AWS CLI v2** (Windows), `aws configure` profile `acj-student`, kiểm tra `sts` | 11/09 | 11/09 |https://cloudjourney.awsstudygroup.com |
| 6 | Học **EC2** (instance types, AMI, EBS, SG, Elastic IP) + checklist Free Tier | 12/09 | 12/09 | https://cloudjourney.awsstudygroup.com |
| 7 | Thực hành: tạo **EC2 t2.micro (Amazon Linux 2023)**, tạo & dùng **key pair (.pem)**, **SSH**; **attach EBS 8GB**, format & mount | 13/09 | 13/09 | https://cloudjourney.awsstudygroup.com |

---

### Kết quả & minh chứng
**Tài nguyên đã tạo**
- **IAM**: 01 user làm việc hằng ngày (Group: Viewer), **MFA** bật cho root.  
- **EC2**: t2.micro (Free Tier), AMI: Amazon Linux 2023, **Security Group** mở `22/tcp` từ **My IP**.  
- **EBS**: 8GB gp3, đã format (xfs) và mount vào `/data`.  
- **Budgets**: Monthly = **5 USD**, alert qua email.  
- **Region mặc định CLI**: `ap-southeast-1` (Singapore).  

**Lệnh CLI tiêu biểu**
```bash
aws sts get-caller-identity --profile acj-student
aws ec2 describe-regions --profile acj-student --output table
aws ec2 describe-instances --profile acj-student --region ap-southeast-1
aws ec2 create-key-pair --key-name fcj-key --query "KeyMaterial" --output text > fcj-key.pem
```

**Minh chứng đã lưu**
- Ảnh: trang **MFA enabled**, **IAM user & group**, **Budgets alert**, **EC2 instance detail**, **EBS volume** và mount point.

---

### Vấn đề và cách xử lý
| Vấn đề | Nguyên nhân | Cách xử lý | Kết quả |
|---|---|---|---|
| SSH thất bại lần đầu | SG chưa mở đúng IP | Cập nhật inbound rule → **My IP** | SSH OK |
| CLI báo thiếu credentials | Nhầm profile/region | Chuẩn hoá profile `acj-student`, set default region `ap-southeast-1` | CLI OK |
| Khó tìm dịch vụ trên Console | Chưa quen UI | Dùng ô Search + pin dịch vụ (EC2, IAM, S3, Budgets) | Điều hướng nhanh hơn |

---

### Kiến thức rút ra
- **Least-privilege**: dùng **IAM user/role**, tránh thao tác bằng root.  
- Quy trình chuẩn tạo EC2 Free Tier + **EBS attach/format/mount**.  
- Đồng bộ **Console ↔ CLI**, quản trị tài nguyên bằng **tag** (`Project=FCJ, Owner=The Liems, Env=Dev`).  
- Sử dụng **Budgets** để phòng tránh vượt chi phí.

---

### Chi phí & bảo mật
- **Budgets:** 5 USD/tháng (đã nhận email thử nghiệm).  
- **Bảo mật:** Bật **MFA**, lưu **.pem** an toàn, hạn chế **SSH** chỉ từ **My IP**.  
- **Tagging:** `Project=FCJ`, `Owner=The Liems`, `Env=Dev`.

---

### Rủi ro và biện pháp
- Rủi ro vượt Free Tier khi quên tắt tài nguyên → Đặt **Budgets** + review tags hằng tuần.  
- Bảo mật key pair/credentials → Lưu trữ an toàn, không commit lên git.


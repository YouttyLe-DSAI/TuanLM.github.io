---
title: "Worklog Tuần 9"
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---
# 📘 Báo cáo công việc Tuần 9 – AWS Journey 

## 1. Mục tiêu hàng tuần

Trong **Tuần 9**, trọng tâm mở rộng sang lĩnh vực **Dữ liệu & Phân tích (Data & Analytics)**. Mục tiêu chính là hiểu quy trình dữ liệu đầu cuối (end-to-end) trên AWS, từ thu thập đến trực quan hóa. Các mục tiêu chính bao gồm:

*   **Kiến trúc Data Lake** – Xây dựng kho lưu trữ có khả năng mở rộng bằng Amazon S3.
*   **ETL & Danh mục dữ liệu** – Sử dụng AWS Glue để khám phá và lập danh mục siêu dữ liệu (metadata).
*   **Truy vấn không máy chủ (Serverless Querying)** – Phân tích dữ liệu trực tiếp trong S3 bằng Amazon Athena (SQL).
*   **Trí tuệ doanh nghiệp (BI)** – Trực quan hóa thông tin chi tiết bằng Amazon QuickSight.

Tuần này trình bày cách biến dữ liệu thô thành thông tin kinh doanh hữu ích bằng các công cụ phân tích serverless.

---

## 2. Tóm tắt công việc chi tiết

### 🗂 Bảng hoạt động

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tham khảo |
| :--- | :--- | :--- | :--- | :--- |
| **Thứ Hai** | - Giới thiệu hệ sinh thái Data & Analytics trên AWS<br>- Hiểu khái niệm Data Lake, quy trình ETL và cách kết nối nguồn dữ liệu | 03/11/2025 | 03/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Ba** | - Tạo Data Lake trên Amazon S3<br>- Cấu trúc thư mục, quyền truy cập<br>- Thiết lập AWS Glue Crawler để xác định schema dữ liệu | 04/11/2025 | 04/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Tư** | - Thực hành AWS Athena để truy vấn dữ liệu trong Data Lake<br>- Viết câu lệnh SQL cơ bản và xuất kết quả ra S3 | 05/11/2025 | 05/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Năm** | - Giới thiệu và thực hành với Amazon QuickSight<br>- Kết nối QuickSight với Athena<br>- Tạo dashboard đơn giản với biểu đồ và bảng tổng hợp | 06/11/2025 | 06/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |
| **Thứ Sáu** | - Ôn tập & củng cố kiến thức tuần (Thu thập → xử lý → phân tích)<br>- So sánh Glue/Athena với công cụ truyền thống<br>- Viết báo cáo tổng kết thực hành | 07/11/2025 | 07/11/2025 | [AWS Journey](https://cloudjourney.awsstudygroup.com/) |

---

## 3. Chi tiết triển khai kỹ thuật

### 3.1 Thiết lập Data Lake (Amazon S3)
*   **Chiến lược lưu trữ:** Tạo S3 bucket với cấu trúc thư mục logic (ví dụ: `raw-data/`, `processed-data/`).
*   **Nhập dữ liệu:** Tải lên các tập dữ liệu mẫu (file CSV/JSON nhật ký bán hàng) vào thư mục `raw-data`.
*   **Bảo mật:** Áp dụng "Block Public Access" và đảm bảo IAM roles sẵn sàng cho Glue và Athena truy cập.

### 3.2 Khám phá Metadata (AWS Glue)
*   **Glue Crawler:** Cấu hình Crawler để quét S3 bucket.
*   **IAM Role:** Tạo service role cấp quyền cho Glue đọc S3 và ghi vào Glue Data Catalog.
*   **Data Catalog:** Chạy thành công crawler, tự động phát hiện schema (cột, kiểu dữ liệu) và tạo định nghĩa bảng trong Glue Database.

### 3.3 Truy vấn không máy chủ (Amazon Athena)
*   **Cấu hình:** Thiết lập vị trí lưu kết quả truy vấn trong S3 (`s3://my-bucket/athena-results/`).
*   **Thao tác SQL:** Thực thi các truy vấn SQL chuẩn trên bảng Glue:
    ```sql
    SELECT product_category, SUM(amount) as total_sales
    FROM sales_data
    GROUP BY product_category;
    ```
*   **Xác minh:** Xác nhận rằng Athena có thể truy vấn dữ liệu CSV trực tiếp mà không cần nạp vào máy chủ cơ sở dữ liệu.

### 3.4 Trực quan hóa dữ liệu (Amazon QuickSight)
*   **Tạo Dataset:** Chọn Athena làm nguồn dữ liệu và nhập bảng đã tạo ở các bước trước.
*   **SPICE:** Nhập dữ liệu vào bộ nhớ đệm SPICE để hiển thị nhanh hơn.
*   **Dashboarding:** Xây dựng bảng điều khiển chứa:
    *   **Biểu đồ cột:** Doanh số theo khu vực.
    *   **Biểu đồ tròn:** Nhân khẩu học khách hàng.
    *   **KPI:** Tổng doanh thu.

---

## 4. Thành tựu

Đến cuối Tuần 9, các kết quả sau đã đạt được:

### ✔ Thành công về mặt chức năng
*   Xây dựng thành công **Data Lake Serverless** sử dụng S3.
*   Tự động hóa việc khám phá cấu trúc dữ liệu bằng **AWS Glue Crawlers**.
*   Thực hiện phân tích SQL tùy ý bằng **Athena** mà không cần cấp phát máy chủ.
*   Tạo **BI Dashboard** trực quan trong QuickSight để trình bày thông tin chi tiết.

### ✔ Phát triển kỹ năng
*   Hiểu sự tách biệt giữa Tính toán (Athena) và Lưu trữ (S3).
*   Có kinh nghiệm với khái niệm **Schema-on-Read** so với Schema-on-Write truyền thống.
*   Học cách quản lý quyền IAM giữa các dịch vụ Phân tích (QuickSight <-> Athena <-> S3).

---

## 5. Thách thức gặp phải & Giải pháp

**Thách thức 1: Lỗi vị trí đầu ra Athena**
*   **Vấn đề:** Truy vấn thất bại với lỗi "No output location provided".
*   **Giải pháp:** Cấu hình "Query Result Location" trong cài đặt Athena trỏ đến một thư mục S3 hợp lệ.

**Thách thức 2: Quyền truy cập QuickSight**
*   **Vấn đề:** QuickSight không thể truy cập dữ liệu trong S3 bucket.
*   **Giải pháp:** Truy cập "Manage QuickSight" > "Security & Permissions" và tích chọn thủ công vào S3 bucket chứa dữ liệu.

**Thách thức 3: Phân loại sai của Glue Crawler**
*   **Vấn đề:** Crawler phân loại dữ liệu CSV không chính xác do vấn đề về tiêu đề (header).
*   **Giải pháp:** Chỉnh sửa trình phân loại tùy chỉnh (custom classifier) trong Glue để nhận diện đúng hàng tiêu đề CSV.

---


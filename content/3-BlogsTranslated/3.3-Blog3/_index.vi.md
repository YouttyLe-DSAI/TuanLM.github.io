---
title: "Blog 3"
weight: 1
chapter: false
pre: " <b> 3.3 </b> "
---
# **Melting The Ice \- Cách Natural Intelligence đơn giản hóa việc chuyển đổi Data lake sang Apache Iceberg**

bởi Yonatan Dolan và Haya Axelrod Stern, Zion Rubin, Michal Urbanowicz vào 28 tháng 4 năm 2025 trong [Advanced (300)](https://aws.amazon.com/blogs/big-data/category/learning-levels/advanced-300/), [Analytics](https://aws.amazon.com/blogs/big-data/category/analytics/), [AWS Glue](https://aws.amazon.com/blogs/big-data/category/analytics/aws-glue/), [Best Practices](https://aws.amazon.com/blogs/big-data/category/post-types/best-practices/), [Case Study](https://aws.amazon.com/blogs/big-data/category/case-study/), [Technical How-to](https://aws.amazon.com/blogs/big-data/category/post-types/technical-how-to/) [Permalink](https://aws.amazon.com/blogs/big-data/melting-the-ice-how-natural-intelligence-simplified-a-data-lake-migration-to-apache-iceberg/)

*Bài viết này được đồng tác giả bởi Haya Axelrod Stern, Zion Rubin và Michal Urbanowicz từ Natural Intelligence..*

Nhiều tổ chức chọn data lake vì tính linh hoạt và khả năng mở rộng trong việc quản lý dữ liệu có cấu trúc và không cấu trúc. Tuy nhiên, việc di chuyển một data lake hiện hữu sang định dạng bảng mới như Apache Iceberg có thể gặp nhiều thách thức về kỹ thuật lẫn tổ chức.	

[Natural Intelligence (NI)](https://www.naturalint.com/) là một đơn vị hàng đầu trong lĩnh vực thị trường đa danh mục. Với các thương hiệu nổi bật như [Top10.com](http://Top10.com) và [BestMoney.com](http://BestMoney.com), NI hỗ trợ hàng triệu người mỗi ngày trong việc đưa ra quyết định thông minh. Gần đây, NI đã khởi động hành trình chuyển đổi data lake truyền thống từ Apache Hive sang Apache Iceberg.

Trong bài viết này, NI chia sẻ hành trình của họ, các giải pháp sáng tạo đã phát triển, và những bài học chính có thể hướng dẫn các tổ chức khác muốn thực hiện con đường tương tự. Nội dung tập trung nhiều vào thách thức thực tế và cách giải quyết trong quá trình chuyển đổi, hơn là các đặc tả kỹ thuật phức tạp của Apache Iceberg.

### **Tại sao chọn Apache Iceberg?**

Kiến trúc dữ liệu tại **NI** tuân theo mô hình **Medallion Architecture** (kiến trúc phân tầng đồng – bạc – vàng), được mô tả như sau:

* **Lớp Đồng (Bronze layer):**  
   Dữ liệu thô chưa qua xử lý được thu thập từ nhiều nguồn khác nhau, lưu trữ ở định dạng gốc trong [**Amazon Simple Storage Service (Amazon S3**](https://aws.amazon.com/pm/serv-s3/)**)** và được nạp thông qua **Apache Kafka brokers**.

* **Lớp Bạc (Silver layer):**  
   Chứa dữ liệu đã được làm sạch và làm giàu (enriched data), được xử lý bằng **Apache Flink**.

* **Lớp Vàng (Gold layer):**  
   Lưu trữ các tập dữ liệu sẵn sàng cho phân tích (analytics-ready datasets) được thiết kế cho **Business Intelligence (BI)** và **báo cáo**.  
   Dữ liệu ở lớp này được tạo ra thông qua các pipeline **Apache Spark** và được sử dụng bởi các dịch vụ như **Snowflake**, [**Amazon Athena**](https://aws.amazon.com/athena/), **Tableau**, và **Apache Druid**.  
   Dữ liệu được lưu ở định dạng **Apache Parquet**, với [**AWS Glue Catalog**](https://docs.aws.amazon.com/prescriptive-guidance/latest/serverless-etl-aws-glue/aws-glue-data-catalog.html) chịu trách nhiệm quản lý siêu dữ liệu (metadata management).

![](/images/3-BlogsTranslated/BDB4681-Arch1.jpg)

Mặc dù kiến trúc này đáp ứng được các nhu cầu phân tích dữ liệu của NI, nhưng nó thiếu tính linh hoạt cần thiết cho một nền tảng dữ liệu mở và có khả năng thích ứng thực sự.Lớp Gold chỉ có thể hoạt động với các công cụ truy vấn (query engines) hỗ trợ Hive và AWS Glue Data Catalog. Dù có thể sử dụng Amazon Athena, nhưng với Snowflake, NI phải duy trì một catalog riêng biệt để có thể truy vấn các bảng external (ngoại bảng). Vấn đề này khiến cho việc đánh giá hoặc áp dụng các công cụ và engine thay thế trở nên khó khăn — nếu không muốn nhân bản dữ liệu, viết lại truy vấn, hoặc đồng bộ lại catalog tốn kém chi phí. Khi quy mô kinh doanh mở rộng, NI cần một nền tảng dữ liệu có thể hỗ trợ đồng thời nhiều công cụ truy vấn khác nhau chỉ với một data catalog duy nhất, đồng thời tránh bị phụ thuộc vào bất kỳ nhà cung cấp nào (vendor lock-in).

### **Sức mạnh của Apache Iceberg**

Apache Iceberg nổi lên như một giải pháp hoàn hảo — một định dạng bảng mở, linh hoạt phù hợp với cách tiếp cận *Data Lake First* của NI. Iceberg cung cấp một số lợi thế quan trọng như giao dịch ACID, phát triển lược đồ, du hành thời gian, cải thiện hiệu suất và hơn thế nữa. Nhưng lợi ích chiến lược chính nằm ở khả năng hỗ trợ nhiều công cụ truy vấn đồng thời. Nó cũng có những ưu điểm sau:

* **Tách biệt giữa lưu trữ và xử lý (Decoupling of storage and compute):** Định dạng bảng mở cho phép bạn tách lớp lưu trữ khỏi công cụ truy vấn, cho phép dễ dàng hoán đổi và hỗ trợ đồng thời nhiều công cụ mà không trùng lặp dữ liệu.

* **Độc lập với nhà cung cấp (Vendor independence) :** Là một định dạng bảng mở, Apache Iceberg ngăn chặn khóa nhà cung cấp, giúp bạn linh hoạt thích ứng với nhu cầu phân tích thay đổi.

* **Được nhiều nền tảng hỗ trợ (Vendor adoption)**: Apache Iceberg được hỗ trợ rộng rãi bởi các nền tảng và công cụ chính, cung cấp khả năng tích hợp liền mạch và khả năng tương thích lâu dài với hệ sinh thái.

Bằng cách chuyển đổi sang Iceberg, NI đã có thể nắm bắt một nền tảng dữ liệu mở thực sự, cung cấp tính linh hoạt lâu dài, khả năng mở rộng và khả năng tương tác trong khi vẫn duy trì một nguồn tin cậy thống nhất cho tất cả các nhu cầu phân tích và báo cáo.

## **Những thách thức phải đối mặt**

Việc di chuyển hồ dữ liệu sản xuất trực tiếp sang Iceberg là một thách thức vì sự phức tạp trong hoạt động và các hạn chế kế thừa. Dịch vụ dữ liệu tại NI chạy hàng trăm quy trình Spark và machine learning, quản lý hàng nghìn bảng và hỗ trợ hơn 400 bảng thông tin—tất cả đều hoạt động 24/7. Bất kỳ quá trình di chuyển nào cũng cần được thực hiện mà không bị gián đoạn sản xuất; và việc điều phối một cuộc di cư như vậy trong khi các hoạt động tiếp tục liền mạch là điều khó khăn.

NI cần đáp ứng những người dùng đa dạng với các yêu cầu và thời gian khác nhau từ kỹ sư dữ liệu đến nhà phân tích dữ liệu cho đến các nhà khoa học dữ liệu và nhóm BI.

Thêm vào thách thức là những hạn chế kế thừa. Một số công cụ hiện có không hỗ trợ đầy đủ Iceberg, vì vậy cần phải duy trì các bảng được hỗ trợ bởi Hive để tương thích. Khi NI nhận ra rằng không phải tất cả người tiêu dùng đều có thể chấp nhận Iceberg ngay lập tức. Cần có một kế hoạch để cho phép chuyển đổi gia tăng mà không có thời gian ngừng hoạt động hoặc gián đoạn các hoạt động đang diễn ra.

### **Các thành phần chính cho quá trình di chuyển**

Để đảm bảo quá trình **chuyển đổi diễn ra suôn sẻ và thành công**, **sáu thành phần quan trọng** đã được xác định như sau:

* **Duy trì hoạt động liên tục (Support ongoing operations):**  
   Đảm bảo khả năng tương thích không bị gián đoạn với các hệ thống và quy trình hiện có trong suốt quá trình di chuyển.

* **Tính minh bạch với người dùng (User transparency):**  
   Giảm thiểu gián đoạn cho người dùng bằng cách **giữ nguyên tên bảng và cách truy cập** như cũ.  
  **Chuyển đổi người dùng dần dần (Gradual consumer migration):**  
   Cho phép người dùng chuyển sang **Iceberg theo tiến độ riêng**, tránh việc phải chuyển đổi đồng loạt cùng lúc.

* **Tính linh hoạt trong ETL (ETL flexibility):**  
   Cho phép **chuyển các pipeline ETL sang Iceberg** mà không áp đặt các ràng buộc trong quá trình **phát triển hoặc triển khai**.

* **Hiệu quả chi phí (Cost effectiveness):**  
   Giảm thiểu **nhân bản dữ liệu lưu trữ và xử lý**, cũng như **chi phí phát sinh** trong giai đoạn chuyển đổi.

* **Giảm thiểu bảo trì (Minimize maintenance):**  
   Giảm gánh nặng vận hành trong việc **duy trì song song hai định dạng bảng (Hive và Iceberg)** trong quá trình chuyển đổi.

### **Đánh giá các phương pháp di chuyển truyền thống**

**Apache Iceberg** hỗ trợ hai phương pháp chính để di chuyển dữ liệu **In-place migration (Chuyển đổi trực tiếp) và Rewrite-based migration (Chuyển đổi bằng cách ghi lại dữ liệu).**

**Chuyển đổi trực tiếp (In-place migration)**

**Cách hoạt động:** Phương pháp này chuyển đổi bộ dữ liệu hiện có sang bảng Iceberg mà không cần nhân bản dữ liệu, bằng cách tạo metadata của Iceberg dựa trên các tệp dữ liệu hiện có, đồng thời giữ nguyên bố cục và định dạng ban đầu.

**Ưu điểm:**

* Tiết kiệm chi phí lưu trữ, vì không có sự nhân bản dữ liệu.

* Dễ triển khai, quá trình thực hiện đơn giản.

* Giữ nguyên tên và vị trí bảng hiện tại, giúp người dùng không phải thay đổi truy cập.

* Không cần di chuyển dữ liệu, yêu cầu tính toán tối thiểu → chi phí thấp hơn.

**Nhược điểm:**

* Cần downtime: Tất cả các thao tác ghi phải tạm dừng trong khi chuyển đổi, điều này không thể chấp nhận được với NI, vì các quy trình dữ liệu và phân tích rất quan trọng và vận hành 24/7.

* Không thể chuyển đổi dần dần: Tất cả người dùng phải chuyển sang Iceberg cùng lúc, làm tăng nguy cơ gián đoạn hệ thống.

* Giới hạn xác thực: Không có cơ hội kiểm tra tính đúng đắn của dữ liệu trước khi hoàn tất chuyển đổi; nếu có lỗi, cần phục hồi từ bản sao lưu.

* Hạn chế kỹ thuật: Việc tiến hóa schema trong quá trình chuyển đổi có thể khó khăn; xung đột kiểu dữ liệu có thể khiến toàn bộ quy trình thất bại.

#### **Rewrite-based migration (Chuyển đổi bằng cách ghi lại dữ liệu)**

**Cách hoạt động:** Phương pháp này tạo một bảng Iceberg mới bằng cách viết lại và tái tổ chức các tệp dữ liệu hiện có theo định dạng và cấu trúc tối ưu của Iceberg, giúp cải thiện hiệu năng và quản lý dữ liệu.

**Ưu điểm:**

* Không cần downtime trong suốt quá trình di chuyển.

* Hỗ trợ chuyển đổi người dùng dần dần, cho phép từng nhóm áp dụng Iceberg theo nhịp riêng.

* Cho phép xác thực dữ liệu kỹ lưỡng trước khi chuyển đổi hoàn toàn.

* Cơ chế rollback đơn giản, có thể dễ dàng quay lại nếu có lỗi.

**Nhược điểm:**

* Tăng chi phí tài nguyên: Cần gấp đôi dung lượng lưu trữ và công suất xử lý trong thời gian di chuyển.

* Phức tạp trong bảo trì: Cần duy trì hai pipeline dữ liệu song song, tăng gánh nặng vận hành.

* Thách thức về tính nhất quán: Khó đảm bảo hai hệ thống luôn đồng bộ hoàn toàn trong thời gian chuyển đổi.

* Ảnh hưởng đến hiệu năng: Ghi dữ liệu song song (dual writes) có thể tăng độ trễ và làm chậm pipeline.

### **Tại sao không phương án nào là đủ tốt**

NI nhận thấy rằng cả hai phương pháp (In-place và Rewrite-based) đều không thể đáp ứng đầy đủ các yêu cầu quan trọng:

* In-place migration không phù hợp vì yêu cầu downtime (ngừng hoạt động) là không thể chấp nhận được, và không hỗ trợ quá trình chuyển đổi dần dần.

* Rewrite-based migration lại tốn kém chi phí và phức tạp trong quản lý vận hành do phải duy trì hai pipeline song song.

Từ những phân tích đó, NI đã phát triển một giải pháp lai (hybrid approach) — kết hợp ưu điểm của cả hai phương pháp, đồng thời giảm thiểu và khắc phục các hạn chế của chúng.

### **Giải pháp Hybrid**

Chiến lược di chuyển lai được **thiết kế dựa trên 5 thành phần cốt lõi**, tận dụng **các dịch vụ phân tích của AWS** để điều phối, xử lý và quản lý trạng thái.

#### **1\. Hive-to-Iceberg CDC (Đồng bộ thay đổi từ Hive sang Iceberg):** Hệ thống tự động đồng bộ các bảng Hive sang Iceberg bằng quy trình CDC (Change Data Capture) tùy chỉnh để hỗ trợ người dùng hiện có. Không giống CDC truyền thống theo mức hàng (row-level), NI áp dụng CDC ở mức phân vùng (partition-level) — vì Hive thường cập nhật dữ liệu bằng cách ghi đè (overwrite) toàn bộ phân vùng. Cách này giúp duy trì tính nhất quán dữ liệu giữa Hive và Iceberg mà không cần thay đổi logic ghi dữ liệu, đảm bảo rằng hai bảng chứa cùng dữ liệu trong giai đoạn di chuyển.

#### **2\. Continuous schema synchronization (Đồng bộ lược đồ liên tục):** Trong quá trình di chuyển, việc tiến hóa schema (schema evolution) gây ra nhiều thách thức trong bảo trì. NI triển khai quy trình đồng bộ lược đồ tự động, so sánh schema giữa Hive và Iceberg, và điều chỉnh sự khác biệt trong khi vẫn giữ tương thích kiểu dữ liệu (type compatibility).

#### **3\. Iceberg-to-Hive reverse CDC (Đồng bộ ngược từ Iceberg sang Hive):** Cho phép nhóm dữ liệu chuyển các job ETL (Extract, Transform, Load) để ghi trực tiếp vào Iceberg, đồng thời vẫn duy trì tính tương thích với các quy trình cũ dùng Hive. Reverse CDC giúp tự động cập nhật dữ liệu từ Iceberg ngược trở lại Hive, đảm bảo các pipeline downstream (phía sau) chưa di chuyển vẫn hoạt động bình thường. Nhờ đó, hệ thống có thể chuyển đổi dần dần, không làm gián đoạn quy trình hiện có.

#### **4\. Alias management in Snowflake (Quản lý bí danh trong Snowflake):** Sử dụng alias (bí danh) trong Snowflake để đảm bảo rằng các bảng Iceberg giữ nguyên tên gốc, giúp quá trình chuyển đổi trở nên trong suốt (transparent) đối với người dùng. Cách này giúp giảm thiểu việc cấu hình lại trên các nhóm phụ thuộc và các workflow hiện có.

#### **5\. Table replacement (Thay thế bảng sản xuất):** Sau khi toàn bộ hệ thống đã chuyển sang Iceberg, NI hoán đổi (swap) các bảng sản xuất, giữ nguyên tên bảng ban đầu, và hoàn tất quá trình di chuyển.

## **Tìm hiểu sâu về kỹ thuật**

Quá trình di chuyển từ Hive đến Iceberg được xây dựng từ một số bước:

### **1\. Sơ đồ Hive-to-Iceberg CDC:**

**Mục tiêu:** Giữ cho bảng Hive và Iceberg được đồng bộ hóa mà không cần nỗ lực trùng lặp.

![](/images/3-BlogsTranslated/BDB4681-arch2.jpg)

Hình trước cho thấy cách mọi phân vùng được ghi vào bảng Hive được sao chép tự động và minh bạch vào bảng Iceberg bằng cách sử dụng quy trình CDC. Quá trình này đảm bảo rằng cả hai bảng đều được đồng bộ hóa, cho phép di chuyển liền mạch và gia tăng mà không làm gián đoạn hệ thống xuôi dòng. NI đã chọn đồng bộ hóa cấp phân vùng vì các công việc Hive ETL cũ đã ghi các bản cập nhật bằng cách ghi đè lên toàn bộ phân vùng và cập nhật vị trí phân vùng. Việc áp dụng cách tiếp cận tương tự trong quy trình CDC đã giúp đảm bảo rằng nó vẫn nhất quán với cách dữ liệu được quản lý ban đầu, giúp quá trình di chuyển suôn sẻ hơn và tránh phải làm lại logic cấp hàng.

Thực hiện:

* Để giữ cho bảng Hive và Iceberg được đồng bộ hóa mà không cần nỗ lực trùng lặp, một quy trình hợp lý đã được triển khai. Bất cứ khi nào các phân vùng trong bảng Hive được cập nhật, AWS Glue Catalog sẽ phát ra các sự kiện như . [Amazon EventBridge](https://aws.amazon.com/eventbridge/) đã nắm bắt các sự kiện này, lọc chúng cho các cơ sở dữ liệu và bảng có liên quan theo quy tắc cầu nối sự kiện, đồng thời kích hoạt [AWS Lambda](https://aws.amazon.com/lambda) Hàm này phân tích siêu dữ liệu sự kiện và gửi các bản cập nhật phân vùng đến chủ đề Apache Kafka.UpdatePartition

* Một tác vụ Spark chạy trên [Amazon EMR](https://aws.amazon.com/emr/) đã sử dụng các tin nhắn từ Kafka, chứa các chi tiết phân vùng được cập nhật từ các sự kiện Danh mục dữ liệu. Sử dụng siêu dữ liệu sự kiện đó, tác vụ Spark truy vấn bảng Hive có liên quan và ghi vào bảng Iceberg trong Amazon S3 bằng API Spark Iceberg, như được hiển thị trong ví dụ sau:overwritePartitions

{

    "id": "10397e54-c049-fc7b-76c8-59e148c7cbfc",

    "detail-type": "Glue Data Catalog Table State Change",

    "source": "aws.glue",

    "time": "2024-10-27T17:16:21Z",

    "region": "us-east-1",

    "detail": {

      "databaseName": "dlk\_visitor\_funnel\_dwh\_production",

      "changedPartitions": \[

        "2024-10-27"

      \],

      "typeOfChange": "UpdatePartition",

      "tableName": "fact\_events"

    }

}

* Bằng cách chỉ nhắm mục tiêu các phân vùng đã sửa đổi, quy trình (được hiển thị trong hình sau) đã giảm đáng kể nhu cầu viết lại toàn bảng tốn kém. Các lớp siêu dữ liệu mạnh mẽ của Iceberg, bao gồm ảnh chụp nhanh và tệp kê khai, đã được cập nhật liền mạch để nắm bắt những thay đổi này, cung cấp đồng bộ hóa hiệu quả và chính xác giữa bảng Hive và Iceberg.

### **2\. Sơ đồ ceberg-to-Hive reverse CDC**

**Mục tiêu:** Hỗ trợ khách hàng Hive đồng thời cho phép các quy trình ETL chuyển sang Iceberg.

![](/images/3-BlogsTranslated/BDB4681-arch4.jpg)

Hình trước cho thấy quá trình ngược lại, trong đó mọi phân vùng được ghi vào bảng Iceberg được sao chép tự động và minh bạch vào bảng Hive bằng cơ chế CDC. Quá trình này giúp đảm bảo đồng bộ hóa giữa hai hệ thống, cho phép cập nhật dữ liệu liền mạch cho các hệ thống cũ vẫn dựa vào Hive trong khi chuyển sang Iceberg.

**Thực hiện:**

Đồng bộ hóa dữ liệu từ bảng Iceberg trở lại bảng Hive đưa ra một thách thức khác. Không giống như bảng Hive, Danh mục dữ liệu không theo dõi các bản cập nhật phân vùng cho bảng Iceberg vì các phân vùng trong Iceberg được quản lý nội bộ chứ không phải trong danh mục. Điều này có nghĩa là NI không thể dựa vào các sự kiện Glue Catalog để phát hiện các thay đổi phân vùng.

Để giải quyết vấn đề này, NI đã triển khai một giải pháp tương tự như quy trình trước đó nhưng thích ứng với kiến trúc của Iceberg. Apache Spark được sử dụng để truy vấn các bảng siêu dữ liệu của Iceberg \- cụ thể là các bảng ảnh chụp nhanh và mục nhập \- để xác định các phân vùng được sửa đổi kể từ lần đồng bộ hóa cuối cùng. Truy vấn được sử dụng là:

SELECT e.data\_file.partition, MAX(s.committed\_at) AS last\_modified\_time 

FROM $target\_table.snapshots JOIN $target\_table.entries e ON s.snapshot\_id \= e.snapshot\_id 

WHERE s.committed\_at &amp;gt; '$last\_sync\_time' 

GROUP BY e.data\_file.partition;

Truy vấn này chỉ trả về các phân vùng đã được cập nhật kể từ lần đồng bộ hóa cuối cùng, cho phép nó tập trung hoàn toàn vào dữ liệu đã thay đổi. Sử dụng thông tin này, tương tự như quy trình trước đó, một công việc Spark đã truy xuất các phân vùng được cập nhật từ Iceberg và ghi chúng trở lại bảng Hive tương ứng, cung cấp sự đồng bộ hóa liền mạch giữa cả hai bảng.

### **3\. Đồng bộ hóa lược đồ liên tục**

**Mục tiêu:** tự động cập nhật lược đồ để duy trì tính nhất quán trên Hive và Iceberg.

**![](/images/3-BlogsTranslated/BDB4681-arch5.jpg)**

Hình trước cho thấy quy trình đồng bộ hóa lược đồ tự động giúp đảm bảo tính nhất quán giữa lược đồ bảng Hive và Iceberg bằng cách tự động đồng bộ hóa các thay đổi lược đồ. Trong ví dụ này, thêm cột, giảm thiểu công việc thủ công và bảo trì kép trong thời gian di chuyển kéo dài.Channel

 **Thực hiện:**

Để xử lý các thay đổi lược đồ giữa Hive và Iceberg, một quy trình đã được thực hiện để phát hiện và đối chiếu sự khác biệt một cách tự động. Khi thay đổi lược đồ xảy ra trong bảng Hive, Danh mục dữ liệu sẽ phát ra một sự kiện. Sự kiện này kích hoạt hàm Lambda (được định tuyến qua EventBridge), hàm này truy xuất lược đồ cập nhật từ Danh mục dữ liệu cho bảng Hive và so sánh với lược đồ Iceberg. Điều quan trọng cần lưu ý là trong thiết lập của NI, các thay đổi lược đồ bắt nguồn từ Hive vì bảng Iceberg được ẩn đằng sau các bí danh trên toàn hệ thống. Bởi vì Iceberg chủ yếu được sử dụng cho Snowflake, đồng bộ hóa một chiều từ Hive đến Iceberg là đủ. Do đó, không có cơ chế để phát hiện hoặc xử lý các thay đổi lược đồ được thực hiện trực tiếp trong Iceberg, vì chúng không cần thiết trong quy trình làm việc hiện tại.UpdateTable

Trong quá trình đối chiếu lược đồ (hiển thị trong hình sau), các kiểu dữ liệu được chuẩn hóa để giúp đảm bảo khả năng tương thích — ví dụ: chuyển đổi Hive sang Iceberg . Mọi trường hoặc thay đổi loại mới đều được xác thực và áp dụng cho lược đồ Iceberg bằng cách sử dụng tác vụ Spark chạy trên Amazon EMR. [Amazon DynamoDB](https://aws.amazon.com/dynamodb/) lưu trữ các điểm kiểm tra đồng bộ hóa lược đồ cho phép theo dõi các thay đổi theo thời gian và duy trì tính nhất quán giữa lược đồ Hive và Iceberg.VARCHARSTRING

Trong ví dụ này, thêm cột, giảm thiểu công việc thủ công và bảo trì kép trong thời gian di chuyển kéo dài.Channel

 Thực hiện:

Để xử lý các thay đổi lược đồ giữa Hive và Iceberg, một quy trình đã được thực hiện để phát hiện và đối chiếu sự khác biệt một cách tự động. Khi thay đổi lược đồ xảy ra trong bảng Hive, Danh mục dữ liệu sẽ phát ra một sự kiện. Sự kiện này kích hoạt hàm Lambda (được định tuyến qua EventBridge), hàm này truy xuất lược đồ cập nhật từ Danh mục dữ liệu cho bảng Hive và so sánh với lược đồ Iceberg. Điều quan trọng cần lưu ý là trong thiết lập của NI, các thay đổi lược đồ bắt nguồn từ Hive vì bảng Iceberg được ẩn đằng sau các bí danh trên toàn hệ thống. Bởi vì Iceberg chủ yếu được sử dụng cho Snowflake, đồng bộ hóa một chiều từ Hive đến Iceberg là đủ. Do đó, không có cơ chế để phát hiện hoặc xử lý các thay đổi lược đồ được thực hiện trực tiếp trong Iceberg, vì chúng không cần thiết trong quy trình làm việc hiện tại.UpdateTable

Trong quá trình đối chiếu lược đồ (hiển thị trong hình sau), các kiểu dữ liệu được chuẩn hóa để giúp đảm bảo khả năng tương thích — ví dụ: chuyển đổi Hive sang Iceberg . Mọi trường hoặc thay đổi loại mới đều được xác thực và áp dụng cho lược đồ Iceberg bằng cách sử dụng tác vụ Spark chạy trên Amazon EMR. [Amazon DynamoDB](https://aws.amazon.com/dynamodb/) lưu trữ các điểm kiểm tra đồng bộ hóa lược đồ cho phép theo dõi các thay đổi theo thời gian và duy trì tính nhất quán giữa lược đồ Hive và Iceberg.VARCHARSTRING

**![](/images/3-BlogsTranslated/BDB4681-arch6.jpg)**

Bằng cách tự động hóa đồng bộ hóa lược đồ này, chi phí bảo trì đã giảm đáng kể và giải phóng các nhà phát triển khỏi việc đồng bộ hóa lược đồ theo cách thủ công, làm cho thời gian di chuyển dài dễ quản lý hơn đáng kể.

![](/images/3-BlogsTranslated/BDB4681-arch7.jpg)

Hình trước mô tả quy trình làm việc tự động để duy trì tính nhất quán lược đồ giữa bảng Hive và Iceberg. AWS Glue ghi lại các sự kiện thay đổi trạng thái bảng từ Hive, kích hoạt sự kiện EventBridge. Sự kiện này gọi một hàm [Lambda](https://aws.amazon.com/pm/lambda/) tìm nạp siêu dữ liệu từ DynamoDB và so sánh các lược đồ được tìm nạp từ AWS Glue cho cả bảng Hive và Iceberg. Nếu phát hiện sự không khớp, lược đồ trong Iceberg sẽ được cập nhật để giúp đảm bảo căn chỉnh, giảm thiểu sự can thiệp thủ công và hỗ trợ hoạt động trơn tru trong quá trình di chuyển.

### **4\. Quản lý bí danh trong Snowflake**

**Mục tiêu:** Cho phép người tiêu dùng Snowflake áp dụng Iceberg mà không cần thay đổi tham chiếu truy vấn.

![](/images/3-BlogsTranslated/BDB4681-arch75.jpg)

Hình trước cho thấy bí danh Snowflake cho phép di chuyển liền mạch bằng cách ánh xạ các truy vấn như bảng Iceberg trong Glue Catalog. Ngay cả khi có thêm hậu tố trong quá trình di chuyển Iceberg, các truy vấn và quy trình làm việc hiện có vẫn không thay đổi, giảm thiểu sự gián đoạn cho các công cụ BI và nhà phân tích.SELECT platform, COUNT(clickouts) FROM funnel.clickouts

**Thực hiện:**

Để giúp đảm bảo trải nghiệm liền mạch cho các công cụ BI và nhà phân tích trong quá trình di chuyển, bí danh Snowflake đã được sử dụng để ánh xạ các bảng bên ngoài với siêu dữ liệu Iceberg được lưu trữ trong Danh mục dữ liệu. Bằng cách gán các bí danh khớp với tên bảng Hive ban đầu, các truy vấn và báo cáo hiện có đã được giữ nguyên mà không bị gián đoạn. Ví dụ: một bảng bên ngoài đã được tạo trong Snowflake và đặt bí danh thành tên bảng ban đầu, như được hiển thị trong truy vấn sau:



    CREATE OR REPLACE ICEBERG TABLE dlk\_visitor\_funnel\_dwh\_production.aggregated\_cost 

    EXTERNAL\_VOLUME \= 's3\_dlk\_visitor\_funnel\_dwh\_production\_iceberg\_migration' 

    CATALOG \= 'glue\_dlk\_visitor\_funnel\_dwh\_production\_iceberg\_migration' 

    CATALOG\_TABLE\_NAME \= 'aggregated\_cost'; 

    ALTER ICEBERG TABLE dlk\_visitor\_funnel\_dwh\_production.aggregated\_cost REFRESH;


Khi quá trình di chuyển hoàn tất, một thay đổi đơn giản trở lại bí danh đã được thực hiện để trỏ đến vị trí hoặc lược đồ mới, giúp quá trình chuyển đổi trở nên liền mạch và giảm thiểu bất kỳ sự gián đoạn nào đối với quy trình làm việc của người dùng.

### **5\. Thay thế bàn**

**Mục tiêu:** Khi tất cả các ETL và quy trình dữ liệu liên quan được chuyển đổi thành công để sử dụng các khả năng của Apache Iceberg và mọi thứ hoạt động chính xác với luồng đồng bộ hóa, đã đến lúc chuyển sang giai đoạn cuối cùng của quá trình di chuyển. Mục tiêu chính là duy trì tên bảng ban đầu, tránh sử dụng bất kỳ tiền tố nào như những tiền tố được sử dụng trong các bước di chuyển trung gian trước đó. Điều này giúp đảm bảo rằng cấu hình vẫn gọn gàng và không có phức tạp đặt tên không cần thiết.

![](/images/3-BlogsTranslated/BDB4681-arch8.jpg)

Hình trước cho thấy việc thay thế bảng để hoàn tất quá trình di chuyển, trong đó Hive trên Amazon EMR được sử dụng để đăng ký các tệp Parquet dưới dạng bảng Iceberg trong khi vẫn giữ nguyên tên bảng ban đầu và tránh trùng lặp dữ liệu, giúp đảm bảo di chuyển liền mạch và gọn gàng.

**Thực hiện:**

Một trong những thách thức là không thể đổi tên bảng trong AWS Glue, điều này ngăn cản việc sử dụng phương pháp đổi tên đơn giản cho các bảng luồng đồng bộ hóa hiện có. Ngoài ra, AWS Glue không hỗ trợ quy trình này tạo siêu dữ liệu Iceberg trên tệp dữ liệu hiện có trong khi vẫn giữ nguyên tên bảng ban đầu. Chiến lược để khắc phục hạn chế này là sử dụng metastore Hive trên cụm Amazon EMR. Bằng cách sử dụng Hive trên Amazon EMR, NI có thể tạo các bảng cuối cùng với tên ban đầu của chúng vì nó hoạt động trong một môi trường metastore riêng biệt, mang lại sự linh hoạt để xác định mọi lược đồ và tên bảng bắt buộc mà không bị can thiệp.Migrate

Quy trình này được sử dụng để đăng ký một cách có phương pháp tất cả các tệp Parquet hiện có, do đó xây dựng tất cả siêu dữ liệu cần thiết trong Hive. Đây là một bước quan trọng, vì nó giúp đảm bảo rằng tất cả các tệp dữ liệu được lập danh mục và liên kết một cách thích hợp trong metastore.add\_files

![](/images/3-BlogsTranslated/BDB4681-arch9.jpg)

Hình trước cho thấy sự chuyển đổi của bảng sản xuất sang Iceberg bằng cách sử dụng thủ tục để đăng ký các tệp Parquet hiện có và tạo siêu dữ liệu Iceberg. Điều này giúp đảm bảo quá trình di chuyển suôn sẻ trong khi vẫn giữ nguyên dữ liệu gốc và tránh trùng lặp.add\_files

Thiết lập này cho phép sử dụng các tệp Parquet hiện có mà không sao chép dữ liệu, do đó tiết kiệm tài nguyên. Mặc dù luồng đồng bộ hóa sử dụng các vùng lưu trữ riêng biệt cho kiến trúc cuối cùng, NI đã chọn duy trì các vùng lưu trữ ban đầu và dọn dẹp các tệp trung gian. Điều này dẫn đến cấu trúc thư mục khác trên Amazon S3. Dữ liệu lịch sử có các thư mục con cho mỗi phân vùng trong thư mục bảng gốc, trong khi dữ liệu Iceberg mới tổ chức các thư mục con trong thư mục *dữ liệu*. Sự khác biệt này có thể chấp nhận được để tránh trùng lặp dữ liệu và giữ nguyên các vùng lưu trữ Amazon S3 ban đầu.

## **Tóm tắt kỹ thuật**

Danh mục dữ liệu AWS Glue đóng vai trò là nguồn tin cậy chính cho các bản cập nhật lược đồ và bảng, với Amazon EventBridge ghi lại các sự kiện Danh mục dữ liệu để kích hoạt quy trình đồng bộ hóa. AWS Lambda phân tích siêu dữ liệu sự kiện và đồng bộ hóa lược đồ được quản lý, trong khi Apache Kafka đệm các sự kiện để xử lý theo thời gian thực. Apache Spark trên Amazon EMR xử lý chuyển đổi dữ liệu và cập nhật gia tăng, đồng thời Amazon DynamoDB duy trì trạng thái, bao gồm các điểm kiểm tra đồng bộ hóa và ánh xạ bảng. Cuối cùng, Snowflake sử dụng liền mạch các bảng Iceberg thông qua bí danh mà không làm gián đoạn quy trình làm việc hiện có.

## **Kết quả di chuyển**

Quá trình di chuyển đã được hoàn thành mà không có thời gian chết; Các hoạt động liên tục được duy trì trong suốt quá trình di chuyển, hỗ trợ hàng trăm đường ống và bảng điều khiển mà không bị gián đoạn. Quá trình di chuyển được thực hiện với tư duy tối ưu hóa chi phí với các bản cập nhật gia tăng và đồng bộ hóa cấp phân vùng giúp giảm thiểu việc sử dụng tài nguyên điện toán và lưu trữ. Cuối cùng, NI đã thiết lập một nền tảng hiện đại, trung lập với nhà cung cấp cho phép mở rộng nhu cầu phân tích và học máy đang phát triển của họ. Nó cho phép tích hợp liền mạch với nhiều công cụ điện toán và truy vấn, hỗ trợ tính linh hoạt và đổi mới hơn nữa.

## **Kết thúc**

Chuyển đổi trí tuệ tự nhiên sang Apache Iceberg là một bước quan trọng trong việc hiện đại hóa cơ sở hạ tầng dữ liệu của công ty. Bằng cách áp dụng chiến lược kết hợp và sử dụng sức mạnh của kiến trúc theo hướng sự kiện, NI đã giúp đảm bảo quá trình chuyển đổi liền mạch cân bằng giữa đổi mới với sự ổn định trong hoạt động. Hành trình nhấn mạnh tầm quan trọng của việc lập kế hoạch cẩn thận, hiểu hệ sinh thái dữ liệu và tập trung vào cách tiếp cận ưu tiên tổ chức.

Trên hết, hoạt động kinh doanh được tập trung và tính liên tục ưu tiên trải nghiệm người dùng. Bằng cách đó, NI đã mở khóa tính linh hoạt và khả năng mở rộng của hồ dữ liệu của họ đồng thời giảm thiểu sự gián đoạn, cho phép các nhóm sử dụng khả năng phân tích tiên tiến, định vị công ty ở vị trí hàng đầu về quản lý dữ liệu hiện đại và sẵn sàng cho tương lai.

Nếu bạn đang cân nhắc di chuyển Apache Iceberg hoặc gặp phải những thách thức tương tự về cơ sở hạ tầng dữ liệu, chúng tôi khuyến khích bạn khám phá các khả năng. Nắm bắt các định dạng mở, sử dụng tự động hóa và thiết kế với nhu cầu riêng của tổ chức bạn. Hành trình có thể phức tạp, nhưng phần thưởng về khả năng mở rộng, tính linh hoạt và đổi mới rất xứng đáng với nỗ lực. Bạn có thể sử dụng [hướng dẫn theo quy định của AWS](https://docs.aws.amazon.com/prescriptive-guidance/latest/apache-iceberg-on-aws/introduction.html) để giúp tìm hiểu thêm về cách sử dụng Apache Iceberg tốt nhất cho tổ chức của bạn

---


**Giới thiệu về các tác giả**

| Ảnh đại diện | Giới thiệu về các tác giả |
| :---: | :--- |
| <img src="/images/3-BlogsTranslated/WhatsApp-Image-2024-12-30-at-15.19.00-100x100.jpeg" width="220" alt="Yonatan Dolan"> | **Yonatan Dolan** là Chuyên gia phân tích chính tại Amazon Web Services. Yonatan là một nhà truyền giáo Apache Iceberg. |
| <img src="/images/3-BlogsTranslated/Haya-NI-100x100.jpg" width="220" alt="Haya Stern"> | **Haya Stern** là Giám đốc Cấp cao về Dữ liệu tại Natural Intelligence. Cô lãnh đạo việc phát triển nền tảng dữ liệu quy mô lớn của NI, tập trung vào việc cho phép phân tích, hợp lý hóa quy trình làm việc dữ liệu và cải thiện hiệu quả phát triển. Trong năm qua, cô đã dẫn dắt việc di chuyển thành công từ kiến trúc dữ liệu trước đó sang một ngôi nhà hồ hiện đại dựa trên Apache Iceberg và Snowflake. |
| <img src="/images/3-BlogsTranslated/Zion-NI-100x100.jpg" width="220" alt="Zion Rubin"> | **Zion Rubin** là Kiến trúc sư dữ liệu tại Natural Intelligence với mười năm kinh nghiệm kiến trúc các nền tảng dữ liệu lớn quy mô lớn, hiện tập trung vào việc phát triển các hệ thống tác nhân thông minh biến dữ liệu phức tạp thành thông tin chi tiết về kinh doanh theo thời gian thực. |
| <img src="/images/3-BlogsTranslated/Michal-NI-100x141.jpg" width="220" alt="Michał Urbanowicz"> | **Michał Urbanowicz** là Kỹ sư dữ liệu đám mây tại Natural Intelligence với chuyên môn trong việc di chuyển kho dữ liệu và triển khai các quy trình lưu giữ, dọn dẹp và giám sát mạnh mẽ để đảm bảo khả năng mở rộng và độ tin cậy. Ông cũng phát triển các tính năng tự động hóa giúp hợp lý hóa và hỗ trợ các hoạt động quản lý chiến dịch trong môi trường dựa trên đám mây. |
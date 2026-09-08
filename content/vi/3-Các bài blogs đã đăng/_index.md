---
title: "3-Các bài Blogs đã đăng"
weight: 3
---

Trong thời gian thực tập, mình đã tìm hiểu và tổng hợp **3 bài blog kỹ thuật chuyên sâu về Amazon Web Services (AWS)**, tập trung vào các chủ đề **giám sát hệ thống, kết nối mạng và kiến trúc serverless**. Các bài viết giúp củng cố kiến thức thực tế về việc triển khai, bảo mật và vận hành workload trên AWS.

| **STT** | **Đề tài** | **Phạm trù** | **Ngày đăng** |
|---|---|---|---|
| Blog 1 | **Giám sát Amazon EC2 với Amazon CloudWatch và thiết lập cảnh báo** | Monitoring & Operations |  |
| Blog 2 | **Kết nối Amazon S3 từ VPC bằng VPC Endpoint** | Networking & Security |  |
| Blog 3 | **Xây dựng kiến trúc hướng sự kiện với Amazon SQS và AWS Lambda** | Serverless & Event-Driven Architecture |  |

---

### [3.1 Blog 1 – Giám sát Amazon EC2 với Amazon CloudWatch](3.1-blog1/)

Amazon EC2 là một trong những dịch vụ compute phổ biến nhất trên AWS. Khi triển khai EC2 trong môi trường production, việc theo dõi tình trạng hoạt động của instance là rất quan trọng để phát hiện sớm các vấn đề về hiệu năng.

Bài blog trình bày cách sử dụng **Amazon CloudWatch** để thu thập và theo dõi các metric của EC2 như **CPU Utilization**, đồng thời xây dựng **CloudWatch Alarm** để tự động phát hiện khi CPU vượt quá ngưỡng được thiết lập.

Kiến trúc giám sát có thể được mô tả:

**Amazon EC2 → Amazon CloudWatch → CloudWatch Alarm → Notification**

Thông qua CloudWatch, quản trị viên có thể theo dõi tình trạng hệ thống theo thời gian thực, xây dựng dashboard và thiết lập cảnh báo khi workload có dấu hiệu bất thường.

Bài viết cũng trình bày một kịch bản thực tế: tạo tải CPU trên EC2, quan sát metric trên CloudWatch, kiểm tra trạng thái Alarm chuyển sang **In alarm**, sau đó giảm tải và xác nhận Alarm quay trở lại trạng thái **OK**.

---

### [3.2 Blog 2 – Kết nối Amazon S3 từ VPC bằng VPC Endpoint](3.2-blog2/)

Workload chạy trong **Amazon VPC** thường cần truy cập Amazon S3 để lưu trữ hoặc lấy dữ liệu. Tuy nhiên, trong nhiều kiến trúc yêu cầu bảo mật cao, việc đưa traffic ra Internet không phải là lựa chọn tối ưu.

**Amazon VPC Endpoint** cung cấp khả năng kết nối private giữa VPC và các dịch vụ AWS được hỗ trợ.

Bài blog tập trung vào hai mô hình chính:

- **Gateway VPC Endpoint**
- **Interface VPC Endpoint**

Với Gateway Endpoint, route table của VPC được cấu hình để traffic tới Amazon S3 đi qua endpoint thay vì phải sử dụng Internet Gateway hoặc NAT Gateway.

Mô hình:

**EC2 Private Subnet → Route Table → S3 Gateway Endpoint → Amazon S3**

Gateway Endpoint có ưu điểm là cấu hình đơn giản, phù hợp với workload chạy trong VPC và có thể kết hợp với **Endpoint Policy** để kiểm soát quyền truy cập.

Bài viết cũng phân tích **Interface Endpoint** dựa trên AWS PrivateLink. Interface Endpoint sử dụng Elastic Network Interface với private IP trong subnet, cho phép workload kết nối tới dịch vụ thông qua mạng private.

Qua đó, bài blog giúp làm rõ cách lựa chọn VPC Endpoint phù hợp dựa trên yêu cầu về **networking, security, connectivity và cost optimization**.

---

### [3.3 Blog 3 – Xây dựng kiến trúc hướng sự kiện với Amazon SQS và AWS Lambda](3.3-blog3/)

Trong kiến trúc cloud hiện đại, mô hình **event-driven architecture** giúp các thành phần của hệ thống hoạt động độc lập và có khả năng mở rộng tốt hơn.

Bài blog trình bày cách kết hợp **Amazon SQS** và **AWS Lambda** để xây dựng một hệ thống xử lý công việc bất đồng bộ.

Mô hình tổng quát:

**Application → Amazon SQS → AWS Lambda → Processing**

Ứng dụng gửi message vào Amazon SQS thay vì trực tiếp gọi service xử lý. Lambda sau đó lấy message từ queue và thực hiện xử lý tự động.

Cách tiếp cận này mang lại nhiều lợi ích:

- Giảm sự phụ thuộc trực tiếp giữa các service.
- Có khả năng xử lý workload tăng đột biến.
- Lambda tự động mở rộng số lượng execution.
- Amazon SQS giúp lưu trữ message khi workload tăng cao.
- Có thể kiểm soát tốc độ xử lý thông qua cơ chế concurrency.

Bài viết cũng tìm hiểu khả năng **scaling và concurrency của AWS Lambda khi sử dụng Amazon SQS làm event source**, qua đó cho thấy cách AWS cải thiện tốc độ polling và khả năng mở rộng Lambda trong các hệ thống event-driven.

Đây là một pattern phù hợp cho các ứng dụng cần xử lý **background jobs, asynchronous processing, queue-based workload và serverless architecture**.

---

## Tổng kết

Ba bài blog tập trung vào ba khía cạnh quan trọng khi xây dựng hệ thống trên AWS:

1. **CloudWatch** – giám sát và cảnh báo hệ thống.
2. **VPC Endpoint** – xây dựng kết nối private và tăng cường bảo mật.
3. **SQS + Lambda** – xây dựng kiến trúc serverless hướng sự kiện.

Thông qua việc tìm hiểu và thực hành các nội dung trên, mình có thêm kiến thức thực tế về **AWS Cloud, Networking, Monitoring, Security và Serverless Architecture**.
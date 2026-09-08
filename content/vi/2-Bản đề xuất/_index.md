---
title: "2. Bản đề xuất"

weight: 2

---


# AWS Monitoring & Alerting System

## Kiến trúc giám sát và cảnh báo Amazon EC2 trên AWS

### 1. Tóm tắt điều hành

Đề xuất này trình bày giải pháp xây dựng một hệ thống **giám sát và cảnh báo cơ bản cho Amazon EC2** trên nền tảng AWS. Mục tiêu của hệ thống là theo dõi tình trạng hoạt động của EC2 instance, thu thập các thông tin giám sát và log hệ thống, phát hiện các trường hợp CPU sử dụng vượt ngưỡng cho phép và gửi cảnh báo đến người quản trị.

Hệ thống sử dụng các dịch vụ AWS gồm **Amazon EC2, Amazon CloudWatch, CloudWatch Agent, Amazon SNS, IAM và Amazon VPC**. EC2 đóng vai trò là máy chủ cần được giám sát. CloudWatch Agent được cài đặt trên EC2 để thu thập log hệ thống và các thông tin giám sát. CloudWatch chịu trách nhiệm lưu trữ metrics, logs và theo dõi trạng thái của hệ thống thông qua Alarm. Khi CPU vượt ngưỡng được cấu hình, CloudWatch Alarm sẽ chuyển trạng thái từ `OK` sang `In alarm` và gửi thông báo thông qua Amazon SNS đến email người quản trị.

Toàn bộ quy trình được thiết kế theo mô hình:

**EC2 → CloudWatch Agent → CloudWatch Metrics / Logs → CloudWatch Alarm → SNS → Email**

Giải pháp giúp xây dựng một quy trình hoàn chỉnh từ **giám sát → phát hiện → cảnh báo → recovery**, đồng thời giúp người thực tập hiểu được cách triển khai hệ thống monitoring cơ bản trên AWS.

---

### 2. Tuyên bố vấn đề

#### Vấn đề hiện tại

- **Khó theo dõi trạng thái máy chủ**: Khi hệ thống có nhiều EC2 instance, việc kiểm tra thủ công CPU, bộ nhớ và log trên từng máy chủ mất nhiều thời gian.
- **Không phát hiện kịp thời tình trạng quá tải**: Nếu CPU của EC2 tăng cao trong thời gian dài nhưng không có hệ thống cảnh báo, quản trị viên có thể không phát hiện được sự cố kịp thời.
- **Log phân tán trên máy chủ**: Log hệ thống được lưu trực tiếp trên EC2 khiến việc kiểm tra và theo dõi từ xa trở nên khó khăn.
- **Thiếu cơ chế cảnh báo tự động**: Khi xảy ra sự cố, hệ thống không tự động gửi thông báo đến người quản trị.
- **Khó kiểm tra quá trình recovery**: Nếu không có monitoring và Alarm, khó xác định chính xác thời điểm hệ thống trở lại trạng thái bình thường.

#### Giải pháp đề xuất

Hệ thống được thiết kế theo nguyên tắc **tập trung việc giám sát và cảnh báo trên Amazon CloudWatch**.

Kiến trúc bao gồm các thành phần chính:

1. **EC2 Instance**: Chạy hệ điều hành Amazon Linux 2023 và đóng vai trò là máy chủ cần giám sát.
2. **IAM Role**: Cung cấp quyền cần thiết để EC2 gửi dữ liệu monitoring và log lên CloudWatch.
3. **CloudWatch Agent**: Được cài đặt trên EC2 để thu thập log hệ thống và dữ liệu monitoring.
4. **CloudWatch Metrics**: Theo dõi các chỉ số hoạt động của EC2, trong đó có CPU Utilization.
5. **CloudWatch Logs**: Tập trung và lưu trữ log từ EC2.
6. **CloudWatch Alarm**: Giám sát CPU và phát hiện khi CPU vượt ngưỡng 70%.
7. **Amazon SNS**: Nhận thông báo từ CloudWatch Alarm và gửi cảnh báo.
8. **Email**: Nhận thông báo cảnh báo từ SNS.

#### Lợi ích

- **Giám sát tập trung**: Các metrics và logs của EC2 được theo dõi trên CloudWatch.
- **Cảnh báo tự động**: CloudWatch Alarm tự động phát hiện CPU vượt ngưỡng.
- **Thông báo nhanh chóng**: SNS gửi cảnh báo trực tiếp đến email.
- **Theo dõi recovery**: Có thể xác nhận Alarm chuyển từ `In alarm` trở lại `OK`.
- **Dễ triển khai và mở rộng**: Mô hình có thể áp dụng cho nhiều EC2 instance và mở rộng thêm nhiều loại metrics khác.

---

### 3. Kiến trúc giải pháp

#### Sơ đồ kiến trúc tổng thể

![Overall AWS architecture diagram](/QuangThienWorkshop-template/images/anh.png)

#### Chi tiết các thành phần trong kiến trúc

##### 1. Amazon VPC & Public Subnet

EC2 instance được triển khai trong môi trường **Amazon VPC** và Public Subnet để có thể kết nối Internet phục vụ quá trình quản trị và thực hành.

Môi trường thực tế sử dụng:

- **VPC:** `vpc-05c77177c5e1b6477`
- **Subnet:** `public-subnet-monitoring`
- **Subnet CIDR:** `172.31.0.0/20`
- **Availability Zone:** `ap-southeast-2a`

##### 2. Security Group

Security Group được sử dụng để kiểm soát lưu lượng truy cập đến EC2.

Cấu hình chính:

- **Inbound:** SSH TCP port `22` từ My IP.
- **Outbound:** Cho phép EC2 kết nối ra ngoài phục vụ việc cài đặt và gửi dữ liệu monitoring.

##### 3. Amazon EC2

EC2 là máy chủ chính được sử dụng để thực hiện bài thực hành monitoring.

Thông tin triển khai:

- **Instance name:** `Monitoring-Lab-Instance`
- **Instance type:** `t3.micro`
- **Operating System:** Amazon Linux 2023
- **Region:** `ap-southeast-2` (Sydney)

##### 4. IAM Role

IAM Role `EC2-CloudWatchAgent-Role` được gắn với EC2 instance nhằm cung cấp quyền cho CloudWatch Agent gửi dữ liệu monitoring và logs lên CloudWatch.

Policy chính:

`CloudWatchAgentServerPolicy`

##### 5. CloudWatch Agent

CloudWatch Agent được cài đặt trực tiếp trên EC2 instance.

Agent có nhiệm vụ thu thập dữ liệu monitoring và log hệ thống, sau đó gửi dữ liệu lên Amazon CloudWatch.

Version được sử dụng:

`1.300069.1`

##### 6. CloudWatch Metrics

CloudWatch Metrics được sử dụng để theo dõi các chỉ số hoạt động của EC2.

Trong workshop, metric quan trọng nhất là:

`CPUUtilization`

Metric này được sử dụng làm cơ sở để tạo CloudWatch Alarm.

##### 7. CloudWatch Logs

CloudWatch Logs được sử dụng để tập trung log từ EC2.

Các Log Group được sử dụng:

- `messages`
- `secure`

Thời gian lưu trữ log:

**7 ngày**

##### 8. CloudWatch Alarm

CloudWatch Alarm được cấu hình để theo dõi CPU Utilization.

Alarm:

`High-CPU-Alarm-Monitoring-Lab`

Ngưỡng:

**CPU > 70% trong 5 phút**

Khi CPU vượt ngưỡng, Alarm chuyển trạng thái:

`OK → In alarm`

Khi CPU giảm trở lại mức bình thường:

`In alarm → OK`

##### 9. Amazon SNS

Amazon SNS được sử dụng để gửi thông báo khi CloudWatch Alarm thay đổi trạng thái.

SNS Topic:

`system-alerts`

SNS gửi email cảnh báo đến địa chỉ email đã đăng ký và xác nhận subscription.

---

### 4. Triển khai kỹ thuật

#### Các giai đoạn triển khai

1. **Giai đoạn 1: Chuẩn bị môi trường AWS**
   - Tạo hoặc sử dụng Amazon VPC.
   - Xác định Public Subnet.
   - Cấu hình Security Group.
   - Chuẩn bị quyền IAM cho EC2.

2. **Giai đoạn 2: Triển khai Amazon EC2**
   - Tạo EC2 instance.
   - Sử dụng Amazon Linux 2023.
   - Chọn instance type `t3.micro`.
   - Gắn IAM Role `EC2-CloudWatchAgent-Role`.
   - Kiểm tra trạng thái EC2 sau khi khởi chạy.

3. **Giai đoạn 3: Cài đặt CloudWatch Agent**
   - Kết nối tới EC2 thông qua SSH.
   - Cài đặt CloudWatch Agent.
   - Kiểm tra version Agent.
   - Tạo và cấu hình file configuration.
   - Khởi động CloudWatch Agent.
   - Kiểm tra trạng thái Agent.

4. **Giai đoạn 4: Cấu hình CloudWatch Logs**
   - Cấu hình Agent thu thập log hệ thống.
   - Gửi log từ EC2 lên CloudWatch Logs.
   - Kiểm tra Log Group `messages`.
   - Kiểm tra Log Group `secure`.
   - Kiểm tra các log events.

5. **Giai đoạn 5: Cấu hình CloudWatch Alarm**
   - Chọn metric `CPUUtilization`.
   - Thiết lập ngưỡng CPU trên 70%.
   - Cấu hình thời gian đánh giá 5 phút.
   - Đặt tên Alarm `High-CPU-Alarm-Monitoring-Lab`.
   - Kiểm tra trạng thái ban đầu của Alarm.

6. **Giai đoạn 6: Cấu hình Amazon SNS**
   - Tạo SNS Topic `system-alerts`.
   - Tạo email subscription.
   - Xác nhận subscription.
   - Liên kết SNS với CloudWatch Alarm.
   - Kiểm tra khả năng nhận email cảnh báo.

7. **Giai đoạn 7: Kiểm thử hệ thống**
   - Tạo tải CPU bằng công cụ `stress`.
   - Theo dõi CPU Utilization.
   - Kiểm tra Alarm chuyển sang `In alarm`.
   - Kiểm tra SNS gửi email.
   - Dừng tải CPU.
   - Kiểm tra CPU giảm về bình thường.
   - Xác nhận Alarm trở lại `OK`.

#### Yêu cầu kỹ thuật & Bảo mật

- **IAM Role**: EC2 sử dụng IAM Role để truy cập các dịch vụ AWS cần thiết thay vì lưu Access Key trực tiếp trên máy chủ.
- **Security Group**: Chỉ cho phép SSH TCP port `22` từ địa chỉ IP quản trị.
- **CloudWatch Monitoring**: Theo dõi trạng thái hoạt động của EC2 thông qua metrics và logs.
- **SNS Notification**: Chỉ sử dụng email subscription đã được xác nhận để nhận cảnh báo.
- **Resource Cleanup**: Dừng EC2 sau khi hoàn thành workshop để tránh phát sinh chi phí không cần thiết.

---

### 5. Lộ trình & Mốc triển khai

```text
+--------------------------------------------------------------------------------+
| Giai đoạn 1: Chuẩn bị môi trường AWS                                           |
|   - Xác định VPC, Public Subnet và Security Group                              |
|   - Chuẩn bị IAM Role                                                          |
+--------------------------------------------------------------------------------+
                                  |
                                  v
+--------------------------------------------------------------------------------+
| Giai đoạn 2: Triển khai EC2                                                     |
|   - Tạo Monitoring-Lab-Instance                                                |
|   - Cấu hình Amazon Linux 2023 và SSH                                          |
+--------------------------------------------------------------------------------+
                                  |
                                  v
+--------------------------------------------------------------------------------+
| Giai đoạn 3: Cấu hình CloudWatch Agent                                          |
|   - Cài đặt CloudWatch Agent                                                   |
|   - Cấu hình Metrics và Logs                                                   |
|   - Kiểm tra Agent hoạt động                                                   |
+--------------------------------------------------------------------------------+
                                  |
                                  v
+--------------------------------------------------------------------------------+
| Giai đoạn 4: Cấu hình CloudWatch & SNS                                          |
|   - Tạo CloudWatch Alarm                                                       |
|   - Cấu hình ngưỡng CPU > 70%                                                  |
|   - Tạo SNS Topic và Email Subscription                                        |
+--------------------------------------------------------------------------------+
                                  |
                                  v
+--------------------------------------------------------------------------------+
| Giai đoạn 5: Kiểm thử & Recovery                                                |
|   - Tạo tải CPU                                                                |
|   - Kiểm tra Alarm chuyển In alarm                                             |
|   - Kiểm tra email SNS                                                         |
|   - Dừng tải và xác nhận Alarm trở lại OK                                      |
+--------------------------------------------------------------------------------+
```

---

### 6. Ước tính ngân sách

Workshop được thiết kế theo hướng **đơn giản và tiết kiệm chi phí**, sử dụng các tài nguyên AWS cần thiết cho mục đích thực hành.

| **Dịch vụ AWS** | **Cấu hình / Quy mô ước tính** | **Chi phí ước tính** |
|---|---|---|
| **Amazon EC2** | `t3.micro`, sử dụng trong thời gian thực hành | Phụ thuộc thời gian sử dụng |
| **Amazon CloudWatch** | Metrics, Logs và Alarm | Phụ thuộc mức sử dụng |
| **CloudWatch Agent** | Cài đặt trên EC2 | Không có phí riêng |
| **Amazon SNS** | 1 Topic + Email Subscription | Chi phí thấp / phụ thuộc sử dụng |
| **Amazon VPC** | VPC và Public Subnet | Không tính phí riêng cho VPC/Subnet |
| **Security Group** | SSH TCP/22 | Không tính phí riêng |
| **IAM Role** | `EC2-CloudWatchAgent-Role` | Không tính phí riêng |

> **Điểm tối ưu chi phí**:
>
> 1. Sử dụng instance type `t3.micro` phù hợp cho môi trường thực hành.
> 2. Chỉ chạy EC2 trong thời gian cần thiết.
> 3. Dừng EC2 sau khi hoàn thành kiểm thử.
> 4. Cấu hình thời gian lưu trữ CloudWatch Logs là 7 ngày.
> 5. Theo dõi AWS Billing để kiểm soát chi phí phát sinh.

---

### 7. Đánh giá rủi ro

#### Ma trận rủi ro & Chiến lược giảm thiểu

| **Rủi ro tiềm ẩn** | **Mức độ ảnh hưởng** | **Xác suất** | **Chiến lược giảm thiểu** |
|---|---|---|---|
| **EC2 không thể kết nối SSH** | Trung bình | Trung bình | Kiểm tra Public IP, Security Group và quyền truy cập TCP port 22. |
| **CloudWatch Agent không hoạt động** | Cao | Thấp | Kiểm tra service status, configuration và IAM Role của EC2. |
| **Không xuất hiện Log Group** | Trung bình | Trung bình | Kiểm tra cấu hình CloudWatch Agent và quyền `CloudWatchAgentServerPolicy`. |
| **CPU không vượt ngưỡng Alarm** | Trung bình | Thấp | Sử dụng công cụ `stress` để tạo tải CPU và kiểm tra lại metric. |
| **SNS không gửi email** | Cao | Thấp | Kiểm tra SNS subscription đã được xác nhận và kiểm tra cấu hình Alarm Action. |
| **Alarm không trở lại OK** | Trung bình | Thấp | Dừng tiến trình tạo tải CPU và tiếp tục theo dõi CPU Utilization. |
| **Phát sinh chi phí AWS** | Trung bình | Trung bình | Dừng EC2 và kiểm tra tài nguyên sau khi hoàn thành workshop. |

---

### 8. Kết quả kỳ vọng

- **Xây dựng thành công hệ thống monitoring**: Triển khai được hệ thống giám sát cơ bản cho Amazon EC2 bằng CloudWatch.
- **Thu thập metrics và logs**: CloudWatch Agent gửi dữ liệu monitoring và log từ EC2 lên CloudWatch.
- **Phát hiện tình trạng CPU cao**: CloudWatch Alarm phát hiện khi CPU vượt ngưỡng 70%.
- **Cảnh báo tự động**: Amazon SNS gửi email khi Alarm chuyển sang trạng thái `In alarm`.
- **Kiểm tra recovery**: Alarm chuyển từ `In alarm` trở lại `OK` sau khi CPU giảm.
- **Nâng cao kiến thức AWS**: Hiểu được cách kết hợp IAM, VPC, EC2, CloudWatch và SNS để xây dựng một hệ thống monitoring thực tế.
- **Tối ưu chi phí**: Sử dụng tài nguyên ở mức phù hợp với môi trường thực hành và thực hiện cleanup sau khi hoàn thành.

Mục tiêu cuối cùng của workshop là xây dựng và kiểm thử thành công quy trình:

**Monitoring → Detection → Alerting → Recovery**

qua đó chứng minh hệ thống có khả năng **giám sát, phát hiện sự cố, gửi cảnh báo và xác nhận hệ thống phục hồi** trên môi trường AWS.
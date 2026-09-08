---
title: "5. Workshop"
weight: 5
---

# Workshop AWS Monitoring

Workshop này xây dựng và kiểm thử một hệ thống giám sát cơ bản cho một Amazon EC2 instance.

Luồng giám sát:

**EC2 Instance → CloudWatch Agent → CloudWatch Logs / Metrics → CloudWatch Alarm → SNS → Email**

Workshop bao gồm cấu hình IAM, mạng VPC/Subnet/Security Group, triển khai EC2, cài đặt CloudWatch Agent, thu thập log, giám sát CPU, tạo Alarm, gửi cảnh báo qua SNS, kiểm thử recovery và dọn dẹp tài nguyên.

## Sơ đồ kiến trúc tổng thể

Sơ đồ dưới đây mô tả kiến trúc AWS được triển khai thực tế trong workshop:

![Sơ đồ kiến trúc tổng thể](/QuangThienWorkshop-template/images/anh.png)

## Luồng hoạt động

1. **USER** truy cập vào môi trường AWS thông qua Internet.
2. **Internet Gateway** cung cấp kết nối Internet cho VPC.
3. **VPC** sử dụng CIDR `10.0.0.0/16`.
4. **Public Subnet** sử dụng CIDR `10.0.1.0/24`.
5. **EC2** được triển khai trong Public Subnet.
6. **Security Group** kiểm soát lưu lượng truy cập đến EC2.
7. **IAM Role** cung cấp quyền cần thiết cho EC2 gửi dữ liệu giám sát lên CloudWatch.
8. **CloudWatch Metrics** nhận các metric, trong đó có CPU Utilization.
9. **CloudWatch Logs** lưu trữ các log từ EC2.
10. **CloudWatch Alarm** giám sát CPU và phát hiện khi CPU vượt ngưỡng.
11. **SNS** nhận thông báo từ CloudWatch Alarm.
12. **Email** nhận cảnh báo từ SNS.

## Môi trường triển khai thực tế

- **Region:** `ap-southeast-2` (Sydney)
- **EC2:** Amazon Linux 2023, `t3.micro`
- **Instance name:** `Monitoring-Lab-Instance`
- **IAM Role:** `EC2-CloudWatchAgent-Role`
- **Log Groups:** `messages`, `secure`
- **Alarm:** `High-CPU-Alarm-Monitoring-Lab`
- **SNS Topic:** `system-alerts`
- **Retention Log:** 7 ngày

## Kết quả

Toàn bộ kịch bản kiểm thử chính đã đạt:

- CloudWatch Agent hoạt động.
- Log xuất hiện trên CloudWatch Logs.
- CloudWatch Metrics nhận dữ liệu giám sát.
- Alarm chuyển trạng thái khi CPU vượt ngưỡng.
- SNS gửi email cảnh báo.
- Alarm quay lại `OK` sau khi dừng tải CPU.

Hệ thống đáp ứng được mục tiêu của workshop là xây dựng một quy trình **giám sát → phát hiện → cảnh báo → recovery** cho Amazon EC2.
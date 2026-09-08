---
title: "5.1 Tổng quan Workshop"
weight: 1
---

## Mục tiêu

Xây dựng và kiểm thử một hệ thống AWS Monitoring thực tế cho một EC2 instance.

Hệ thống thu thập log hệ thống và metric hiệu năng, theo dõi CPU, phát hiện tải cao thông qua CloudWatch Alarm và gửi email cảnh báo thông qua Amazon SNS.

## Kiến trúc giám sát

**EC2 → CloudWatch Agent → CloudWatch Logs / Metrics → CloudWatch Alarm → SNS → Email**

## Các dịch vụ AWS sử dụng

- **Amazon EC2:** máy chủ Linux được giám sát.
- **AWS IAM:** cấp quyền cho CloudWatch Agent.
- **Amazon VPC:** cung cấp môi trường mạng.
- **Amazon CloudWatch:** thu thập Logs/Metrics và tạo Alarm.
- **Amazon SNS:** gửi email khi Alarm thay đổi trạng thái.

## Kết quả mong đợi

Sau Workshop, hệ thống phải có khả năng thu thập log, theo dõi CPU, kích hoạt Alarm khi CPU vượt 70%, gửi email cảnh báo và chuyển Alarm trở lại `OK` khi tải CPU giảm.

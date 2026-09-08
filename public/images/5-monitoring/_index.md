---
title: "5. Hệ thống Log tập trung & Giám sát cơ bản"
weight: 5
---

# Hệ thống Log tập trung & Giám sát cơ bản

Workshop triển khai hệ thống Monitoring trên AWS với EC2, IAM, CloudWatch, SNS và VPC.

**Region:** `ap-southeast-2 (Sydney)`  
**Trạng thái:** Hoàn thành - toàn bộ kịch bản kiểm thử đều đạt.

## Nội dung

1. [Tổng quan](1-overview/)
2. [Kiến trúc hệ thống](2-architecture/)
3. [Chuẩn bị IAM & EC2](3-setup-iam-ec2/)
4. [Cài đặt CloudWatch Agent](4-cloudwatch-agent/)
5. [CloudWatch Alarm & SNS](5-cloudwatch-alarm-sns/)
6. [Kiểm thử hệ thống](6-testing/)
7. [Kết quả đạt được](7-results/)
8. [Xử lý sự cố](8-troubleshooting/)
9. [Chi phí & tài liệu tham khảo](9-cost-reference/)

## Luồng tổng quát

```text
EC2
 ↓
CloudWatch Agent
 ↓
CloudWatch Logs / Metrics
 ↓
CloudWatch Alarm
 ↓
SNS
 ↓
Email
```

---
title: "Tổng quan"
weight: 1
---

# Mục tiêu & ý nghĩa

Dự án xây dựng hệ thống giám sát tập trung cho một EC2 instance, thu thập log hệ thống về CloudWatch Logs, theo dõi `CPUUtilization` theo thời gian thực, tự động phát hiện tải cao qua CloudWatch Alarm và gửi cảnh báo email qua SNS.

Dự án đã được triển khai và kiểm thử thành công đầu-cuối: từ cài đặt hạ tầng, cấu hình Agent, đến việc xác nhận Alarm thực sự kích hoạt và gửi email khi CPU vượt ngưỡng.

## AWS Services

- EC2
- IAM
- CloudWatch
- SNS
- VPC

**Region:** `ap-southeast-2 (Sydney)`

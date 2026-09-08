---
title: "5.10 Monitoring"
weight: 10
---

## Kiểm tra hệ thống Monitoring

Hệ thống được theo dõi theo chuỗi:

**EC2 → CloudWatch Agent → Logs / Metrics → Alarm → SNS → Email**

Các thành phần cần kiểm tra:

- CloudWatch Agent: `running`
- Log Groups: `messages`, `secure`
- Metric: `CPUUtilization`
- Alarm: `High-CPU-Alarm-Monitoring-Lab`
- SNS Topic: `system-alerts`

Mục tiêu là xác nhận dữ liệu từ EC2 được thu thập và Alarm có thể phản ứng khi CPU tăng cao.

---
title: "Kiến trúc hệ thống"
weight: 2
---

# Kiến trúc & tài nguyên

## Luồng dữ liệu

```text
EC2 Instance (CloudWatch Agent)
              │
              ▼
     CloudWatch Logs / Metrics
              │
              ▼
       CloudWatch Alarm
              │
              ▼
          SNS Topic
              │
              ▼
            Email
```

## Vai trò dịch vụ

| Dịch vụ | Vai trò |
|---|---|
| EC2 | Nguồn phát sinh log hệ thống và metric hiệu năng |
| IAM | Cấp quyền cho CloudWatch Agent |
| CloudWatch | Thu thập Logs, Metrics và tạo Alarms |
| SNS | Gửi thông báo email khi Alarm chuyển trạng thái |
| VPC/Subnet | Hạ tầng mạng cho EC2 |

## Tài nguyên

| Thành phần | Giá trị |
|---|---|
| Instance | `Monitoring-Lab-Instance` |
| Instance ID | `i-0b1a18be8044b8bb0` |
| Region | `ap-southeast-2 (Sydney)` |
| VPC | `vpc-05c77177c5e1b6477` |
| Subnet | `public-subnet-monitoring` |
| CIDR | `172.31.0.0/20` |
| IAM Role | `EC2-CloudWatchAgent-Role` |
| Log Groups | `messages`, `secure` |
| Alarm | `High-CPU-Alarm-Monitoring-Lab` |
| SNS Topic | `system-alerts` |

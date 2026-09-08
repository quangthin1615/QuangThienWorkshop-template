---
title: "Chuẩn bị IAM & EC2"
weight: 3
---

# Chuẩn bị IAM & EC2

## 3.1 Tạo IAM Role

Mục đích: cấp quyền để CloudWatch Agent trên EC2 có thể gửi log và metric lên CloudWatch.

1. Vào **IAM Console → Roles → Create role**.
2. Chọn **AWS service**, use case **EC2**.
3. Tìm và chọn `CloudWatchAgentServerPolicy`.
4. Đặt Role name: `EC2-CloudWatchAgent-Role`.
5. Kiểm tra permissions và chọn **Create role**.

## 3.2 Tạo Subnet

Do Default VPC không còn subnet khả dụng:

1. Vào **VPC Console → Subnets → Create subnet**.
2. Chọn Default VPC.
3. Subnet name: `public-subnet-monitoring`.
4. Availability Zone: `ap-southeast-2a`.
5. IPv4 CIDR: `172.31.0.0/20`.
6. Bật **Enable auto-assign public IPv4 address**.

## 3.3 Tạo EC2 Instance

- Name: `Monitoring-Lab-Instance`
- AMI: Amazon Linux 2023
- Instance type: `t3.micro`
- Key pair: `monitoring-lab-key.pem`
- Subnet: `public-subnet-monitoring`
- Auto-assign Public IP: Enable
- Security Group: SSH port 22 từ My IP
- IAM instance profile: `EC2-CloudWatchAgent-Role`

Sau khi Launch, chờ instance chuyển sang `Running` và Status checks đạt.

---
title: "5.2 Chuẩn bị"
weight: 2
---

## Yêu cầu

- Có tài khoản AWS.
- Có quyền truy cập các dịch vụ EC2, IAM, VPC, CloudWatch và SNS.
- Có máy Windows để kết nối SSH.
- Có PowerShell.
- Có key pair định dạng `.pem`.

## Thông tin lab

- Region: `ap-southeast-2` (Sydney)
- Instance type: `t3.micro`
- AMI: Amazon Linux 2023
- Key pair: `monitoring-lab-key.pem`
- Instance name: `Monitoring-Lab-Instance`

## Lưu ý

Trong quá trình thực hiện cần theo dõi trạng thái EC2 và CloudWatch. Sau khi kiểm thử xong nên Stop EC2 để tránh phát sinh chi phí không cần thiết.

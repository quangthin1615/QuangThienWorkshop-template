---
title: "5.4.2 Tạo Public Subnet"
weight: 2
---

## Tạo Subnet

1. Vào **VPC Console → Subnets → Create subnet**.
2. Chọn **Default VPC**.
3. Đặt Subnet name: `public-subnet-monitoring`.
4. Availability Zone: `ap-southeast-2a`.
5. IPv4 CIDR: `172.31.0.0/20`.
6. Bấm **Create subnet**.
7. Chọn subnet vừa tạo → **Actions → Edit subnet settings**.
8. Bật **Enable auto-assign public IPv4 address**.
9. Lưu cấu hình.

## Kết quả

Subnet public được tạo và có khả năng cấp Public IPv4 cho EC2.

---
title: "5.3.3 Kiểm tra môi trường AWS"
weight: 3
---

## Kiểm tra

Kiểm tra Default VPC và tài nguyên mạng hiện có.

Trong lab thực tế, Default VPC không còn subnet khả dụng nên cần tạo lại một subnet trước khi tạo EC2.

Thông tin subnet sử dụng:

- Name: `public-subnet-monitoring`
- Availability Zone: `ap-southeast-2a`
- IPv4 CIDR: `172.31.0.0/20`

## Kết quả

Môi trường mạng được kiểm tra và sẵn sàng cho bước tạo Subnet và EC2.

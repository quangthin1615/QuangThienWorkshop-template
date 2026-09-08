---
title: "5.4 Networking"
weight: 4
---

## Mục tiêu

Chuẩn bị mạng public cho EC2 instance.

Luồng mạng:

**EC2 → Public Subnet → Route 0.0.0.0/0 → Internet Gateway**

Default VPC đã có Internet Gateway và route mặc định nên không cần tạo route thủ công.

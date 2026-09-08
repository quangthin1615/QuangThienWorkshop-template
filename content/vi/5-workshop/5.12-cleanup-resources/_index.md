---
title: "5.12 Dọn dẹp tài nguyên"
weight: 12
---

## Dừng EC2

Sau khi hoàn thành kiểm thử:

1. Vào **EC2 Console → Instances**.
2. Chọn `Monitoring-Lab-Instance`.
3. Chọn **Instance state → Stop instance**.
4. Xác nhận Stop.
5. Không cần chọn Skip OS shutdown.

Trong lab này, VPC, Subnet, Security Group, IAM Role, Alarm và SNS Topic được giữ lại để sử dụng cho các lần học tiếp theo.

![Hình 16. Xác nhận Stop EC2 instance để tránh phát sinh chi phí]16

## Kết quả

EC2 được Stop sau khi hoàn thành kiểm thử, giúp hạn chế chi phí phát sinh.

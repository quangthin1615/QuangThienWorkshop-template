---
title: "5.6.1 Khởi tạo EC2"
weight: 1
---

## Tạo EC2 Instance

1. Vào **EC2 Console → Instances → Launch instance**.
2. Name: `Monitoring-Lab-Instance`.
3. AMI: **Amazon Linux 2023**.
4. Instance type: `t3.micro`.
5. Tạo key pair `monitoring-lab-key.pem` với RSA, định dạng `.pem`.
6. Network settings:
   - VPC: Default VPC
   - Subnet: `public-subnet-monitoring`
   - Auto-assign Public IP: Enable
   - Security Group: cho phép SSH từ My IP.
7. Advanced details → IAM instance profile: chọn `EC2-CloudWatchAgent-Role`.
8. Bấm **Launch instance**.
9. Chờ instance chuyển sang `Running` và Status Check đạt.

![Hình 2. Khởi tạo EC2 instance thành công](/QuangThienWorkshop-template/images/figure-02.png)

![Hình 3. Instance chuyển trạng thái Running và Status Check đạt](/QuangThienWorkshop-template/images/figure-03.png)

## Kết quả

EC2 `Monitoring-Lab-Instance` được tạo thành công.

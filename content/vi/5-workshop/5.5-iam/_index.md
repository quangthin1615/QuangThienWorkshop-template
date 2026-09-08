---
title: "5.5 IAM"
weight: 5
---

## Tạo IAM Role cho EC2

### Mục đích

Cấp quyền cần thiết để CloudWatch Agent trên EC2 có thể gửi log và metric lên CloudWatch.

### Thực hiện

1. Vào **IAM Console → Roles → Create role**.
2. Trusted entity type: **AWS service**.
3. Use case: **EC2**.
4. Bấm **Next**.
5. Tìm `CloudWatchAgentServerPolicy`.
6. Chọn đúng policy này.
7. Đặt Role name: `EC2-CloudWatchAgent-Role`.
8. Kiểm tra lại policy.
9. Bấm **Create role**.

![Hình 1. IAM Role EC2-CloudWatchAgent-Role được tạo thành công](/QuangThienWorkshop-template/images/figure-01.png)

## Kết quả

IAM Role `EC2-CloudWatchAgent-Role` được tạo và sẵn sàng gắn vào EC2.

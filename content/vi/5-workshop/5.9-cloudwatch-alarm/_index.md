---
title: "5.9 CloudWatch Alarm"
weight: 9
---

## Tạo Alarm

1. Vào **CloudWatch → Alarms → Create alarm → Select metric**.
2. Chọn **EC2 → Per-Instance Metrics**.
3. Tìm Instance ID của `Monitoring-Lab-Instance`.
4. Chọn metric `CPUUtilization`.
5. Statistic: `Average`.
6. Period: `5 minutes`.
7. Threshold type: `Static`.
8. Condition: **Greater than 70**.
9. Bấm **Next**.

![Hình 10. Cấu hình Alarm CPUUtilization > 70%](/QuangThienWorkshop-template/images/figure-10.png)

## Kết quả

Alarm được cấu hình để phát hiện CPU vượt 70% trong khoảng thời gian theo cấu hình.

---
title: "CloudWatch Alarm & SNS"
weight: 5
---

# CloudWatch Alarm & SNS

## 5.1 Tạo CloudWatch Alarm

1. Vào **CloudWatch → Alarms → Create alarm → Select metric**.
2. Chọn **EC2 → Per-Instance Metrics**.
3. Tìm Instance ID và chọn `CPUUtilization`.
4. Statistic: `Average`.
5. Period: `5 minutes`.
6. Threshold type: `Static`.
7. Condition: **Greater than 70**.

Điều kiện:

```text
CPUUtilization > 70%
trong 5 phút
```

## 5.2 Tạo SNS Topic

1. Alarm state trigger: `In alarm`.
2. Chọn **Create new topic**.
3. Topic name: `system-alerts`.
4. Nhập email nhận cảnh báo.
5. Mở email từ AWS Notification và chọn **Confirm subscription**.

## 5.3 Hoàn tất Alarm

Đặt:

```text
Alarm name = High-CPU-Alarm-Monitoring-Lab
```

Sau đó kiểm tra Preview và Create alarm.

## Luồng cảnh báo

```text
CPU > 70%
     ↓
CloudWatch Alarm
     ↓
State = ALARM
     ↓
SNS system-alerts
     ↓
Email
```

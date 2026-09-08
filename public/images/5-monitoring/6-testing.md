---
title: "Kiểm thử hệ thống"
weight: 6
---

# Kiểm thử toàn hệ thống

## 6.1 Tạo tải CPU

Trên terminal SSH:

```bash
sudo yum install stress -y
```

Chạy tải trong 5 phút:

```bash
stress --cpu 2 --timeout 300
```

## 6.2 Theo dõi Alarm

Mở **CloudWatch → Alarms → High-CPU-Alarm-Monitoring-Lab**.

Theo dõi:

```text
OK → ALARM
```

Kết quả thực tế: CPU đạt khoảng `87–100%`, vượt ngưỡng 70%.

## 6.3 Kiểm tra Email

Kiểm tra hộp thư nhận cảnh báo từ SNS.

Email chứa thông tin chi tiết về Alarm và lý do kích hoạt.

## 6.4 Kiểm tra Alarm quay về OK

Sau khi lệnh `stress` tự kết thúc:

```text
CPU giảm
   ↓
ALARM → OK
```

Biểu đồ CPU thể hiện rõ giai đoạn tăng tải và giảm tải.

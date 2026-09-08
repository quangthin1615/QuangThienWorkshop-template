---
title: "Kết quả đạt được"
weight: 7
---

# Kết quả kiểm thử

| Kịch bản | Kết quả |
|---|---|
| Cài CloudWatch Agent qua yum | Đạt |
| Cấu hình Agent | Đạt |
| Agent gửi log về CloudWatch | Đạt |
| SSH tạo sự kiện log | Đạt |
| Chạy `stress --cpu 2 --timeout 300` | Đạt |
| CPU vượt 70% | Đạt |
| Alarm chuyển OK → ALARM | Đạt |
| SNS gửi email | Đạt |
| Dừng tải, Alarm quay về OK | Đạt |

## Kết quả đạt được

- Log hệ thống được tập trung và truy vấn trên CloudWatch Logs, retention 7 ngày.
- Alarm hoạt động chính xác theo ngưỡng khi mô phỏng tải cao.
- Nhận được email cảnh báo tự động qua SNS.
- Đã xử lý thành công nhiều sự cố thực tế phát sinh ngoài kế hoạch.
- Áp dụng nguyên tắc least privilege khi cấp quyền cho CloudWatch Agent.

## Kết luận

Hệ thống Monitoring đã được triển khai và kiểm thử thành công đầu-cuối. Luồng từ EC2 → CloudWatch → Alarm → SNS → Email hoạt động đúng theo thiết kế.

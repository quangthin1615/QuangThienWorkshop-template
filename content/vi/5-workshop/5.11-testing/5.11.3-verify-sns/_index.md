---
title: "5.11.3 Kiểm tra SNS"
weight: 3
---

Sau khi Alarm chuyển sang `In alarm`:

1. Mở hộp thư email đã đăng ký.
2. Kiểm tra email cảnh báo từ AWS Notification.
3. Xác nhận email có Alarm Details và Reason.
4. Kiểm tra thời điểm Alarm chuyển trạng thái.

Ví dụ nội dung cảnh báo thực tế:

```text
State Change: OK -> ALARM
Reason: Threshold Crossed
[100.0] was greater than the threshold (70.0)
```

![Hình 14. Email cảnh báo thực tế nhận được từ SNS](/QuangThienWorkshop-template/images/figure-14.png)
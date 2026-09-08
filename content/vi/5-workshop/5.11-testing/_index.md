---
title: "5.11 Testing"
weight: 11
---

## Mục tiêu kiểm thử

Kiểm thử end-to-end:

**Tạo tải CPU → CloudWatch nhận metric → Alarm chuyển In alarm → SNS gửi email → CPU giảm → Alarm trở lại OK**

## Bảng kết quả kiểm thử

| Kịch bản | Kết quả mong đợi | Kết quả thực tế | Đánh giá |
|---|---|---|---|
| Cài CloudWatch Agent | Cài thành công | Version 1.300069.1 cài thành công | Đạt |
| Cấu hình Agent | Có config hợp lệ | Config hoạt động sau khi xử lý `collectd` | Đạt |
| Gửi log | Log Group xuất hiện | `messages`, `secure` xuất hiện | Đạt |
| Chạy stress | CPU vượt 70% | CPU đạt khoảng 87–100% | Đạt |
| Alarm | OK → In alarm | Alarm chuyển trạng thái | Đạt |
| SNS | Có email cảnh báo | Email nhận đầy đủ Details/Reason | Đạt |
| Dừng tải | CPU giảm | CPU giảm về bình thường | Đạt |
| Recovery | In alarm → OK | Alarm quay lại OK | Đạt |

## Kết luận

Toàn bộ kịch bản kiểm thử chính đều đạt, chứng minh luồng monitoring và cảnh báo hoạt động end-to-end.

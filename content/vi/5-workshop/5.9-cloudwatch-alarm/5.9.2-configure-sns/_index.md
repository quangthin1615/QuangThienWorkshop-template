---
title: "5.9.2 Cấu hình SNS"
weight: 2
---

## Tạo SNS Topic

1. Ở **Configure actions**, Alarm state trigger: chọn `In alarm`.
2. Chọn **Create new topic**.
3. Topic name: `system-alerts`.
4. Nhập email nhận cảnh báo.
5. Bấm **Create topic**.
6. Mở email từ AWS Notification.
7. Bấm **Confirm subscription**.
8. Đặt Alarm name: `High-CPU-Alarm-Monitoring-Lab`.
9. Kiểm tra lại cấu hình và bấm **Create alarm**.

![Hình 11. Cấu hình SNS Topic system-alerts](/QuangThienWorkshop-template/images/figure-11.png)

![Hình 12. Xác nhận email subscription thành công](/QuangThienWorkshop-template/images/figure-12.png)
## Kết quả

SNS Topic `system-alerts` có email subscription ở trạng thái đã xác nhận.

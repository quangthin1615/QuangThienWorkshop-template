---
title: "5.11.4 Kiểm tra Alarm trở lại OK"
weight: 4
---

## Kiểm tra Alarm trở lại trạng thái OK

Sau khi lệnh `stress` kết thúc sau 300 giây:

1. CPU giảm dần.
2. Tiếp tục quan sát Alarm trên CloudWatch.
3. Xác nhận trạng thái Alarm chuyển từ `In alarm` → `OK`.
4. Kiểm tra biểu đồ CPU thể hiện quá trình tăng tải rồi giảm tải.

## Kết quả thực tế

Alarm quay lại trạng thái `OK`, chứng minh cơ chế recovery hoạt động đúng.

## Minh chứng thực tế

![Hình 15. Alarm quay lại OK sau khi dừng tải](/QuangThienWorkshop-template/images/figure-15.png)

*Hình 15. Alarm quay lại OK sau khi dừng tải*

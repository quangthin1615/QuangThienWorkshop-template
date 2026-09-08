---
title: "Xử lý sự cố"
weight: 8
---

# Bài học & sự cố thực tế

| Sự cố | Nguyên nhân | Cách khắc phục |
|---|---|---|
| Default VPC không có subnet khả dụng | Subnet mặc định đã bị xoá | Tạo lại subnet, bật Auto-assign Public IPv4 |
| EC2 Instance Connect lỗi | Lỗi tạm thời phía dịch vụ trình duyệt | SSH qua PowerShell bằng key pair `.pem` |
| Log Group không xuất hiện | Amazon Linux 2023 không cài sẵn rsyslog | Cài và khởi động rsyslog |
| Agent báo `permission denied` | File log chỉ root đọc được, Agent chạy dưới `cwagent` | Thêm `cwagent` vào group `adm`, chmod 640, chgrp `adm` |
| Wizard bật CollectD | Chọn nhầm Yes dù chưa cài CollectD | Xoá khối `collectd` trong `config.json` |

## Ghi chú

- Amazon Linux 2023 dùng journald làm hệ thống log mặc định; Amazon Linux 2 có sẵn rsyslog.
- CloudWatch Agent publish dữ liệu theo chu kỳ mặc định 1 phút, cần chờ vài phút trước khi kỳ vọng thấy dữ liệu.
- Khi EC2 Instance Connect lỗi dù cấu hình mạng đúng, SSH qua terminal là phương án dự phòng đáng tin cậy.

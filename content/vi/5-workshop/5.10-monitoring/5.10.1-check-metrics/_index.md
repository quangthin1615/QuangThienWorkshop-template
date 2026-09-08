---
title: "5.10.1 Kiểm tra Metrics"
weight: 1
---

## Kiểm tra CPUUtilization

1. Vào **CloudWatch → Metrics**.
2. Chọn **EC2 → Per-Instance Metrics**.
3. Tìm instance `Monitoring-Lab-Instance`.
4. Mở metric `CPUUtilization`.
5. Quan sát dữ liệu theo thời gian.

CloudWatch Agent publish dữ liệu theo chu kỳ và có thể cần chờ vài phút trước khi dữ liệu xuất hiện đầy đủ.

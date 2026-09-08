---
title: "5.11.1 Tạo tải CPU"
weight: 1
---

Trong terminal SSH, cài công cụ stress:

```bash
sudo yum install stress -y
```

Chạy tải CPU trong 5 phút:

```bash
stress --cpu 2 --timeout 300
```

Trong thời gian chạy, CPU tăng cao và tạo điều kiện để Alarm được kích hoạt.

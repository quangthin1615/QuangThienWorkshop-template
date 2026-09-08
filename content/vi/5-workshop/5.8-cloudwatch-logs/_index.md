---
title: "5.8 CloudWatch Logs"
weight: 8
---

## Khắc phục Log Group không xuất hiện

Nếu Agent đang chạy nhưng Log Group chưa xuất hiện:

1. Kiểm tra log Agent:

```bash
sudo tail -n 30 /opt/aws/amazon-cloudwatch-agent/logs/amazon-cloudwatch-agent.log
```

2. Kiểm tra:

```bash
sudo tail -n 20 /var/log/messages
```

Trên Amazon Linux 2023, `rsyslog` không được cài sẵn nên các file `/var/log/messages` và `/var/log/secure` có thể chưa tồn tại.

3. Cài và bật rsyslog:

```bash
sudo yum install rsyslog -y
sudo systemctl enable rsyslog
sudo systemctl start rsyslog
```

4. Cấp quyền đọc cho Agent:

```bash
sudo usermod -a -G adm cwagent
sudo chmod 640 /var/log/messages /var/log/secure
sudo chgrp adm /var/log/messages /var/log/secure
```

5. Khởi động lại Agent:

```bash
sudo systemctl restart amazon-cloudwatch-agent
```

## Xác nhận log

Vào **CloudWatch Console → Log management → Log groups**.

Kiểm tra các Log Group:

- `messages`
- `secure`

Chọn Log Stream theo Instance ID để xem log gần thời gian thực.

![Hình 7. Khắc phục sự cố rsyslog](/QuangThienWorkshop-template/images/figure-07.png)

![Hình 8. Log Group messages và secure xuất hiện](/QuangThienWorkshop-template/images/figure-08.png)

![Hình 9. Log events hiển thị trong Log Stream](/QuangThienWorkshop-template/images/figure-09.png)

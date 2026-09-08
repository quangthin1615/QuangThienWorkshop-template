---
title: "Cài đặt CloudWatch Agent"
weight: 4
---

# Cài đặt & cấu hình CloudWatch Agent

## 4.1 Kết nối SSH

Trên PowerShell:

```powershell
cd $HOME\Downloads
icacls.exe .\monitoring-lab-key.pem /reset
icacls.exe .\monitoring-lab-key.pem /grant:r "$($env:USERNAME):(R)"
icacls.exe .\monitoring-lab-key.pem /inheritance:r
```

Kết nối:

```bash
ssh -i "monitoring-lab-key.pem" ec2-user@<Public-IP-cua-instance>
```

## 4.2 Cài Agent

```bash
sudo yum install amazon-cloudwatch-agent -y
rpm -q amazon-cloudwatch-agent
```

## 4.3 Cấu hình Agent

```bash
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard
```

Chọn Linux, EC2, user `cwagent`, tắt StatsD, bật host metrics (CPU/Memory/Disk), thu thập:

```text
/var/log/messages
/var/log/secure
```

Retention: 7 ngày.

Nếu wizard lỡ bật `collectd`, mở `config.json` và xoá khối `collectd`.

## 4.4 Khởi động Agent

```bash
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -s -c file:/opt/aws/amazon-cloudwatch-agent/bin/config.json
```

Kiểm tra:

```bash
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a status
```

Kỳ vọng: `status = running`.

## 4.5 Khắc phục Log Group không xuất hiện

Amazon Linux 2023 không cài sẵn `rsyslog`, nên `/var/log/messages` và `/var/log/secure` có thể chưa tồn tại.

```bash
sudo yum install rsyslog -y
sudo systemctl enable rsyslog
sudo systemctl start rsyslog
```

Cấp quyền đọc cho Agent:

```bash
sudo usermod -a -G adm cwagent
sudo chmod 640 /var/log/messages /var/log/secure
sudo chgrp adm /var/log/messages /var/log/secure
```

Khởi động lại:

```bash
sudo systemctl restart amazon-cloudwatch-agent
```

## 4.6 Xác nhận Log

Vào **CloudWatch → Log management → Log groups**.

Kiểm tra hai Log Group:

- `messages`
- `secure`

Chọn Log Stream theo Instance ID để xem log gần thời gian thực.

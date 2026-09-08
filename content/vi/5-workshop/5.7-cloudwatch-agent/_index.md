---
title: "5.7 CloudWatch Agent"
weight: 7
---

## Cài đặt Agent

Cài đặt:

```bash
sudo yum install amazon-cloudwatch-agent -y
```

Kiểm tra:

```bash
rpm -q amazon-cloudwatch-agent
```

Chạy config wizard:

```bash
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard
```

Cấu hình:

- OS: Linux
- Environment: EC2
- User: `cwagent`
- Tắt StatsD
- Bật host metrics CPU/Memory/Disk
- Thu thập `/var/log/messages`
- Thu thập `/var/log/secure`
- Retention: 7 ngày
- Không lưu config vào SSM

Nếu wizard tạo khối `collectd` trong khi CollectD chưa được cài, mở file config và xóa khối này.

```bash
sudo nano /opt/aws/amazon-cloudwatch-agent/bin/config.json
```

Khởi động Agent:

```bash
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -s -c file:/opt/aws/amazon-cloudwatch-agent/bin/config.json
```

Kiểm tra:

```bash
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a status
```

Kỳ vọng: `status = running`.

![Hình 5. Cài đặt CloudWatch Agent hoàn tất](/QuangThienWorkshop-template/images/figure-05.png)
![Hình 6. Kiểm tra trạng thái Agent: running](/QuangThienWorkshop-template/images/figure-06.png)
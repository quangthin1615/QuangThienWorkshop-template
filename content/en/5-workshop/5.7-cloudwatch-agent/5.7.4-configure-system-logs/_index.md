---
title: "5.7.4 Configure System Logs"
weight: 4
---

## Configure rsyslog

Amazon Linux 2023 may not have `/var/log/messages` and `/var/log/secure` available by default.

```bash
sudo yum install rsyslog -y
sudo systemctl enable rsyslog
sudo systemctl start rsyslog
```

Allow the CloudWatch Agent to read the logs:

```bash
sudo usermod -a -G adm cwagent
sudo chmod 640 /var/log/messages /var/log/secure
sudo chgrp adm /var/log/messages /var/log/secure
sudo systemctl restart amazon-cloudwatch-agent
```

![rsyslog configuration](/QuangThienWorkshop-template/images/figure-07.png)
*Figure 7. rsyslog installed and started successfully.*

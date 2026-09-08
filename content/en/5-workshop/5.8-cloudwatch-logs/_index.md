---
title: "5.8 CloudWatch Logs"
weight: 8
---

**## Troubleshooting: Log Group Not Appearing**

If the Agent is running but the Log Group does not appear:

1. Check the Agent log:

```bash
sudo tail -n 30 /opt/aws/amazon-cloudwatch-agent/logs/amazon-cloudwatch-agent.log
```

2. Check:

```bash
sudo tail -n 20 /var/log/messages
```

On Amazon Linux 2023, `rsyslog` is not installed by default, so the `/var/log/messages` and `/var/log/secure` files may not exist.

3. Install and enable rsyslog:

```bash
sudo yum install rsyslog -y

sudo systemctl enable rsyslog

sudo systemctl start rsyslog
```

4. Grant read permissions to the Agent:

```bash
sudo usermod -a -G adm cwagent

sudo chmod 640 /var/log/messages /var/log/secure

sudo chgrp adm /var/log/messages /var/log/secure
```

5. Restart the Agent:

```bash
sudo systemctl restart amazon-cloudwatch-agent
```

**## Verify Logs**

Go to **CloudWatch Console → Log management → Log groups**.

Check the following Log Groups:

- `messages`
- `secure`

Select the Log Stream by Instance ID to view the logs in near real time.

![Figure 7. Troubleshooting rsyslog](/QuangThienWorkshop-template/images/figure-07.png)

![Figure 8. Log Groups messages and secure appear](/QuangThienWorkshop-template/images/figure-08.png)

![Figure 9. Log events displayed in the Log Stream](/QuangThienWorkshop-template/images/figure-09.png)
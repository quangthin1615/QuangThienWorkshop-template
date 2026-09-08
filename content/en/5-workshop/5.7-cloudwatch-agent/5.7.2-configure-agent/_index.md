---
title: "5.7.2 Configure CloudWatch Agent"
weight: 2
---

## Run the Configuration Wizard

```bash
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard
```

Settings used in this lab:

- OS: Linux
- Environment: EC2
- User: `cwagent`
- StatsD: disabled
- Host metrics: enabled
- CPU, memory, and disk metrics: enabled
- Logs: `/var/log/messages` and `/var/log/secure`
- Retention: 7 days
- Do not store configuration in SSM.

![CloudWatch Agent configuration](/QuangThienWorkshop-template/images/figure-06.png)

*Figure 6. CloudWatch Agent configuration.*

---
title: "5.9 CloudWatch Alarm"
weight: 9
---

## CPU Alarm

The alarm monitors the EC2 `CPUUtilization` metric.

- Statistic: `Average`
- Period: `5 minutes`
- Threshold: greater than `70%`
- Alarm name: `High-CPU-Alarm-Monitoring-Lab`
- SNS topic: `system-alerts`

![Alarm condition](/QuangThienWorkshop-template/images/figure-10.png)

*Figure 10. CPU alarm configured with a threshold above 70%.*

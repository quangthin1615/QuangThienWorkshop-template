---
title: "5.9.1 Create CPU Alarm"
weight: 1
---

## Create the Alarm

1. Open **CloudWatch → Alarms → Create alarm**.
2. Select **Select metric**.
3. Choose **EC2 → Per-Instance Metrics**.
4. Find the monitoring instance.
5. Select `CPUUtilization`.
6. Statistic: `Average`.
7. Period: `5 minutes`.
8. Condition: **Greater than 70**.
9. Continue to configure the alarm actions.

![Alarm condition](/QuangThienWorkshop-template/images/figure-10.png)

*Figure 10. CPU alarm configured with a threshold above 70%.*

---
title: "5.10 Monitoring"

weight: 10

---

**## Checking the Monitoring System**

The system is monitored through the following workflow:

**EC2 → CloudWatch Agent → Logs / Metrics → Alarm → SNS → Email**

The components that need to be checked:

- CloudWatch Agent: `running`

- Log Groups: `messages`, `secure`

- Metric: `CPUUtilization`

- Alarm: `High-CPU-Alarm-Monitoring-Lab`

- SNS Topic: `system-alerts`

The objective is to confirm that data from EC2 is collected and that the Alarm can respond when CPU utilization increases significantly.
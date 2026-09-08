---
title: "5.9.2 Configure SNS Notification"
weight: 2
---

## Create the SNS Topic

1. Set the alarm trigger to **In alarm**.
2. Select **Create new topic**.
3. Topic name: `system-alerts`.
4. Enter the email address that will receive notifications.
5. Create the topic.
6. Open the confirmation email from AWS.
7. Select **Confirm subscription**.
8. Set the alarm name to `High-CPU-Alarm-Monitoring-Lab`.
9. Review and create the alarm.

## Result

The SNS subscription is confirmed and the alarm is connected to the notification topic.

![SNS configuration](/QuangThienWorkshop-template/images/figure-11.png)

*Figure 11. SNS topic configured for the CloudWatch Alarm.*

![Subscription confirmed](/QuangThienWorkshop-template/images/figure-12.png)

*Figure 12. SNS email subscription confirmed.*

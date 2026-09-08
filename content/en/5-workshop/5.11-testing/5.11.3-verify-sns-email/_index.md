---
title: "5.11.3 Check SNS"
weight: 3
---

After the Alarm changes to `In alarm`:

1. Open the registered email inbox.
2. Check the alert email from AWS Notification.
3. Confirm that the email contains Alarm Details and Reason.
4. Check the time when the Alarm changed state.

Example of the actual alert content:

```text
State Change: OK -> ALARM
Reason: Threshold Crossed
[100.0] was greater than the threshold (70.0)
```

![Figure 14. Actual alert email received from SNS](/QuangThienWorkshop-template/images/figure-14.png)
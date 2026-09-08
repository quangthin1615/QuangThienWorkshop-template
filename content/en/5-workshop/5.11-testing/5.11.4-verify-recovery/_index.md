---
title: "5.11.4 Check Alarm Returns to OK"

weight: 4

---

**## Check Alarm Returns to OK Status**

After the `stress` command ends after 300 seconds:

1. CPU gradually decreases.

2. Continue observing the Alarm on CloudWatch.

3. Confirm that the Alarm status changes from `In alarm` → `OK`.

4. Check the CPU chart showing the process of increasing load and then decreasing load.

**## Actual Result**

The Alarm returns to `OK` status, demonstrating that the recovery mechanism works correctly.

**## Actual Evidence**

![Figure 15. Alarm returns to OK after stopping the load](/QuangThienWorkshop-template/images/figure-15.png)

*Figure 15. Alarm returns to OK after stopping the load*
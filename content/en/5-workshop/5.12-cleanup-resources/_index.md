---
title: "5.12 Cleanup Resources"
weight: 12
---

## Cleanup

After completing the workshop, stop the EC2 instance to avoid unnecessary charges.

1. Open **EC2 → Instances**.
2. Select `Monitoring-Lab-Instance`.
3. Select **Instance state → Stop instance**.
4. Confirm the stop operation.

CloudWatch resources can be removed when they are no longer required.

## Cost Control

For a learning lab, resources should be stopped or deleted immediately after testing. In the actual lab, the EC2 instance was stopped after the test to minimize costs.

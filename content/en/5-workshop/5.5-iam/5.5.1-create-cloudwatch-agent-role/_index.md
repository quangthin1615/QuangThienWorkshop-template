---
title: "5.5.1 Create CloudWatch Agent Role"
weight: 1
---

## Create the IAM Role

1. Open **IAM Console → Roles**.
2. Select **Create role**.
3. Trusted entity type: **AWS service**.
4. Use case: **EC2**.
5. Add `CloudWatchAgentServerPolicy`.
6. Role name: `EC2-CloudWatchAgent-Role`.
7. Review and create the role.

## Result

The IAM role is created and can be attached to the EC2 instance.

![IAM Role](/QuangThienWorkshop-template/images/figure-01.png)

*Figure 1. IAM Role `EC2-CloudWatchAgent-Role` created successfully.*
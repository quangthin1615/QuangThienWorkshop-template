---
title: "5.6.1 Launch EC2"
weight: 1
---

## Launch the EC2 Instance

1. Open **EC2 → Instances → Launch instance**.
2. Name the instance `Monitoring-Lab-Instance`.
3. Select **Amazon Linux 2023**.
4. Select `t3.micro`.
5. Create key pair `monitoring-lab-key.pem`.
6. Select the Default VPC and `public-subnet-monitoring`.
7. Enable auto-assign public IPv4.
8. Allow SSH from My IP.
9. Select `EC2-CloudWatchAgent-Role` as the IAM instance profile.
10. Launch the instance.

## Result

The EC2 instance changes to `Running` and passes the status checks.

![EC2 instance](/QuangThienWorkshop-template/images/figure-02.png)

*Figure 2. EC2 instance launched successfully.*

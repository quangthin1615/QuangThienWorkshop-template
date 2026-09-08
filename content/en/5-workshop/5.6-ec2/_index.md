---
title: "5.6 EC2"
weight: 6
---

## EC2 Deployment

An EC2 instance is used as the monitoring target.

- Name: `Monitoring-Lab-Instance`
- AMI: Amazon Linux 2023
- Instance type: `t3.micro`
- Region: `ap-southeast-2`
- Subnet: `public-subnet-monitoring`
- IAM role: `EC2-CloudWatchAgent-Role`

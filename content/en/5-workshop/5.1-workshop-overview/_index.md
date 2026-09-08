---
title: "5.1 Workshop Overview"
weight: 1
---

## Objective

The objective of this workshop is to build and verify a practical AWS monitoring system for an EC2 instance.

The system collects system logs and performance metrics, monitors CPU utilization, detects high CPU usage through a CloudWatch Alarm, and sends an email notification through Amazon SNS.

## Monitoring Architecture

**EC2 → CloudWatch Agent → CloudWatch Logs / Metrics → CloudWatch Alarm → SNS → Email**

## AWS Services Used

- **Amazon EC2:** provides the monitored Linux server.
- **AWS IAM:** provides permissions for the CloudWatch Agent.
- **Amazon VPC:** provides the network environment.
- **Amazon CloudWatch:** collects logs and metrics and evaluates alarms.
- **Amazon SNS:** sends email notifications when the alarm changes state.

## Expected Result

1. Collect system logs from EC2.
2. Publish CPU metrics to CloudWatch.
3. Detect CPU utilization above 70%.
4. Change the alarm from `OK` to `In alarm`.
5. Send an SNS email notification.
6. Return the alarm from `In alarm` to `OK` after CPU usage decreases.

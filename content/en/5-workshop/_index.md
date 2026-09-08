---
title: "5. Workshop"
weight: 5
---

# AWS Monitoring Workshop

This workshop builds and tests a basic monitoring system for an Amazon EC2 instance.

Monitoring flow:

**EC2 Instance → CloudWatch Agent → CloudWatch Logs / Metrics → CloudWatch Alarm → SNS → Email**

The workshop includes IAM configuration, VPC/Subnet/Security Group configuration, EC2 deployment, CloudWatch Agent installation, log collection, CPU monitoring, alarm configuration, SNS email notifications, recovery testing, and resource cleanup.

## Overall Architecture Diagram

The following diagram describes the AWS architecture actually deployed during the workshop:

![Overall AWS architecture diagram](/QuangThienWorkshop-template/images/anh.png)

*Figure 1. Overall AWS architecture*

## Operation Flow

1. **USER** accesses the AWS environment through the Internet.

2. **Internet Gateway** provides Internet connectivity to the VPC.

3. **VPC** uses the CIDR `10.0.0.0/16`.

4. **Public Subnet** uses the CIDR `10.0.1.0/24`.

5. **EC2** is deployed inside the Public Subnet.

6. **Security Group** controls inbound and outbound traffic to the EC2 instance.

7. **IAM Role** provides the permissions required for EC2 to send monitoring data to CloudWatch.

8. **CloudWatch Metrics** receives monitoring metrics, including CPU Utilization.

9. **CloudWatch Logs** stores logs collected from the EC2 instance.

10. **CloudWatch Alarm** monitors CPU utilization and detects when the CPU exceeds the configured threshold.

11. **SNS** receives notifications from the CloudWatch Alarm.

12. **Email** receives alert notifications from SNS.

## Actual Deployment Environment

- **Region:** `ap-southeast-2` (Sydney)
- **EC2:** Amazon Linux 2023, `t3.micro`
- **Instance Name:** `Monitoring-Lab-Instance`
- **IAM Role:** `EC2-CloudWatchAgent-Role`
- **Log Groups:** `messages`, `secure`
- **Alarm:** `High-CPU-Alarm-Monitoring-Lab`
- **SNS Topic:** `system-alerts`
- **Log Retention:** 7 days

## Results

The main testing scenarios were successfully completed:

- CloudWatch Agent was successfully installed and running.
- Logs were successfully sent to CloudWatch Logs.
- CloudWatch Metrics successfully received monitoring data.
- The CloudWatch Alarm changed its state when CPU utilization exceeded the configured threshold.
- SNS successfully sent an email notification.
- The alarm returned to `OK` after the CPU load was stopped.

The workshop successfully achieved its objective of building a monitoring workflow for Amazon EC2:

**Monitoring → Detection → Alerting → Recovery**

This demonstrates a basic but practical AWS monitoring solution that can be used to monitor EC2 resources and detect abnormal CPU utilization.
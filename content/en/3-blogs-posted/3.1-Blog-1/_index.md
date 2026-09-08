---
title: "Monitoring Amazon EC2 with Amazon CloudWatch and Automated Alarms"
weight: 1
---


## 1. Overview

Running an Amazon EC2 instance does not automatically mean that the application is healthy. CPU utilization can spike, network traffic can become abnormal, or resources can approach capacity limits.

Amazon CloudWatch provides metric collection, visualization, dashboards, and CloudWatch Alarms. Common EC2 metrics include CPUUtilization, NetworkIn, NetworkOut, DiskReadOps, and DiskWriteOps.

![EC2 and CloudWatch architecture](/images/blog1-01-ec2-cloudwatch.png)

## 2. Architecture

The basic flow is:

**Amazon EC2 → CloudWatch Metrics → CloudWatch Dashboard/Alarm → notification or operational action**

EC2 produces metrics and CloudWatch stores them for monitoring. An alarm evaluates the configured condition and changes state when the condition is met.

![EC2 metrics to CloudWatch](/images/blog1-02-cloudwatch-metric.png)

## 3. Monitoring CPU

CPUUtilization is a useful starting metric. Sustained CPU utilization above 80% may indicate increased workload or an application issue.

Charts help identify normal levels, traffic spikes, abnormal behavior, and long-term trends. Thresholds should be based on the actual workload.

## 4. CloudWatch Alarm

A simple alarm can use:

- Metric: EC2 CPUUtilization
- Statistic: Average
- Period: 5 minutes
- Threshold: greater than 80%
- Action: send an SNS notification

When the condition is met, the alarm enters **ALARM**. When the metric returns to a safe range, it can return to **OK**.

![CloudWatch Alarm](/images/blog1-03-cloudwatch-alarm.png)

## 5. Practical example

A web server normally runs at 20–40% CPU. During a traffic spike, CPU rises above 80%.

Workflow:

1. EC2 produces high CPU utilization.
2. CloudWatch records the metric.
3. The alarm evaluates the condition.
4. The alarm enters ALARM.
5. SNS can notify the administrator.
6. The administrator checks the application and logs.
7. When load decreases, the alarm returns to OK.

## 6. Key takeaway

Monitoring is not only about viewing graphs. The value comes from turning metrics into actionable information through **monitor → detect → alert → respond**.

## 7. References

- [AWS News Blog – Amazon CloudWatch – Alarm Actions](https://aws.amazon.com/blogs/aws/amazon-cloudwatch-alarm-actions/)

- [AWS Compute Blog – Automating Amazon EC2-Windows EBS Volumes monitoring and creating alarms](https://aws.amazon.com/blogs/compute/automating-amazon-ec2-windows-ebs-volumes-monitoring-and-creating-alarms/)
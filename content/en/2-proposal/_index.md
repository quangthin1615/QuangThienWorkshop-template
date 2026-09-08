---
title: "2. Proposal"

weight: 2

---


# AWS Monitoring & Alerting System

## Architecture for Monitoring and Alerting Amazon EC2 on AWS

### 1. Executive Summary

This proposal presents a solution for building a **basic monitoring and alerting system for Amazon EC2** on the AWS platform. The goal of the system is to monitor the operating status of an EC2 instance, collect monitoring information and system logs, detect cases where CPU usage exceeds the allowed threshold, and send alerts to the administrator.

The system uses AWS services including **Amazon EC2, Amazon CloudWatch, CloudWatch Agent, Amazon SNS, IAM, and Amazon VPC**. EC2 acts as the server to be monitored. CloudWatch Agent is installed on EC2 to collect system logs and monitoring information. CloudWatch is responsible for storing metrics, logs, and monitoring the system status through Alarms. When CPU exceeds the configured threshold, the CloudWatch Alarm changes from `OK` to `In alarm` and sends a notification through Amazon SNS to the administrator's email.

The entire process is designed according to the following model:

**EC2 → CloudWatch Agent → CloudWatch Metrics / Logs → CloudWatch Alarm → SNS → Email**

The solution helps build a complete process from **monitoring → detection → alerting → recovery**, while helping the intern understand how to deploy a basic monitoring system on AWS.

---

### 2. Problem Statement

#### Current Problems

- **Difficulty monitoring server status**: When a system has multiple EC2 instances, manually checking CPU, memory, and logs on each server takes a lot of time.
- **Failure to detect overload conditions promptly**: If the CPU of an EC2 instance remains high for a long time without an alerting system, the administrator may not detect the problem in time.
- **Logs distributed across servers**: System logs are stored directly on EC2, making remote inspection and monitoring difficult.
- **Lack of automatic alerting mechanisms**: When a problem occurs, the system does not automatically send notifications to the administrator.
- **Difficulty checking the recovery process**: Without monitoring and Alarms, it is difficult to accurately determine when the system returns to normal status.

#### Proposed Solution

The system is designed based on the principle of **centralizing monitoring and alerting on Amazon CloudWatch**.

The architecture includes the following main components:

1. **EC2 Instance**: Runs Amazon Linux 2023 and acts as the server to be monitored.
2. **IAM Role**: Provides the necessary permissions for EC2 to send monitoring data and logs to CloudWatch.
3. **CloudWatch Agent**: Installed on EC2 to collect system logs and monitoring data.
4. **CloudWatch Metrics**: Monitors EC2 operating metrics, including CPU Utilization.
5. **CloudWatch Logs**: Centralizes and stores logs from EC2.
6. **CloudWatch Alarm**: Monitors CPU and detects when CPU exceeds the 70% threshold.
7. **Amazon SNS**: Receives notifications from CloudWatch Alarm and sends alerts.
8. **Email**: Receives alert notifications from SNS.

#### Benefits

- **Centralized monitoring**: EC2 metrics and logs are monitored on CloudWatch.
- **Automatic alerting**: CloudWatch Alarm automatically detects when CPU exceeds the threshold.
- **Fast notification**: SNS sends alerts directly to email.
- **Recovery monitoring**: The Alarm can be confirmed to change from `In alarm` back to `OK`.
- **Easy deployment and scalability**: The model can be applied to multiple EC2 instances and expanded with additional types of metrics.

---

### 3. Solution Architecture

#### Overall Architecture Diagram

![Overall AWS architecture diagram](/QuangThienWorkshop-template/images/anh.png)

#### Details of the Components in the Architecture

##### 1. Amazon VPC & Public Subnet

The EC2 instance is deployed in an **Amazon VPC** and Public Subnet to allow Internet connectivity for administration and practical activities.

Actual environment:

- **VPC:** `vpc-05c77177c5e1b6477`
- **Subnet:** `public-subnet-monitoring`
- **Subnet CIDR:** `172.31.0.0/20`
- **Availability Zone:** `ap-southeast-2a`

##### 2. Security Group

The Security Group is used to control traffic to the EC2 instance.

Main configuration:

- **Inbound:** SSH TCP port `22` from My IP.
- **Outbound:** Allows EC2 to connect externally for installation and sending monitoring data.

##### 3. Amazon EC2

EC2 is the main server used to perform the monitoring lab.

Deployment information:

- **Instance name:** `Monitoring-Lab-Instance`
- **Instance type:** `t3.micro`
- **Operating System:** Amazon Linux 2023
- **Region:** `ap-southeast-2` (Sydney)

##### 4. IAM Role

The IAM Role `EC2-CloudWatchAgent-Role` is attached to the EC2 instance to provide permissions for CloudWatch Agent to send monitoring data and logs to CloudWatch.

Main policy:

`CloudWatchAgentServerPolicy`

##### 5. CloudWatch Agent

CloudWatch Agent is installed directly on the EC2 instance.

The Agent is responsible for collecting monitoring data and system logs, then sending the data to Amazon CloudWatch.

Version used:

`1.300069.1`

##### 6. CloudWatch Metrics

CloudWatch Metrics is used to monitor EC2 operating metrics.

The most important metric in the workshop is:

`CPUUtilization`

This metric is used as the basis for creating the CloudWatch Alarm.

##### 7. CloudWatch Logs

CloudWatch Logs is used to centralize logs from EC2.

Log Groups used:

- `messages`
- `secure`

Log retention period:

**7 days**

##### 8. CloudWatch Alarm

CloudWatch Alarm is configured to monitor CPU Utilization.

Alarm:

`High-CPU-Alarm-Monitoring-Lab`

Threshold:

**CPU > 70% for 5 minutes**

When CPU exceeds the threshold, the Alarm changes status:

`OK → In alarm`

When CPU decreases back to normal:

`In alarm → OK`

##### 9. Amazon SNS

Amazon SNS is used to send notifications when the CloudWatch Alarm changes state.

SNS Topic:

`system-alerts`

SNS sends alert emails to the registered email address and confirms the subscription.

---

### 4. Technical Implementation

#### Implementation Stages

1. **Stage 1: Prepare the AWS Environment**
   - Create or use an Amazon VPC.
   - Identify the Public Subnet.
   - Configure the Security Group.
   - Prepare IAM permissions for EC2.

2. **Stage 2: Deploy Amazon EC2**
   - Create an EC2 instance.
   - Use Amazon Linux 2023.
   - Select instance type `t3.micro`.
   - Attach the IAM Role `EC2-CloudWatchAgent-Role`.
   - Check the EC2 status after launch.

3. **Stage 3: Install CloudWatch Agent**
   - Connect to EC2 through SSH.
   - Install CloudWatch Agent.
   - Check the Agent version.
   - Create and configure the configuration file.
   - Start CloudWatch Agent.
   - Check the Agent status.

4. **Stage 4: Configure CloudWatch Logs**
   - Configure the Agent to collect system logs.
   - Send logs from EC2 to CloudWatch Logs.
   - Check the `messages` Log Group.
   - Check the `secure` Log Group.
   - Check the log events.

5. **Stage 5: Configure CloudWatch Alarm**
   - Select the `CPUUtilization` metric.
   - Set the CPU threshold above 70%.
   - Configure the evaluation period to 5 minutes.
   - Name the Alarm `High-CPU-Alarm-Monitoring-Lab`.
   - Check the initial Alarm status.

6. **Stage 6: Configure Amazon SNS**
   - Create the SNS Topic `system-alerts`.
   - Create an email subscription.
   - Confirm the subscription.
   - Link SNS with the CloudWatch Alarm.
   - Check the ability to receive alert emails.

7. **Stage 7: Test the System**
   - Create CPU load using the `stress` tool.
   - Monitor CPU Utilization.
   - Check the Alarm changes to `In alarm`.
   - Check SNS sends an email.
   - Stop the CPU load.
   - Check CPU decreases to normal.
   - Confirm the Alarm returns to `OK`.

#### Technical & Security Requirements

- **IAM Role**: EC2 uses an IAM Role to access the required AWS services instead of storing Access Keys directly on the server.
- **Security Group**: Only allows SSH TCP port `22` from the administrator's IP address.
- **CloudWatch Monitoring**: Monitors the EC2 operating status through metrics and logs.
- **SNS Notification**: Only uses the confirmed email subscription to receive alerts.
- **Resource Cleanup**: Stops EC2 after completing the workshop to avoid unnecessary costs.

---

### 5. Implementation Roadmap & Milestones

```text
+--------------------------------------------------------------------------------+
| Stage 1: Prepare the AWS Environment                                            |
|   - Identify VPC, Public Subnet and Security Group                             |
|   - Prepare IAM Role                                                           |
+--------------------------------------------------------------------------------+
                                  |
                                  v
+--------------------------------------------------------------------------------+
| Stage 2: Deploy EC2                                                             |
|   - Create Monitoring-Lab-Instance                                             |
|   - Configure Amazon Linux 2023 and SSH                                       |
+--------------------------------------------------------------------------------+
                                  |
                                  v
+--------------------------------------------------------------------------------+
| Stage 3: Configure CloudWatch Agent                                             |
|   - Install CloudWatch Agent                                                   |
|   - Configure Metrics and Logs                                                  |
|   - Check Agent operation                                                      |
+--------------------------------------------------------------------------------+
                                  |
                                  v
+--------------------------------------------------------------------------------+
| Stage 4: Configure CloudWatch & SNS                                             |
|   - Create CloudWatch Alarm                                                    |
|   - Configure CPU threshold > 70%                                              |
|   - Create SNS Topic and Email Subscription                                    |
+--------------------------------------------------------------------------------+
                                  |
                                  v
+--------------------------------------------------------------------------------+
| Stage 5: Testing & Recovery                                                     |
|   - Create CPU load                                                           |
|   - Check Alarm changes to In alarm                                            |
|   - Check SNS email                                                            |
|   - Stop the load and confirm Alarm returns to OK                              |
+--------------------------------------------------------------------------------+
```

---

### 6. Budget Estimation

The workshop is designed in a **simple and cost-effective** way, using the AWS resources necessary for practical purposes.

| **AWS Service** | **Estimated Configuration / Scale** | **Estimated Cost** |
|---|---|---|
| **Amazon EC2** | `t3.micro`, used during the practical session | Depends on usage time |
| **Amazon CloudWatch** | Metrics, Logs and Alarm | Depends on usage |
| **CloudWatch Agent** | Installed on EC2 | No separate charge |
| **Amazon SNS** | 1 Topic + Email Subscription | Low cost / depends on usage |
| **Amazon VPC** | VPC and Public Subnet | No separate charge for VPC/Subnet |
| **Security Group** | SSH TCP/22 | No separate charge |
| **IAM Role** | `EC2-CloudWatchAgent-Role` | No separate charge |

> **Cost Optimization Points**:
>
> 1. Use the `t3.micro` instance type suitable for the practical environment.
> 2. Only run EC2 when necessary.
> 3. Stop EC2 after completing the tests.
> 4. Configure CloudWatch Logs retention to 7 days.
> 5. Monitor AWS Billing to control incurred costs.

---

### 7. Risk Assessment

#### Risk Matrix & Mitigation Strategies

| **Potential Risk** | **Impact Level** | **Probability** | **Mitigation Strategy** |
|---|---|---|---|
| **EC2 cannot connect through SSH** | Medium | Medium | Check Public IP, Security Group and TCP port 22 access permissions. |
| **CloudWatch Agent does not work** | High | Low | Check service status, configuration and the IAM Role of EC2. |
| **Log Group does not appear** | Medium | Medium | Check the CloudWatch Agent configuration and `CloudWatchAgentServerPolicy` permissions. |
| **CPU does not exceed the Alarm threshold** | Medium | Low | Use the `stress` tool to create CPU load and check the metric again. |
| **SNS does not send email** | High | Low | Check that the SNS subscription has been confirmed and check the Alarm Action configuration. |
| **Alarm does not return to OK** | Medium | Low | Stop the CPU load process and continue monitoring CPU Utilization. |
| **AWS costs are incurred** | Medium | Medium | Stop EC2 and check resources after completing the workshop. |

---

### 8. Expected Results

- **Successfully build the monitoring system**: Deploy a basic monitoring system for Amazon EC2 using CloudWatch.
- **Collect metrics and logs**: CloudWatch Agent sends monitoring data and logs from EC2 to CloudWatch.
- **Detect high CPU conditions**: CloudWatch Alarm detects when CPU exceeds the 70% threshold.
- **Automatic alerting**: Amazon SNS sends an email when the Alarm changes to `In alarm`.
- **Check recovery**: The Alarm changes from `In alarm` back to `OK` after CPU decreases.
- **Improve AWS knowledge**: Understand how to combine IAM, VPC, EC2, CloudWatch and SNS to build a practical monitoring system.
- **Optimize costs**: Use resources appropriately for the practical environment and perform cleanup after completion.

The final goal of the workshop is to successfully build and test the following process:

**Monitoring → Detection → Alerting → Recovery**

thereby demonstrating that the system can **monitor, detect incidents, send alerts, and confirm system recovery** in the AWS environment.
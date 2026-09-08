---

title: "3-Blogs-Posted"
weight: 3

---

During my internship, I studied and summarized **three technical blog topics related to Amazon Web Services (AWS)**, focusing on **system monitoring, networking, and serverless event-driven architectures**. These topics helped strengthen my practical understanding of deploying, securing, and operating workloads on AWS.

| **#** | **Topic** | **Category** | **Publication Date** |
|---|---|---|---|
| Blog 1 | **Monitoring Amazon EC2 with Amazon CloudWatch and Configuring Alarms** | Monitoring & Operations | |
| Blog 2 | **Connecting Amazon S3 from a VPC using VPC Endpoints** | Networking & Security | |
| Blog 3 | **Building Event-Driven Architectures with Amazon SQS and AWS Lambda** | Serverless & Event-Driven Architecture | |

---

### [3.1 Blog 1 – Monitoring Amazon EC2 with Amazon CloudWatch](3.1-blog1/)

Amazon EC2 is one of the most widely used compute services on AWS. When running EC2 instances in a production environment, monitoring system performance is important for identifying potential issues early.

This blog explains how to use **Amazon CloudWatch** to collect and monitor EC2 metrics such as **CPU Utilization**, and how to configure a **CloudWatch Alarm** to automatically detect when CPU utilization exceeds a defined threshold.

The monitoring architecture can be described as:

**Amazon EC2 → Amazon CloudWatch → CloudWatch Alarm → Notification**

CloudWatch allows administrators to monitor system performance, create dashboards, and configure alarms when workloads show abnormal behavior.

The blog also presents a practical testing scenario: generating CPU load on an EC2 instance, observing the metric in CloudWatch, verifying that the alarm changes to **In alarm**, and finally reducing the CPU load to confirm that the alarm returns to **OK**.

---

### [3.2 Blog 2 – Connecting Amazon S3 from a VPC using VPC Endpoints](3.2-blog2/)

Workloads running inside an **Amazon VPC** often need to access Amazon S3 for storing and retrieving data. However, for architectures with strict security requirements, sending traffic through the public Internet may not be the preferred approach.

**Amazon VPC Endpoint** provides private connectivity between a VPC and supported AWS services.

This blog focuses on two major endpoint models:

- **Gateway VPC Endpoint**
- **Interface VPC Endpoint**

With a Gateway Endpoint, the VPC route table is configured so that traffic destined for Amazon S3 is routed through the endpoint instead of requiring an Internet Gateway or NAT Gateway.

The architecture is:

**EC2 Private Subnet → Route Table → S3 Gateway Endpoint → Amazon S3**

Gateway Endpoints are simple to configure, suitable for workloads running inside a VPC, and can be combined with **Endpoint Policies** to control access.

The blog also explains **Interface Endpoints**, which are based on AWS PrivateLink. An Interface Endpoint creates an Elastic Network Interface with a private IP address inside selected subnets, allowing workloads to connect to supported services through private networking.

This comparison helps clarify how to select an appropriate VPC Endpoint architecture based on **networking, security, connectivity, and cost requirements**.

---

### [3.3 Blog 3 – Building Event-Driven Architectures with Amazon SQS and AWS Lambda](3.3-blog3/)

In modern cloud architectures, an **event-driven architecture** allows different components of a system to operate independently while providing better scalability.

This blog explains how to combine **Amazon SQS** and **AWS Lambda** to build an asynchronous processing system.

The overall architecture is:

**Application → Amazon SQS → AWS Lambda → Processing**

Instead of directly calling the processing service, the application sends messages to Amazon SQS. Lambda then retrieves messages from the queue and processes them automatically.

This architecture provides several benefits:

- Reduces direct dependencies between services.
- Handles workload spikes more effectively.
- Allows Lambda to automatically scale execution.
- Amazon SQS buffers messages during traffic spikes.
- Processing speed can be controlled through concurrency configuration.

The blog also explores **AWS Lambda scaling and concurrency when Amazon SQS is used as an event source**, including improvements to polling and Lambda scale-up behavior for event-driven workloads.

This pattern is suitable for applications requiring **background jobs, asynchronous processing, queue-based workloads, and serverless architectures**.

---

## Summary

The three blog topics cover three important aspects of building systems on AWS:

1. **CloudWatch** – system monitoring and alerting.
2. **VPC Endpoint** – private connectivity and improved security.
3. **SQS + Lambda** – serverless event-driven architecture.

Studying these topics provided practical knowledge of **AWS Cloud, Networking, Monitoring, Security, and Serverless Architecture**.
---
title: "Connecting Amazon S3 from a VPC with VPC Endpoints"
weight: 2
---


## 1. Overview

Workloads inside an Amazon VPC often need to read or write data in Amazon S3. A VPC endpoint provides a private entry point from the VPC to supported AWS services.

For S3, two important choices are **Gateway VPC Endpoints** and **Interface VPC Endpoints**.

![VPC to S3](/images/blog2-01-vpc-s3.png)

## 2. Gateway VPC Endpoint

A gateway endpoint is a common choice for workloads inside a VPC accessing S3 in the Region. The route table directs S3 traffic through the endpoint.

An Internet Gateway or NAT Gateway is not required solely for S3 access.

![Gateway VPC Endpoint](/images/blog2-02-gateway-endpoint.png)

Advantages:
- simple;
- suitable for EC2 inside a VPC;
- supports endpoint policies;
- generally cost-efficient.

## 3. Interface VPC Endpoint

An interface endpoint uses AWS PrivateLink. AWS creates an Elastic Network Interface with a private IP address in the selected subnet.

Workloads connect to the private IP and traffic remains on the AWS network.

![Interface VPC Endpoint](/images/blog2-03-interface-endpoint.png)

This is useful for broader private connectivity requirements, including architectures involving on-premises environments and PrivateLink.

## 4. Comparison

| Criteria | Gateway Endpoint | Interface Endpoint |
|---|---|---|
| Technology | Route table | AWS PrivateLink |
| S3 | Yes | Yes |
| Main component | Route table | ENI/private IP |
| Typical use | VPC workloads | PrivateLink/private connectivity |
| Cost profile | Usually more cost-efficient | Endpoint and data processing charges |

## 5. Security

Private connectivity does not automatically provide unrestricted access. A strong design can combine IAM policies, S3 bucket policies, endpoint policies, and least-privilege access. Security groups are also important for interface endpoints.

## 6. Example

**EC2 private subnet → Route Table → S3 Gateway Endpoint → Amazon S3**

The EC2 instance does not need a public IP or NAT Gateway solely for S3 access.

## 7. Key takeaway

VPC endpoints are an important building block for private-by-design AWS networking. Gateway endpoints are commonly suitable for VPC workloads accessing S3, while interface endpoints support broader PrivateLink requirements.

## 8. References

1. [Choosing Your VPC Endpoint Strategy for Amazon S3 – AWS Architecture Blog](https://aws.amazon.com/blogs/architecture/choosing-your-vpc-endpoint-strategy-for-amazon-s3/)

2. [Reduce Cost and Increase Security with Amazon VPC Endpoints – AWS Architecture Blog](https://aws.amazon.com/blogs/architecture/reduce-cost-and-increase-security-with-amazon-vpc-endpoints/)

3. [Introducing private DNS support for Amazon S3 with AWS PrivateLink – AWS Storage Blog](https://aws.amazon.com/blogs/storage/introducing-private-dns-support-for-amazon-s3-with-aws-privatelink/)

---
title: "5.4.2 Create Public Subnet"
weight: 2
---

## Create the Public Subnet

1. Open **VPC Console → Subnets → Create subnet**.
2. Select the Default VPC.
3. Subnet name: `public-subnet-monitoring`.
4. Availability Zone: `ap-southeast-2a`.
5. IPv4 CIDR: `172.31.0.0/20`.
6. Create the subnet.
7. Enable **Auto-assign public IPv4 address**.

## Result

The public subnet is ready for the EC2 monitoring instance.

![Public subnet](/QuangThienWorkshop-template/images/figure-03.png)

*Figure 3. Public subnet prepared for the monitoring instance.*

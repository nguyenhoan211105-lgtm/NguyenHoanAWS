---
title: "Creating the NAT Gateway"
date: 2026-07-21
weight: 4
chapter: false
pre: " <b> 5.2.4. </b> "
---

# 5.2.4. Creating the NAT Gateway

The NAT Gateway allows instances in the private subnets to reach the internet (e.g. to download OS updates) without being directly reachable from it.

1. In the VPC console, go to **NAT Gateways** > **Create NAT gateway**.
   ![vpc_natGW](/images/5-Workshop/5.2-vpc-network/vpc_NAT.png)
2. **Name**: `my-natGW-01`.
3. **Subnet**: select `public-subnet-01`.
4. **Connectivity type**: Public.
5. Click **Allocate Elastic IP** to assign a new Elastic IP.
6. Click **Create NAT gateway**.
   ![vpc_natGW](/images/5-Workshop/5.2-vpc-network/vpc_NAT_create.png)
7. Repeat the process to create another one named `my-natGW-02` in `public-subnet-02`.

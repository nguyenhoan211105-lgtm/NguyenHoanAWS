---
title: "Configuring Route Tables"
date: 2026-07-21
weight: 5
chapter: false
pre: " <b> 5.2.5. </b> "
---

# 5.2.5. Configuring Route Tables

Create **3 route tables**: one for public subnets (routes to the Internet Gateway) and two for private subnets (routes to the NAT Gateway).

1. In the VPC console, go to **Route Tables** > **Create route table**.
   ![vpc_RTB](/images/5-Workshop/5.2-vpc-network/vpc_RTB.png)
2. **Public route table**:
   * Add name `my-public-rtb`. select `my-vpc-01`
   * ![vpc_RTB](/images/5-Workshop/5.2-vpc-network/vpc_RTB_create.png)
   * Add route `0.0.0.0/0` → Target: `my-igw-01`.
   * ![vpc_RTB](/images/5-Workshop/5.2-vpc-network/RTB_route_01.png)
   * ![vpc_RTB](/images/5-Workshop/5.2-vpc-network/RTB_route_02.png)
   * Under **Subnet associations**, associate `public-subnet-01` and `public-subnet-02`.
   * ![vpc_RTB](/images/5-Workshop/5.2-vpc-network/RTB_associations_01.png)
   * ![vpc_RTB](/images/5-Workshop/5.2-vpc-network/RTB_associations_02.png)
1. **Private route table 1**:
   * Add name `my-private-rtb-01`.
   * Add route `0.0.0.0/0` → Target: `my-natGW-01`.
   * ![vpc_RTB](/images/5-Workshop/5.2-vpc-network/vpc_RTB_create_02.png)
   * Under **Subnet associations**, associate `private-subnet-01`.
   * ![vpc_RTB](/images/5-Workshop/5.2-vpc-network/RTB_associations_03.png)
2. **Private route table 2**:
   * Add name `my-private-rtb-02`.
   * ![vpc_RTB](/images/5-Workshop/5.2-vpc-network/RTB_route_3.png)
   * Add route `0.0.0.0/0` → Target: `my-natGW-02`.
   * Under **Subnet associations**, associate `private-subnet-02`.
   * ![vpc_RTB](/images/5-Workshop/5.2-vpc-network/RTB_associations_3.png)
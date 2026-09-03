---
title: "Creating Subnets Across Two Availability Zones"
date: 2026-07-21
weight: 2
chapter: false
pre: " <b> 5.2.2. </b> "
---

# 5.2.2. Creating Subnets Across Two Availability Zones

Create **4 subnets** — 2 public and 2 private — across two Availability Zones to ensure high availability:

| Subnet Name | AZ | CIDR Block | Type |
| :--- | :--- | :--- | :--- |
| `public-subnet-01` | us-east-1a | `10.0.0.0/20` | Public |
| `public-subnet-02` | us-east-1b | `10.0.16.0/20` | Public |
| `private-subnet-01` | us-east-1a | `10.0.32.0/20` | Private |
| `private-subnet-02` | us-east-1b | `10.0.48.0/20` | Private |

1. In the VPC Console, go to **Subnets** > **Create subnet**.
   ![vpc_subnet](/images/5-Workshop/5.2-vpc-network/vpc_subnet.png)
   ![vpc_subnet](/images/5-Workshop/5.2-vpc-network/vpc_subnet_create_2.png)
2. Configure the subnet:
   * Select the VPC `my-vpc-01`.
   * Enter the subnet name: `public-subnet-01`
   * Select the Availability Zone: `us-east-1a`
   * Enter the IPv4 subnet CIDR block: `10.0.0.0/20`
   * Select **Add new subnet** to add another subnet.
3. Add all **4 subnets** listed above using their corresponding Availability Zones and CIDR blocks.
4. Click **Create subnet**.
5. For the **2 public subnets**, go to **Actions** > **Edit subnet settings** and enable **Auto-assign public IPv4 address**.
   ![vpc_subnet](/images/5-Workshop/5.2-vpc-network/vpc_subnet_setting_01.png)

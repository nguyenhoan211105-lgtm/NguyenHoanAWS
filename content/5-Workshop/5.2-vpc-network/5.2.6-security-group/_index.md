---
title: "Configuring Security Groups"
date: 2026-07-21
weight: 6
chapter: false
pre: " <b> 5.2.6. </b> "
---

# 5.2.6. Configuring Security Groups

Create the following Security Groups (least-privilege — each tier only accepts traffic from the tier in front of it):

| Security Group | Inbound Rule | Source |
| :--- | :--- | :--- |
| `my-public-sg` | HTTP (80), HTTPS (443), SSH (22) | `0.0.0.0/0` (HTTP, HTTPS), `my-ip` (SSH) |
| `my-private-sg` | Custom TCP (8080), HTTP (80), SSH (22) | `my-public-sg`, `my-ip` (SSH) |
| `my-db-sg` | MySQL/Aurora (3306) | `my-private-sg` |

1. In the VPC Console, go to **Security Groups** > **Create security group**.
   ![vpc_SG](/images/5-Workshop/5.2-vpc-network/vpc_SG.png)
2. Create the Security Groups listed above in `my-vpc-01`. For the inbound rules, use the corresponding Security Group as the source (instead of a CIDR block), as shown in the table above.
   ![vpc_SG](/images/5-Workshop/5.2-vpc-network/vpc_sg_create_01.png)
   ![vpc_SG](/images/5-Workshop/5.2-vpc-network/vpc_sg_create_02.png)
   ![vpc_SG](/images/5-Workshop/5.2-vpc-network/vpc_sg_create_03.png)

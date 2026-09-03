---
title: "Configuring Target Groups & Health Checks"
date: 2026-07-21
weight: 1
chapter: false
pre: " <b> 5.5.1. </b> "
---

# 5.5.1. Configuring Target Groups & Health Checks

Create **2 Target Groups**, one per tier:

1. In the EC2 Console, go to **Target Groups** > **Create target group**.
   ![tg](/images/5-Workshop/5.5-load-balancer/tg.png)

2. **Target group for the Frontend** (`public-tg`):
   * **Target type**: Instances
   * **Protocol/Port**: HTTP / 80
   * **IP address type**: IPv4
   * **VPC**: `my-vpc-01`
   * **Protocol version**: HTTP 1.1
   * **Health check path**: `/`
   * ![tg](/images/5-Workshop/5.5-load-balancer/tg_create_01.png)
   * Register the two Frontend EC2 instances (created in Section 5.4.3) as targets.
   * ![tg](/images/5-Workshop/5.5-load-balancer/tg_create_02.png)
   * Click **Create target group**.
   * ![tg](/images/5-Workshop/5.5-load-balancer/tg_create_03.png)

3. **Target group for the Backend** (`backend-tg`):
   * **Target type**: Instances
   * **Protocol/Port**: HTTP / 8080
   * **IP address type**: IPv4
   * **VPC**: `my-vpc-01`
   * **Protocol version**: HTTP 1.1
   * **Health check path**: `/api/documents`
   * ![tg](/images/5-Workshop/5.5-load-balancer/tg_create_04.png)
   * Register the two Backend EC2 instances (created in Section 5.4.4) as targets.
   * ![tg](/images/5-Workshop/5.5-load-balancer/tg_create_05.png)
   * Click **Create target group**.
   * ![tg](/images/5-Workshop/5.5-load-balancer/tg_create_06.png)
4. Confirm that both target groups show the **Healthy** status after a few minutes.

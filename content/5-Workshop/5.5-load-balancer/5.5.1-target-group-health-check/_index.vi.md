---
title: "Cấu hình Target Group và Health Check"
date: 2026-07-21
weight: 1
chapter: false
pre: " <b> 5.5.1. </b> "
---

# 5.5.1. Cấu hình Target Group và Health Check

Tạo **2 Target Group**, mỗi target group cho một tầng:

1. Trong EC2 console, vào **Target Groups** > **Create target group**.
   ![tg](/images/5-Workshop/5.5-load-balancer/tg.png)
2. **Target group cho Frontend** (`public-tg`):
   * **Target type**: Instances
   * **Protocol/Port**: HTTP / 80
   * **IP address type**: IPv4
   * **VPC**: `my-vpc-01`
   * **Protocol version**: HTTP 1.1
   * **Health check path**: `/`
   * ![tg](/images/5-Workshop/5.5-load-balancer/tg_create_01.png)
   * Đăng ký 2 instance EC2 frontend (mục 5.4.3) làm target.
   * ![tg](/images/5-Workshop/5.5-load-balancer/tg_create_02.png)
   * chon **create target group**
   * ![tg](/images/5-Workshop/5.5-load-balancer/tg_create_03.png)
3. **Target group cho Backend** (`backend-tg`):
   * **Target type**: Instances
   * **Protocol/Port**: HTTP / 8080
   * **IP address type**: IPv4
   * **VPC**: `my-vpc-01`
   * **Protocol version**: HTTP 1.1
   * **Health check path**: `/api/documents` 
   * ![tg](/images/5-Workshop/5.5-load-balancer/tg_create_04.png)
   * Đăng ký 2 instance EC2 backend (mục 5.4.4) làm target.
   * ![tg](/images/5-Workshop/5.5-load-balancer/tg_create_05.png)
   * chon **create target group**
   * ![tg](/images/5-Workshop/5.5-load-balancer/tg_create_06.png)
4. Xác nhận cả hai target group báo trạng thái **healthy** sau vài phút.

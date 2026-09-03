---
title: "Tạo Application Load Balancer cho Frontend"
date: 2026-07-21
weight: 2
chapter: false
pre: " <b> 5.5.2. </b> "
---

# 5.5.2. Tạo Application Load Balancer cho Frontend

1. Trong EC2 console, vào **Load Balancers** > **Create load balancer** > **Application Load Balancer**.
    ![alb](/images/5-Workshop/5.5-load-balancer/alb.png)
   ![alb](/images/5-Workshop/5.5-load-balancer/alb_create_01.png)
2. **Name**: `public-alb`.
3. **Scheme**: Internet-facing.
4. **IP address type**: IPv4
5. **VPC**: `my-vpc-01`; **Mappings**: `public-subnet-01` và `public-subnet-02`.
6. **Security groups**: `my-public-sg`.
7. **Listener**: HTTP : 80 → forward đến `public-tg`.
8. Nhấn **Create load balancer**.
   ![alb](/images/5-Workshop/5.5-load-balancer/alb_create_02.png)
9.  Sau khi khởi tạo xong, ghi lại **DNS name** của ALB — đây là URL public mà người dùng cuối sẽ dùng để truy cập ứng dụng.

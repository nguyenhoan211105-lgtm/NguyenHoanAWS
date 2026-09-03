---
title: "Creating the Frontend Application Load Balancer"
date: 2026-07-21
weight: 2
chapter: false
pre: " <b> 5.5.2. </b> "
---

# 5.5.2. Creating the Frontend Application Load Balancer

1. In the EC2 console, go to **Load Balancers** > **Create load balancer** > **Application Load Balancer**.
   ![alb](/images/5-Workshop/5.5-load-balancer/alb.png)
   ![alb](/images/5-Workshop/5.5-load-balancer/alb_create_01.png)
2. **Name**: `public-alb`.
3. **Scheme**: Internet-facing.
4. **IP address type**: IPv4
5. **VPC**: `my-vpc-01`; **Mappings**: `public-subnet-01` and `public-subnet-02`.
6. **Security groups**: `my-public-sg`.
7. **Listener**: HTTP : 80 → forward to `public-tg`.
8. Click **Create load balancer**.
    ![alb](/images/5-Workshop/5.5-load-balancer/alb_create_02.png)
9. After initialization is complete, record the ALB's **DNS name**—this is the public URL that end users will use to access the application.

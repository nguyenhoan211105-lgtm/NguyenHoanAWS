---
title: "Creating the Backend Application Load Balancer"
date: 2026-07-21
weight: 3
chapter: false
pre: " <b> 5.5.3. </b> "
---

# 5.5.3. Creating the Backend Application Load Balancer

1. In the EC2 console, go to **Load Balancers** > **Create load balancer** > **Application Load Balancer**.
   ![alb](/images/5-Workshop/5.5-load-balancer/alb.png)
   ![alb](/images/5-Workshop/5.5-load-balancer/alb_create_01.png)
2. **Name**: `private-alb`.
3. **Scheme**: Internal (the backend API only needs to be reachable from the frontend, not directly from the internet).
4. **IP address type**: IPv4
5. **VPC**: `my-vpc-01`; **Mappings**: `private-subnet-01` and `private-subnet-02`.
6. **Security groups**: `my-private-sg`.
7. **Listener**: HTTP : 80 → forward to `private-tg` (port 8080).
8. Click **Create load balancer**.
   ![alb](/images/5-Workshop/5.5-load-balancer/alb_create_03.png)
9. Note the backend ALB's **DNS name** and update the frontend configuration in section 5.4.1 (`API_BASE_URL`) to point to it, then redeploy the frontend build.

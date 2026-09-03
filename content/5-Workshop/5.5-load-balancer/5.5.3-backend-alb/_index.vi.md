---
title: "Tạo Application Load Balancer cho Backend"
date: 2026-07-21
weight: 3
chapter: false
pre: " <b> 5.5.3. </b> "
---

# 5.5.3. Tạo Application Load Balancer cho Backend

1. Trong EC2 console, vào **Load Balancers** > **Create load balancer** > **Application Load Balancer**.
   ![alb](/images/5-Workshop/5.5-load-balancer/alb.png)
   ![alb](/images/5-Workshop/5.5-load-balancer/alb_create_01.png)
2. **Name**: `private-alb`.
3. **Scheme**: Internal (backend API chỉ cần được frontend gọi tới, không cần public trực tiếp ra internet).
4. **IP address type**: IPv4
5. **VPC**: `my-vpc-01`; **Mappings**: `private-subnet-01` và `private-subnet-02`.
6. **Security groups**: `my-private-sg`.
7. **Listener**: HTTP : 80 → forward đến `private-tg` (port 8080).
8. Nhấn **Create load balancer**.
   ![alb](/images/5-Workshop/5.5-load-balancer/alb_create_03.png)
9.  Ghi lại **DNS name** của backend ALB và cập nhật vào cấu hình frontend ở mục 5.4.1 (`API_BASE_URL`), sau đó build và triển khai lại frontend.

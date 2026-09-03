---
title: "Cấu hình Security Group"
date: 2026-07-21
weight: 6
chapter: false
pre: " <b> 5.2.6. </b> "
---

# 5.2.6. Cấu hình Security Group

Tạo các Security Group sau (nguyên tắc tối thiểu quyền — mỗi tầng chỉ nhận traffic từ tầng phía trước nó):

| Security Group | Inbound Rule | Nguồn |
| :--- | :--- | :--- |
| `my-public-sg` | HTTP (80), HTTPS (443), SSH(22) | `0.0.0.0`(HTTP, HTTPs), `my-ip`(SSH) |
| `my-private-sg` | Custom TCP (8080), HTTP (80), SSH(22) | `my-public-sg`, `my-ip`(SSH)|
| `my-db-sg` | MySQL/Aurora (3306) | `my-private-sg` |

1. Trong VPC console, vào **Security Groups** > **Create security group**.
   ![vpc_SG](/images/5-Workshop/5.2-vpc-network/vpc_SG.png)
2. Tạo lần lượt các nhóm trên trong `my-vpc-01`, với inbound rule lấy Security Group tương ứng (không phải dải CIDR) làm nguồn như bảng trên.
   ![vpc_SG](/images/5-Workshop/5.2-vpc-network/vpc_sg_create_01.png)
   ![vpc_SG](/images/5-Workshop/5.2-vpc-network/vpc_sg_create_02.png)
   ![vpc_SG](/images/5-Workshop/5.2-vpc-network/vpc_sg_create_03.png)

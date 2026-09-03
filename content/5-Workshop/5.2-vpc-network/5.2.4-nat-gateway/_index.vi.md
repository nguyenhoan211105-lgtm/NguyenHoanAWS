---
title: "Tạo NAT Gateway"
date: 2026-07-21
weight: 4
chapter: false
pre: " <b> 5.2.4. </b> "
---

# 5.2.4. Tạo NAT Gateway

NAT Gateway cho phép các instance trong private subnet truy cập internet (ví dụ để tải bản cập nhật hệ điều hành) mà không bị truy cập trực tiếp từ bên ngoài.

1. Trong VPC console, vào **NAT Gateways** > **Create NAT gateway**.
   ![vpc_natGW](/images/5-Workshop/5.2-vpc-network/vpc_NAT.png)
2. **Name**: `my-natGW-01`.
3. **Subnet**: chọn `public-subnet-01`.
4. **Connectivity type**: Public.
5. Nhấn **Allocate Elastic IP** để cấp một Elastic IP mới.
6. Nhấn **Create NAT gateway**.
   ![vpc_natGW](/images/5-Workshop/5.2-vpc-network/vpc_NAT_create.png)
7. làm tương tự thêm 1 cái nữa với tên `my-natGW-02` đặt tại `public-subnet-02`

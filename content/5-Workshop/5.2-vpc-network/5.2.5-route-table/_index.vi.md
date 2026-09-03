---
title: "Cấu hình Route Table"
date: 2026-07-21
weight: 5
chapter: false
pre: " <b> 5.2.5. </b> "
---

# 5.2.5. Cấu hình Route Table

Tạo **3 Route Table**: một Route Table dành cho các Public Subnet (định tuyến đến Internet Gateway) và hai Route Table dành cho các Private Subnet (định tuyến đến NAT Gateway).

1. Trong VPC Console, vào **Route Tables** > **Create route table**.
   ![vpc_RTB](/images/5-Workshop/5.2-vpc-network/vpc_RTB.png)

2. **Public Route Table**:
   * Đặt tên `my-public-rtb`, chọn VPC `my-vpc-01`.
   * ![vpc_RTB](/images/5-Workshop/5.2-vpc-network/vpc_RTB_create.png)
   * Thêm Route `0.0.0.0/0` → Target: `my-igw-01`.
   * ![vpc_RTB](/images/5-Workshop/5.2-vpc-network/RTB_route_01.png)
   * ![vpc_RTB](/images/5-Workshop/5.2-vpc-network/RTB_route_02.png)
   * Trong phần **Subnet associations**, liên kết với `public-subnet-01` và `public-subnet-02`.
   * ![vpc_RTB](/images/5-Workshop/5.2-vpc-network/RTB_associations_01.png)
   * ![vpc_RTB](/images/5-Workshop/5.2-vpc-network/RTB_associations_02.png)

3. **Private Route Table 1**:
   * Đặt tên `my-private-rtb-01`.
   * Thêm Route `0.0.0.0/0` → Target: `my-natGW-01`.
   * ![vpc_RTB](/images/5-Workshop/5.2-vpc-network/vpc_RTB_create_02.png)
   * Trong phần **Subnet associations**, liên kết với `private-subnet-01`.
   * ![vpc_RTB](/images/5-Workshop/5.2-vpc-network/RTB_associations_03.png)

4. **Private Route Table 2**:
   * Đặt tên `my-private-rtb-02`.
   * ![vpc_RTB](/images/5-Workshop/5.2-vpc-network/RTB_route_3.png)
   * Thêm Route `0.0.0.0/0` → Target: `my-natGW-02`.
   * Trong phần **Subnet associations**, liên kết với `private-subnet-02`.
   * ![vpc_RTB](/images/5-Workshop/5.2-vpc-network/RTB_associations_3.png)

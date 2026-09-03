---
title: "Tạo các Subnet trên hai Availability Zone"
date: 2026-07-21
weight: 2
chapter: false
pre: " <b> 5.2.2. </b> "
---

# 5.2.2. Tạo các Subnet trên hai Availability Zone

Tạo **4 subnet** — 2 public và 2 private — trải trên hai AZ để đảm bảo tính sẵn sàng cao:

| Tên Subnet | AZ | Dải CIDR | Loại |
| :--- | :--- | :--- | :--- |
| `public-subnet-01` | us-east-1a | `10.0.0.0/20` | Public |
| `public-subnet-02` | us-east-1b | `10.0.16.0/20` | Public |
| `private-subnet-01` | us-east-1a | `10.0.32.0/20` | Private |
| `private-subnet-02` | us-east-1b | `10.0.48.0/20` | Private |

1. Trong VPC console, vào **Subnets** > **Create subnet**.
   ![vpc_subnet](/images/5-Workshop/5.2-vpc-network/vpc_subnet.png)
   ![vpc_subnet](/images/5-Workshop/5.2-vpc-network/vpc_subnet_create_2.png)
2. cau hinh:
   * Chọn VPC `my-vpc-01`.
   * Tên Subnet `public-subnet-01`
   * AZ  us-east-1a
   * IPv4 subnet CIDR block `10.0.0.0/20`
   * chọn add subnet để thêm subnet mới
3. Thêm 4 subnet ở trên với AZ và dải CIDR tương ứng.
4. Nhấn **Create subnet**.
5. Với 2 public subnet, vào **Actions** > **Edit subnet settings** và bật **Auto-assign public IPv4 address**.
   ![vpc_subnet](/images/5-Workshop/5.2-vpc-network/vpc_subnet_setting_01.png)

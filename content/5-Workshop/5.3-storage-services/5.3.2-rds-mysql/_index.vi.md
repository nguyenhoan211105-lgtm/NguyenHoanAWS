---
title: "Tạo cơ sở dữ liệu Amazon RDS MySQL"
date: 2026-07-21
weight: 2
chapter: false
pre: " <b> 5.3.2. </b> "
---

# 5.3.2. Tạo cơ sở dữ liệu Amazon RDS MySQL

1. Trong thanh tìm kiếm của AWS Console, nhập **RDS** và mở dịch vụ **RDS**.
   ![RDS](/images/5-Workshop/5.3-S3-RDS/rds.png)
2. Vào **Databases** > **Create database**.
   ![RDS](/images/5-Workshop/5.3-S3-RDS/rds_02.png)
3. **Engine type**: MySQL.
4. **Creation method**: Standard create.
5. **Templates**: Dev/Test.
6. **Availability and durability**: Single-AZ DB instance deployment (1 instance).
7. **Engine version**: `8.4.11`.
8. **DB instance identifier**: `my-database-01`.
9. **Master username/password**: Tự thiết lập thông tin đăng nhập (lưu trữ thông tin này một cách an toàn, ví dụ trong AWS Secrets Manager).
10. **DB instance class**:
   * **Instance type**: `db.t3.micro` (hoặc loại phù hợp với nhu cầu).
   * **Storage type**: `gp3`.
   * **Allocated storage**: `20 GiB`.
11. **Connectivity**:
   * **VPC**: `my-vpc-01`.
   * **DB subnet group**: `default`.
   * **Public access**: Yes.
   * **VPC security group**: `my-DB-sg`.
12. Nhấn **Create database** và chờ trạng thái chuyển thành **Available**.
   ![RDS](/images/5-Workshop/5.3-S3-RDS/rds_create.png)

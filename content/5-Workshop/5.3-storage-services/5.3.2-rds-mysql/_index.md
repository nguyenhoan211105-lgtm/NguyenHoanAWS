---
title: "Creating the Amazon RDS MySQL Database"
date: 2026-07-21
weight: 2
chapter: false
pre: " <b> 5.3.2. </b> "
---

# 5.3.2. Creating the Amazon RDS MySQL Database

1. In the AWS Console search bar, type **RDS** and open the **RDS** service.
   ![RDS](/images/5-Workshop/5.3-S3-RDS/rds.png)
2. Go to **Databases** > **Create database**.
   ![RDS](/images/5-Workshop/5.3-S3-RDS/rds_02.png)
3. **Engine type**: MySQL.
4. **method**: full configtion
5. **Templates**:Dev/Test.
6. **availability and duabilitdur** : Single-AZ DB instance deployment (1 instance)
7. **engine version:** `8.4.11`
8. **DB instance identifier**: `my-database-01`.
9.  **Master username/password**: set your own credentials (store them securely, e.g. in AWS Secrets Manager).
10. **DB instance class**: 
   * **instance type**:`db.t3.micro` (or as appropriate).
   * **storage type**: `gp3`
   * **allocated storage**: `20 GiB`
11. **Connectivity**:
   * **VPC**: `my-vpc-01`
   * **DB subnet group**: `default`
   * **Public access**: yes
   * **VPC security group**: `my-DB-sg`
12. Click **Create database** and wait for the status to become **Available**.
    ![RDS](/images/5-Workshop/5.3-S3-RDS/rds_create.png)

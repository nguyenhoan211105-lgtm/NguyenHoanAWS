---
title: "Configuring the S3 VPC Endpoint"
date: 2026-07-21
weight: 7
chapter: false
pre: " <b> 5.2.7. </b> "
---

# 5.2.7. Configuring the S3 VPC Endpoint

A **Gateway VPC Endpoint** lets the private-subnet backend instances reach Amazon S3 directly through the AWS network, without routing through the NAT Gateway — reducing cost and improving security.

1. In the VPC console, go to **Endpoints** > **Create endpoint**.
   ![vpc_s3](/images/5-Workshop/5.2-vpc-network/vpc_S3_endpoint.png)
2. **Service category**: AWS services.
   ![vpc_s3](/images/5-Workshop/5.2-vpc-network/vpc_S3_endpoint_create_01.png)
3. **Service Name**: search for and select `com.amazonaws.us-east-1.s3.s3` 
4. Type: **Gateway**.
   ![vpc_s3](/images/5-Workshop/5.2-vpc-network/vpc_S3_endpoint_create_02.png)
5. **VPC**: `my-vpc-01`.
6. **Route tables**: select `my-private-rtb-01`, `my-private-rtb-02` so private-subnet traffic to S3 uses the endpoint.
   ![vpc_s3](/images/5-Workshop/5.2-vpc-network/vpc_S3_endpoint_create_03.png)
7. Click **Create endpoint**.
    ![vpc_s3](/images/5-Workshop/5.2-vpc-network/vpc_S3_endpoint_create_04.png)
---
title: "Cấu hình S3 Endpoint"
date: 2026-07-21
weight: 7
chapter: false
pre: " <b> 5.2.7. </b> "
---

# 5.2.7. Cấu hình S3 Endpoint

**Gateway VPC Endpoint** cho phép các instance trong private subnet truy cập trực tiếp Amazon S3 qua mạng nội bộ của AWS mà không cần đi qua NAT Gateway — giúp giảm chi phí và tăng tính bảo mật.

1. Trong VPC console, vào **Endpoints** > **Create endpoint**.
   ![vpc_s3](/images/5-Workshop/5.2-vpc-network/vpc_S3_endpoint.png)
2. **Service category**: AWS services.
   ![vpc_s3](/images/5-Workshop/5.2-vpc-network/vpc_S3_endpoint_create_01.png)
3. **Service Name**: tìm và chọn `com.amazonaws.us-east-1.s3` 
4. Type: **Gateway**.
   ![vpc_s3](/images/5-Workshop/5.2-vpc-network/vpc_S3_endpoint_create_02.png)
5. **VPC**: `my-vpc-01`.
6. **Route tables**: chọn `my-private-rtb-01`, `my-private-rtb-02` để traffic từ private subnet đến S3 đi qua endpoint.
   ![vpc_s3](/images/5-Workshop/5.2-vpc-network/vpc_S3_endpoint_create_03.png)
7. Nhấn **Create endpoint**.
    ![vpc_s3](/images/5-Workshop/5.2-vpc-network/vpc_S3_endpoint_create_04.png)
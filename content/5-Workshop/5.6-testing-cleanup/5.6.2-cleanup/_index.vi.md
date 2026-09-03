---
title: "Dọn dẹp tài nguyên AWS"
date: 2026-07-21
weight: 2
chapter: false
pre: " <b> 5.6.2. </b> "
---

# 5.6.4. Dọn dẹp tài nguyên AWS

Để tránh phát sinh chi phí ngoài ý muốn, hãy xóa tài nguyên theo thứ tự sau (ngược với thứ tự tạo, để xóa các tài nguyên phụ thuộc trước):

1. **Load Balancer**: xóa `public-alb` và `private-alb`.
   ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_01.png)
2. **Target Group**: xóa `public-tg` và `private-tg`.
   ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_02.png)
3. **EC2 Instance**: terminate toàn bộ instance frontend và backend.
   ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_03.png)
4. **IAM Role**: xóa `ec2-backend-to-s3` (gỡ policy trước nếu cần).
   ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_04.png)
5. **RDS**: xóa instance `my-database-01` (chỉ bỏ qua final snapshot nếu không cần giữ lại dữ liệu).
   ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_05.png)
6. **S3 Bucket**: làm rỗng bucket `s3-document-manage-bucket`, sau đó xóa bucket.
   ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_06.png)
   ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_07.png)
7. **VPC Endpoint**: xóa S3 Gateway Endpoint.
   ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_08.png)
8. **NAT Gateway**: xóa `my-natGW-01`, `my-natGW-02`, sau đó release Elastic IP liên kết với nó.
   ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_09.png)
9.  **Route Table**: xóa `my-public-rtb` và `my-private-rtb-01`, `my-private-rtb-02` (sau khi gỡ các subnet association).
    ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_10.png)
10. **Internet Gateway**: detach `my-igw-01` khỏi VPC, sau đó xóa.
    ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_11.png)
    ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_12.png)
11. **Subnet**: xóa toàn bộ 4 subnet.
    ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_13.png)
12. **Security Group**: xóa  `public-sg`, `private-sg`, `my-DB-sg`.
    ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_14.png)
13. **VPC**: cuối cùng, xóa `my-vpc-01`.
    ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_15.png)

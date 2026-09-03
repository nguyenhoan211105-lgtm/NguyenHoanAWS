---
title: "Cleaning Up AWS Resources"
date: 2026-07-21
weight: 2
chapter: false
pre: " <b> 5.6.2. </b> "
---

# 5.6.4. Cleaning Up AWS Resources

To avoid unexpected charges, delete the resources in the following order (reverse of creation order, so dependent resources are removed first):

1. **Load Balancers**: Delete `public-alb` and `private-alb`.
   ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_01.png)
2. **Target Groups**: Delete `public-tg` and `private-tg`.
   ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_02.png)
3. **EC2 Instances**: Terminate all Frontend and Backend instances.
   ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_03.png)
4. **IAM Role**: Delete `ec2-backend-to-s3` (detach the policy first if necessary).
   ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_04.png)
5. **RDS**: Delete the `my-database-01` instance (skip the final snapshot only if you do not need to retain the data).
   ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_05.png)
6. **S3 Bucket**: Empty the `s3-document-manage-bucket` bucket, then delete the bucket.
   ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_06.png)
   ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_07.png)
7. **VPC Endpoint**: Delete the S3 Gateway Endpoint.
   ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_08.png)
8. **NAT Gateways**: Delete `my-natGW-01` and `my-natGW-02`, then release the Elastic IP addresses associated with them.
   ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_09.png)
9. **Route Tables**: Delete `my-public-rtb`, `my-private-rtb-01`, and `my-private-rtb-02` (after removing the subnet associations).
   ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_10.png)
10. **Internet Gateway**: Detach `my-igw-01` from the VPC, then delete it.
    ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_11.png)
    ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_12.png)
11. **Subnets**: Delete all four subnets.
    ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_13.png)
12. **Security Groups**: Delete `public-sg`, `private-sg`, and `my-DB-sg`.
    ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_14.png)
13. **VPC**: Finally, delete `my-vpc-01`.
    ![clean](/images/5-Workshop/5.6-testing-cleanup/cl_15.png)

---
title: "Creating the Amazon S3 Bucket"
date: 2026-07-21
weight: 1
chapter: false
pre: " <b> 5.3.1. </b> "
---

# 5.3.1. Creating the Amazon S3 Bucket

1. In the AWS Console search bar, enter **S3** and open the **S3** service.
   ![s3](/images/5-Workshop/5.3-S3-RDS/s3.png)
2. Click **Create bucket**.
   ![s3](/images/5-Workshop/5.3-S3-RDS/s3_2.png)
3. **Bucket name**: `s3-document-manage-bucket` (must be globally unique).
4. **Region**: Select the same Region used for the VPC.
5. Keep **Block all public access** enabled — the application will access the bucket through the backend IAM role, rather than directly from the browser.
6. Enable **Bucket Versioning** *(optional)* (recommended to help protect against accidental overwrites or deletions).
7. Click **Create bucket**.
   ![s3](/images/5-Workshop/5.3-S3-RDS/s3_create.png)
8. In the **Permissions** section, scroll down to **Cross-origin resource sharing (CORS)** > click **Edit** > enter the policy below to allow the frontend to access the bucket > click **Save changes**.
   ```
   [
    {
        "AllowedHeaders": [
            "*"
        ],
        "AllowedMethods": [
            "PUT",
            "GET"
        ],
        "AllowedOrigins": [
            "http://127.0.0.1:5500",
            "http://localhost:5500",
            "http://public-alb-780378168.us-east-1.elb.amazonaws.com"
        ],
        "ExposeHeaders": [
            "ETag"
        ],
        "MaxAgeSeconds": 3000
    }
   ]
   ```
   ![s3](/images/5-Workshop/5.3-S3-RDS/s3_cors.png)
   ![s3](/images/5-Workshop/5.3-S3-RDS/s3_cors_02.png)

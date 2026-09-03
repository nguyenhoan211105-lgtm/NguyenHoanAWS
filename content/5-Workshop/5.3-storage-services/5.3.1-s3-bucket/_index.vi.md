---
title: "Tạo Amazon S3 Bucket"
date: 2026-07-21
weight: 1
chapter: false
pre: " <b> 5.3.1. </b> "
---

# 5.3.1. Tạo Amazon S3 Bucket

1. Trong thanh tìm kiếm AWS Console, gõ **S3** và mở dịch vụ **S3**.
   ![s3](/images/5-Workshop/5.3-S3-RDS/s3.png)
2. Nhấn **Create bucket**.
   ![s3](/images/5-Workshop/5.3-S3-RDS/s3_2.png)
3. **Bucket name**: `s3-document-manage-bucket` (phải là duy nhất toàn cầu).
4. **Region**: cùng Region đã dùng cho VPC.
5. Giữ nguyên **Block all public access** — ứng dụng sẽ truy cập bucket thông qua IAM role của backend, không truy cập trực tiếp từ trình duyệt.
6. Bật **Bucket Versioning**(optional) (khuyến nghị, giúp bảo vệ khỏi việc ghi đè/xóa nhầm).
7. Nhấn **Create bucket**.
   ![s3](/images/5-Workshop/5.3-S3-RDS/s3_create.png)
8. Tại phần **permission**, kéo xuống phần **Cross-origin resource sharing (CORS)** > nhấn **edit** > lưu polices bên dưới để cho phép frontend truy cập > **save change**
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
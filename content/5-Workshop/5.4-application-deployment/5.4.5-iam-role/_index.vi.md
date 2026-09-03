---
title: "Cấu hình IAM Role"
date: 2026-07-21
weight: 5
chapter: false
pre: " <b> 5.4.5. </b> "
---

# 5.4.5. Cấu hình IAM Role

Backend cần quyền đọc/ghi object trong S3 bucket. Thay vì hard-code access key, ta gắn một **IAM Role** cho các EC2 instance backend.

1. Trong thanh tìm kiếm AWS Console, gõ **IAM** và mở dịch vụ **IAM**.
2. Vào **Roles** > **Create role**.
  ![role](/images/5-Workshop/5.4-application-deployment/iam_role.png)
3. **Trusted entity type**: AWS service.
4. **Use case**: EC2.
  ![role](/images/5-Workshop/5.4-application-deployment/role_create_01.png)
5. Gắn một custom policy giới hạn phạm vi đúng bucket lưu trữ file:
  ![role](/images/5-Workshop/5.4-application-deployment/role_create_02.png)
  
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Statement1",
            "Effect": "Allow",
            "Action": [
                "s3:*"
            ],
            "Resource": [
                "arn:aws:s3:::s3-document-manage-bucket",
                "arn:aws:s3:::s3-document-manage-bucket/*"
            ]
        }
    ]
}
```

6. **Role name**: `EC2-backend-to-s3`.
7. Nhấn **Create role**.
  ![role](/images/5-Workshop/5.4-application-deployment/role_create_03.png)
8. Gắn role này cho các EC2 instance backend  **Actions** > **Security** > **Modify IAM role**.
   ![role](/images/5-Workshop/5.4-application-deployment/role_attach.png)
   ![role](/images/5-Workshop/5.4-application-deployment/role_attach_02.png)

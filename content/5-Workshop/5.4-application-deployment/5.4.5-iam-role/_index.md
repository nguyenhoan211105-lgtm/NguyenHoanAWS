---
title: "Configuring the IAM Role"
date: 2026-07-21
weight: 5
chapter: false
pre: " <b> 5.4.5. </b> "
---

# 5.4.5. Configuring the IAM Role

The backend needs permission to read/write objects in the S3 bucket. Instead of hard-coding credentials, attach an **IAM Role** to the backend EC2 instances.

1. In the AWS Console search bar, enter **IAM** and open the **IAM** service.
2. Go to **Roles** > **Create role**.
   ![role](/images/5-Workshop/5.4-application-deployment/iam_role.png)
3. **Trusted entity type**: AWS service.
4. **Use case**: EC2.
   ![role](/images/5-Workshop/5.4-application-deployment/role_create_01.png)
5. Attach a custom policy that restricts permissions to the specific S3 bucket used for file storage:
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
7. Click **Create role**.
   ![role](/images/5-Workshop/5.4-application-deployment/role_create_03.png)
8. Attach this role to the backend EC2 instances by selecting **Actions** > **Security** > **Modify IAM role**.
   ![role](/images/5-Workshop/5.4-application-deployment/role_attach.png)
   ![role](/images/5-Workshop/5.4-application-deployment/role_attach_02.png)

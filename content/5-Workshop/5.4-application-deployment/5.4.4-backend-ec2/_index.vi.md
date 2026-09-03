---
title: "Triển khai Backend trên EC2"
date: 2026-07-21
weight: 4
chapter: false
pre: " <b> 5.4.4. </b> "
---

# 5.4.4. Triển khai Backend trên EC2

1. Trong EC2 console, nhấn **Launch instance**.
   ![APP_deploy](/images/5-Workshop/5.4-application-deployment/EC2.png)
2. **Name**: `private-BE-01`.
3. **AMI**: Amazon Linux 2023.
4. **Instance type**: `t3.micro`.
5. **key-pair**: chọn key-pair của bạn
6. **Network settings**: chọn **edit** > VPC `my-vpc-01`, subnet `private-subnet-01`, Security group `my-private-sg`.
7. Nhấn **Launch instance**.
   ![APP_deploy](/images/5-Workshop/5.4-application-deployment/EC2_BE_create.png)
8. Sau khi instance chạy, kết nối qua **EC2 Instance Connect**, vào **in web browser**, vào **ssm session manage**, chon **connect**.
    ![APP_deploy](/images/5-Workshop/5.4-application-deployment/ec2_be_connect.png)
    ![APP_deploy](/images/5-Workshop/5.4-application-deployment/ec2_be_connect_02.png)
    ![APP_deploy](/images/5-Workshop/5.4-application-deployment/ec2_be_connect_03.png)
9.  chạy lần lượt các lệnh bên dưới để cấu hình ec2

```bash
#[ec2-user@ip-{your-ec2-public-ip} ~]$
sudo dnf install -y java-17-amazon-corretto
aws s3 cp s3://s3-document-manage-bucket/Doc_manage_BE-0.0.1-SNAPSHOT.jar /home/ec2-user/app.jar #tải file jar của bạn lên có thể up lên s3 rồi tải
sudo nano /etc/systemd/system/doc-manage.service
#dán tập lệnh bên dưới để cấu hình be
[Unit]
Description=Doc Manage Spring Boot Backend
After=network-online.target
Wants=network-online.target

[Service]
User=ec2-user
WorkingDirectory=/home/ec2-user

Environment="APP_CORS_ALLOWED_ORIGINS=http://localhost:5500,http://127.0.0.1:5500,http://public-alb-780378168.us-east-1.elb.amazonaws.com"

ExecStart=/usr/bin/java -jar /home/ec2-user/app.jar --server.tomcat.keep-alive-timeout=65000 --server.tomcat.max-keep-alive-requests=10000

Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
#ctrl+O để lưu, ctrl+X để thoát
sudo systemctl daemon-reload
sudo systemctl enable doc-manage
sudo systemctl start doc-manage
```
10. Tạo BE-ami
    * ở giao diện instance chọn public-FE-01
    * chọn **action**
    * chọn **image and templates** > **create image**
    * ![APP_deploy](/images/5-Workshop/5.4-application-deployment/BE_img.png)
    * nhập tên của image > **create image**
    * ![APP_deploy](/images/5-Workshop/5.4-application-deployment/BE_img_create.png)
11. Tạo thêm một ec2 frontend trên subnet còn lại
    * giữ nguyên các bước tao bình thường nhưng thay vì chọn ami của **amazon** thì ta chọn **BE-img** mà ta vừa tạo và subnet là `private-subnet-02`
    * ![APP_deploy](/images/5-Workshop/5.4-application-deployment/EC2_BE_img_create.png)

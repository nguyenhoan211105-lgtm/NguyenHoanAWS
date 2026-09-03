---
title: "Triển khai Frontend trên EC2"
date: 2026-07-21
weight: 3
chapter: false
pre: " <b> 5.4.3. </b> "
---

# 5.4.3. Triển khai Frontend trên EC2

1. Trong EC2 console, nhấn **Launch instance**.
   ![APP_deploy](/images/5-Workshop/5.4-application-deployment/EC2.png)
2. **Name**: `public-FE-01`.
3. **AMI**: Amazon Linux 2023.
4. **Instance type**: `t3.micro`.
5. **key-pair**: chọn key-pair của bạn
6. **Network settings**: chọn **edit** > VPC `my-vpc-01`, subnet `public-subnet-01`, Security group `my-public-sg`.
7. Nhấn **Launch instance**.
   ![APP_deploy](/images/5-Workshop/5.4-application-deployment/EC2_FE_create.png)
8. Sau khi instance chạy, kết nối qua **EC2 Instance Connect**, vào **SSH client**, copy lệnh của phần **4. Connect to your instance using its Public DNS**.
9.  bật cmd trên máy tính bạn ở folder chứa **key-pair** mà bạn tạo **ec2** và dán giòng lệnh đã copy vào để kết nối đến **ec2**.
    ![APP_deploy](/images/5-Workshop/5.4-application-deployment/ec2_connect-01.png)
    ![APP_deploy](/images/5-Workshop/5.4-application-deployment/ec2_connect_02.png)
    ![APP_deploy](/images/5-Workshop/5.4-application-deployment/ec2_connect_03.png)
10. chạy lần lượt các lệnh bên dưới để cấu hình ec2

```bash
#[ec2-user@ip-{your-ec2-public-ip} ~]$
sudo dnf install nginx -y
aws s3 cp s3://s3-document-manage-bucket/index.html /home/ec2-user/index.html #tải file chứa frontend của bạn lên có thể tải tại máy cx có thể up lên s3 rồi tải
sudo rm -rf /usr/share/nginx/html/*
sudo cp /home/ec2-user/index.html /usr/share/nginx/html/index.html
sudo nano /etc/nginx/conf.d/frontend.conf #tạo file config cho nginx điều hướng tới backend
#dán tập lệnh bên dưới
server {
    listen 80;
    server_name _;
    root /usr/share/nginx/html;
    index index.html;

    # ==========================
    # FRONTEND
    # ==========================
    location / {
        try_files $uri $uri/ =404;
    }

    # ==========================
    # BACKEND API
    # ==========================
    location /api/ {
        proxy_pass http://private-alb-1572325469.us-east-1.elb.amazonaws.com;

        proxy_http_version 1.1;

        proxy_set_header Host private-alb-1572325469.us-east-1.elb.amazonaws.com;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
#ctrl+O để lưu, ctrl+X để thoát
sudo systemctl enable nginx
sudo systemctl start nginx
```
11. Tạo FE-ami
    * ở giao diện instance chọn public-FE-01
    * chọn **action**
    * chọn **image and templates** > **create image**
    * ![APP_deploy](/images/5-Workshop/5.4-application-deployment/FE_img.png)
    * nhập tên của image > **create image**
    * ![APP_deploy](/images/5-Workshop/5.4-application-deployment/FE_img_create.png)
12. Tạo thêm một ec2 frontend trên subnet còn lại
    * giữ nguyên các bước tao bình thường nhưng thay vì chọn ami của **amazon** thì ta chọn **FE-img** mà ta vừa tạo và subnet là `public-subnet-02`
    * ![APP_deploy](/images/5-Workshop/5.4-application-deployment/EC2_FE_img_create.png)
    
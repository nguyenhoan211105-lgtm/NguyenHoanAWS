---
title: "Deploying the Frontend on EC2"
date: 2026-07-21
weight: 3
chapter: false
pre: " <b> 5.4.3. </b> "
---

# 5.4.3. Deploying the Frontend on EC2

1. In the EC2 Console, click **Launch instance**.

   ![APP_deploy](/images/5-Workshop/5.4-application-deployment/EC2.png)

2. **Name**: `public-FE-01`.

3. **AMI**: Amazon Linux 2023.

4. **Instance type**: `t3.micro`.

5. **Key pair**: Select your key pair.

6. **Network settings**: Select **Edit** > choose VPC `my-vpc-01`, subnet `public-subnet-01`, and Security Group `my-public-sg`.

7. Click **Launch instance**.

   ![APP_deploy](/images/5-Workshop/5.4-application-deployment/EC2_FE_create.png)

8. After the instance is running, connect using **EC2 Instance Connect**. Go to **SSH client** and copy the command under **4. Connect to your instance using its Public DNS**.

9. Open Command Prompt on your computer in the folder containing the **EC2 key pair** that you created, then paste and run the copied command to connect to the **EC2 instance**.

   ![APP_deploy](/images/5-Workshop/5.4-application-deployment/ec2_connect-01.png)

   ![APP_deploy](/images/5-Workshop/5.4-application-deployment/ec2_connect_02.png)

   ![APP_deploy](/images/5-Workshop/5.4-application-deployment/ec2_connect_03.png)

10. Run the following commands to configure the EC2 instance:

```bash
# [ec2-user@ip-{your-ec2-public-ip} ~]$
sudo dnf install nginx -y
# Download your frontend file. You can upload it directly to the EC2 instance
# or upload it to Amazon S3 and download it from there.
aws s3 cp s3://s3-document-manage-bucket/index.html /home/ec2-user/index.html
sudo rm -rf /usr/share/nginx/html/*
sudo cp /home/ec2-user/index.html /usr/share/nginx/html/index.html
# Create an Nginx configuration file to route API requests to the backend
sudo nano /etc/nginx/conf.d/frontend.conf
# Paste the following configuration
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
# Press Ctrl+O to save, then Ctrl+X to exit
sudo systemctl enable nginx
sudo systemctl start nginx
```
11. Create the `FE-img` AMI:
   * In the **Instances** interface, select `public-FE-01`.
   * Select **Actions**.
   * Select **Image and templates** > **Create image**.
   * ![APP_deploy](/images/5-Workshop/5.4-application-deployment/FE_img.png)
   * Enter a name for the image, then click **Create image**.
   * ![APP_deploy](/images/5-Workshop/5.4-application-deployment/FE_img_create.png)
12. Create another Frontend EC2 instance in the remaining subnet:
   * Follow the same steps as before. However, instead of selecting an **Amazon-provided AMI**, select the `FE-img` AMI that you just created. Set the subnet to `public-subnet-02`.
   * ![APP_deploy](/images/5-Workshop/5.4-application-deployment/EC2_FE_img_create.png)
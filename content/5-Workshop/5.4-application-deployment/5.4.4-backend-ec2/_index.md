---
title: "Deploying the Backend on EC2"
date: 2026-07-21
weight: 4
chapter: false
pre: " <b> 5.4.4. </b> "
---

# 5.4.4. Deploying the Backend on EC2

1. In the EC2 Console, click **Launch instance**.

   ![APP_deploy](/images/5-Workshop/5.4-application-deployment/EC2.png)

2. **Name**: `private-BE-01`.

3. **AMI**: Amazon Linux 2023.

4. **Instance type**: `t3.micro`.

5. **Key pair**: Select your key pair.

6. **Network settings**: Select **Edit** > choose VPC `my-vpc-01`, subnet `private-subnet-01`, and Security Group `my-private-sg`.

7. Click **Launch instance**.

   ![APP_deploy](/images/5-Workshop/5.4-application-deployment/EC2_BE_create.png)

8. After the instance is running, connect to it through **EC2 Instance Connect**. Select **Connect**, then go to **Session Manager** and select **Connect**.

   ![APP_deploy](/images/5-Workshop/5.4-application-deployment/ec2_be_connect.png)

   ![APP_deploy](/images/5-Workshop/5.4-application-deployment/ec2_be_connect_02.png)

   ![APP_deploy](/images/5-Workshop/5.4-application-deployment/ec2_be_connect_03.png)

9. Run the following commands to configure the EC2 instance:

```bash
# [ec2-user@ip-{your-ec2-private-ip} ~]$
sudo dnf install -y java-17-amazon-corretto
# Download your JAR file. You can upload it to Amazon S3 and download it from there.
aws s3 cp s3://s3-document-manage-bucket/Doc_manage_BE-0.0.1-SNAPSHOT.jar /home/ec2-user/app.jar
sudo nano /etc/systemd/system/doc-manage.service
# Paste the following configuration to configure the backend service
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
# Press Ctrl+O to save, then Ctrl+X to exit
sudo systemctl daemon-reload
sudo systemctl enable doc-manage
sudo systemctl start doc-manage
```

10. Create the `BE-img` AMI:
   * In the **Instances** interface, select `private-BE-01`.
   * Select **Actions**.
   * Select **Image and templates** > **Create image**.
   * ![APP_deploy](/images/5-Workshop/5.4-application-deployment/BE_img.png)
   * Enter a name for the image, then click **Create image**.
   * ![APP_deploy](/images/5-Workshop/5.4-application-deployment/BE_img_create.png)

11. Create another Backend EC2 instance in the remaining subnet:
   * Follow the same steps as before. However, instead of selecting an **Amazon-provided AMI**, select the `BE-img` AMI that you just created and set the subnet to `private-subnet-02`.
   * ![APP_deploy](/images/5-Workshop/5.4-application-deployment/EC2_BE_img_create.png)
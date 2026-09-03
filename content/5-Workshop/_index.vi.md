---
title: "Workshop"
date: 2026-07-21
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Hướng dẫn chi tiết: Triển khai Hệ thống Lưu trữ & Chia sẻ File trên AWS

#### Tổng quan bài Thực hành (Workshop)

Bài thực hành này hướng dẫn xây dựng và triển khai một **Ứng dụng Web Lưu trữ & Chia sẻ File 2-tier** trên AWS, sử dụng hạ tầng mạng VPC sẵn sàng cao, EC2 cho tầng tính toán, RDS MySQL lưu trữ metadata, Amazon S3 lưu trữ file và Application Load Balancer để phân phối lưu lượng. Nội dung được cấu trúc thành các chương chính từ **5.1** đến **5.6** và các bài thực hành chi tiết **5.x.y** dưới đây:

---

#### Danh sách các chương thực hành:

1. [5.1. Chuẩn bị môi trường](5.1-prerequisite/)
2. [5.2. Thiết kế và triển khai VPC](5.2-vpc-network/)
   * [5.2.1. Khởi tạo VPC](5.2-vpc-network/5.2.1-create-vpc/)
   * [5.2.2. Tạo các Subnet trên hai Availability Zone](5.2-vpc-network/5.2.2-subnet/)
   * [5.2.3. Tạo và cấu hình Internet Gateway](5.2-vpc-network/5.2.3-internet-gateway/)
   * [5.2.4. Tạo NAT Gateway](5.2-vpc-network/5.2.4-nat-gateway/)
   * [5.2.5. Cấu hình Route Table](5.2-vpc-network/5.2.5-route-table/)
   * [5.2.6. Cấu hình Security Group](5.2-vpc-network/5.2.6-security-group/)
   * [5.2.7. Cấu hình S3 Endpoint](5.2-vpc-network/5.2.7-S3-endpoint/)
3. [5.3. Triển khai các dịch vụ lưu trữ](5.3-storage-services/)
   * [5.3.1. Tạo Amazon S3 Bucket](5.3-storage-services/5.3.1-s3-bucket/)
   * [5.3.2. Tạo cơ sở dữ liệu Amazon RDS MySQL](5.3-storage-services/5.3.2-rds-mysql/)
   * [5.3.3. Thiết kế cơ sở dữ liệu Metadata](5.3-storage-services/5.3.3-database-metadata/)
4. [5.4. Xây dựng và triển khai ứng dụng](5.4-application-deployment/)
   * [5.4.1. Xây dựng Frontend](5.4-application-deployment/5.4.1-frontend/)
   * [5.4.2. Xây dựng Backend Spring Boot](5.4-application-deployment/5.4.2-backend-spring-boot/)
   * [5.4.3. Triển khai Frontend trên EC2](5.4-application-deployment/5.4.3-frontend-ec2/)
   * [5.4.4. Triển khai Backend trên EC2](5.4-application-deployment/5.4.4-backend-ec2/)
   * [5.4.5. Cấu hình IAM Role](5.4-application-deployment/5.4.5-iam-role/)
5. [5.5. Cấu hình Load Balancer](5.5-load-balancer/)
   * [5.5.1. Cấu hình Target Group và Health Check](5.5-load-balancer/5.5.1-target-group-health-check/)
   * [5.5.2. Tạo Application Load Balancer cho Frontend](5.5-load-balancer/5.5.2-frontend-alb/)
   * [5.5.3. Tạo Application Load Balancer cho Backend](5.5-load-balancer/5.5.3-backend-alb/)
6. [5.6. Kiểm thử và dọn dẹp tài nguyên](5.6-testing-cleanup/)
   * [5.6.1. Kiểm thử chức năng](5.6-testing-cleanup/5.6.1-testing/)
   * [5.6.2. Dọn dẹp tài nguyên AWS](5.6-testing-cleanup/5.6.2-cleanup/)

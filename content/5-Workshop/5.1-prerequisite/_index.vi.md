---
title: "Chuẩn bị môi trường"
date: 2026-07-21
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

# 5.1. Chuẩn bị môi trường

### Yêu cầu tiên quyết
1. **Tài khoản AWS** có quyền Administrator Access, hoặc IAM User/Role có đủ quyền thao tác trên VPC, EC2, RDS, S3, IAM và ELB.
2. **Công cụ cài đặt trên máy local**:
   * AWS CLI v2 (đã cấu hình bằng `aws configure`)
   * Java 17+ và Maven (để build Backend Spring Boot)
   * Node.js 18+ (để build Frontend, nếu dùng framework JS)
   * MySQL client (MySQL Workbench, DBeaver hoặc `mysql` CLI) để kiểm tra kết nối RDS
3. **Trình duyệt web**: Google Chrome, Firefox, Safari hoặc Microsoft Edge.

---

### Bước 1: Đăng nhập Console và Chọn Region
1. Truy cập [AWS Management Console](https://console.aws.amazon.com/) và đăng nhập tài khoản của bạn.
2. Trên góc trên bên phải thanh điều hướng, chọn Region sẽ triển khai **United States(N. Virginia) - us-east-1**. Sử dụng thống nhất một Region cho toàn bộ tài nguyên trong bài thực hành này.

### Bước 2: Phác thảo kiến trúc
Trước khi khởi tạo tài nguyên, cần phác thảo kiến trúc mục tiêu:

| Thành phần | Vai trò |
| :--- | :--- |
| VPC (2 AZ) | Ranh giới cô lập mạng cho toàn hệ thống |
| Public Subnet | Đặt các ALB và NAT Gateway |
| Private Subnet | Đặt các EC2 instance (frontend/backend) và cơ sở dữ liệu RDS |
| Amazon S3 | Lưu trữ file thực tế được tải lên |
| Amazon RDS (MySQL) | Lưu trữ metadata của file (tên file, chủ sở hữu, dung lượng, ngày tải lên...) |
| Application Load Balancer | Phân phối lưu lượng đến các EC2 frontend và backend |

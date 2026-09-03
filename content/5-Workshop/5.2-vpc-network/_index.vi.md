---
title: "Thiết kế và triển khai VPC"
date: 2026-07-21
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

# 5.2. Thiết kế và triển khai VPC

Chương này khởi tạo một VPC sẵn sàng cao trải trên **hai Availability Zone**, gồm các Public Subnet (đặt ALB, NAT Gateway) và Private Subnet (đặt EC2, RDS) — theo đúng khuyến nghị của AWS cho ứng dụng 2-tier chạy production.

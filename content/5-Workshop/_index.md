---
title: "Workshop"
date: 2026-07-21
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Step-by-Step Guide: Deploying a File Storage & Sharing System on AWS

#### Workshop Overview

This workshop walks through building and deploying a **2-tier File Storage & Sharing Web Application** on AWS, using a highly-available VPC network, EC2 for compute, RDS MySQL for metadata, Amazon S3 for file storage, and Application Load Balancers for traffic distribution. The modules are structured under main chapters **5.1** through **5.6** and sub-modules **5.x.y** below:

---

#### Agenda:

1. [5.1. Environment Preparation](5.1-prerequisite/)
2. [5.2. VPC Network Design & Deployment](5.2-vpc-network/)
   * [5.2.1. Creating the VPC](5.2-vpc-network/5.2.1-create-vpc/)
   * [5.2.2. Creating Subnets Across Two Availability Zones](5.2-vpc-network/5.2.2-subnet/)
   * [5.2.3. Creating and Configuring the Internet Gateway](5.2-vpc-network/5.2.3-internet-gateway/)
   * [5.2.4. Creating the NAT Gateway](5.2-vpc-network/5.2.4-nat-gateway/)
   * [5.2.5. Configuring Route Tables](5.2-vpc-network/5.2.5-route-table/)
   * [5.2.6. Configuring Security Groups](5.2-vpc-network/5.2.6-security-group/)
   * [5.2.7. Configuring the S3 VPC Endpoint](5.2-vpc-network/5.2.7-S3-endpoint/)
3. [5.3. Deploying Storage Services](5.3-storage-services/)
   * [5.3.1. Creating the Amazon S3 Bucket](5.3-storage-services/5.3.1-s3-bucket/)
   * [5.3.2. Creating the Amazon RDS MySQL Database](5.3-storage-services/5.3.2-rds-mysql/)
   * [5.3.3. Designing the Metadata Database](5.3-storage-services/5.3.3-database-metadata/)
4. [5.4. Building and Deploying the Application](5.4-application-deployment/)
   * [5.4.1. Building the Frontend](5.4-application-deployment/5.4.1-frontend/)
   * [5.4.2. Building the Spring Boot Backend](5.4-application-deployment/5.4.2-backend-spring-boot/)
   * [5.4.3. Deploying the Frontend on EC2](5.4-application-deployment/5.4.3-frontend-ec2/)
   * [5.4.4. Deploying the Backend on EC2](5.4-application-deployment/5.4.4-backend-ec2/)
   * [5.4.5. Configuring the IAM Role](5.4-application-deployment/5.4.5-iam-role/)
5. [5.5. Configuring the Load Balancers](5.5-load-balancer/)
   * [5.5.1. Configuring Target Groups & Health Checks](5.5-load-balancer/5.5.1-target-group-health-check/)
   * [5.5.2. Creating the Frontend Application Load Balancer](5.5-load-balancer/5.5.2-frontend-alb/)
   * [5.5.3. Creating the Backend Application Load Balancer](5.5-load-balancer/5.5.3-backend-alb/)
6. [5.6. Testing and Resource Cleanup](5.6-testing-cleanup/)
   * [5.6.1. Testing the Feature](5.6-testing-cleanup/5.6.1-testing/)
   * [5.6.2. Cleaning Up AWS Resources](5.6-testing-cleanup/5.6.2-cleanup/)

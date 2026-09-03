---
title: "Environment Preparation"
date: 2026-07-21
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

# 5.1. Environment Preparation

### Prerequisites
1. **AWS Account** with Administrator Access, or an IAM User/Role with sufficient permissions on VPC, EC2, RDS, S3, IAM and ELB.
2. **Local tools**:
   * AWS CLI v2 (configured with `aws configure`)
   * Java 17+ and Maven (to build the Spring Boot backend)
   * Node.js 18+ (to build the frontend, if using a JS framework)
   * A MySQL client (MySQL Workbench, DBeaver, or `mysql` CLI) to verify RDS connectivity
3. **Web browser**: Google Chrome, Firefox, Safari or Microsoft Edge.

---

### Step 1: Sign In to the Console and Select a Region
1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/).
2. In the top-right corner of the navigation bar, select the Region you will deploy to **United States(N. Virginia) - us-east-1**. Use the same Region for every resource created throughout this workshop.

### Step 2: Plan the Architecture
Before provisioning resources, sketch out the target architecture:

| Component | Purpose |
| :--- | :--- |
| VPC (2 AZs) | Network isolation boundary for the whole system |
| Public Subnets | Host the ALBs and the NAT Gateway |
| Private Subnets | Host the EC2 instances (frontend/backend) and the RDS database |
| Amazon S3 | Stores the actual uploaded files |
| Amazon RDS (MySQL) | Stores file metadata (filename, owner, size, upload date...) |
| Application Load Balancer | Distributes traffic to the frontend and backend EC2 fleets |

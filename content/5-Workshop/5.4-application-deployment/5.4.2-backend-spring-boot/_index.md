---
title: "Building the Spring Boot Backend"
date: 2026-07-21
weight: 2
chapter: false
pre: " <b> 5.4.2. </b> "
---

# 5.4.2. Building the Spring Boot Backend

1. Create a Spring Boot project (via [Spring Initializr](https://start.spring.io/)) with dependencies: **spring-boot-starter**, **spring-boot-devtools**, **mysql-connector-j**, **lombok**, **spring-boot-starter-data-jpa**, **spring-boot-starter-test**, **spring-boot-starter-web**, **spring-boot-starter-validation**, **software.amazon.awssdk:s3**.
2. Configure the database and S3 bucket in `application.yaml`:

```application.yaml
server:
  port: 8080
spring:
  application:
    name: Doc_manage_BE

  datasource:
    url: jdbc:mysql://my-database-01.c27mskqeg2mr.us-east-1.rds.amazonaws.com:3306/docMetadata?useSSL=true&requireSSL=true&serverTimezone=UTC&characterEncoding=UTF-8
    username: admin
    password: 123456789
    driver-class-name: com.mysql.cj.jdbc.Driver
    hikari:
      maximum-pool-size: 10
      minimum-idle: 2
      connection-timeout: 5000
      idle-timeout: 300000
      max-lifetime: 600000

  jpa:
    hibernate:
      ddl-auto: update   # dùng 'validate' khi đã ổn định schema
    properties:
      hibernate:
        dialect: org.hibernate.dialect.MySQLDialect
        format_sql: true
    show-sql: false
    open-in-view: false

app:
  aws:
    region: us-east-1
    s3:
      bucket-name: s3-document-manage-bucket
      presign-upload-expiry-minutes: 10
      presign-download-expiry-minutes: 15
  upload:
    max-file-size-bytes: 52428800   # 50MB — khớp với FileValidator và Frontend
    allowed-extensions: pdf,doc,docx,xls,xlsx,ppt,pptx,png,jpg,jpeg,txt
  cors:
    allowed-origins: http://127.0.0.1:5500,http://localhost:5500
```

3. Implement the REST controller with the four core endpoints listed in 5.4.1 (`upload`, `confirm`, `list`, `download`, `delete`), using the AWS SDK's `S3Client` to read/write objects and Spring Data JPA to persist metadata.
4. Package the application:

```bash
mvn clean package -DskipTests
```

The resulting `.jar` file (in `target/`) will be deployed to the backend EC2 instance in section 5.4.4.

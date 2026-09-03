---
title: "Designing the Metadata Database"
date: 2026-07-21
weight: 3
chapter: false
pre: " <b> 5.3.3. </b> "
---

# 5.3.3. Designing the Metadata Database

Connect to the RDS endpoint using your MySQL client, then create the schema:

```sql
CREATE DATABASE docMetadata;

USE docMetadata;

CREATE TABLE documents (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,

    original_file_name VARCHAR(255) NOT NULL,

    stored_key VARCHAR(512) NOT NULL UNIQUE,

    content_type VARCHAR(100) NOT NULL,

    file_size BIGINT NOT NULL,

    status VARCHAR(20) NOT NULL,

    created_at DATETIME NOT NULL,

    updated_at DATETIME NOT NULL
);

CREATE INDEX idx_documents_status
ON documents(status);
CREATE INDEX idx_documents_stored_key
ON documents(stored_key);
```

* `documents`: It stores all data about the uploaded file, including `stored_key` to upload the actual file to S3.
![RDS](/images/5-Workshop/5.3-S3-RDS/rds_metadata.png)
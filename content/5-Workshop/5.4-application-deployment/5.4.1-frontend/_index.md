---
title: "Building the Frontend"
date: 2026-07-21
weight: 1
chapter: false
pre: " <b> 5.4.1. </b> "
---

# 5.4.1. Building the Frontend

1. Initialize the frontend project (e.g. React, or plain HTML/CSS/JS) with three core screens: **Login/Register**, **File List**, and **Upload**.
2. Configure the API base URL to point to the backend ALB DNS name (created in section 5.5.3):

```javascript
// config.js
export const API_BASE_URL = "";
```

3. Implement the calls to the backend REST API:
   * `POST /api/documents/presign-upload` — create file metadata and generate a pre-signed URL for uploading the file to Amazon S3
   * `PUT "https://bucket-name.s3.us-east-1.amazonaws.com/documents/{year}/{month}/{day}/uploadUrl"` — upload the file to Amazon S3
   * `POST /api/documents/{id}/confirm` — confirm that the file has been successfully uploaded to Amazon S3
   * `GET /api/documents/{id}/download-url` — generate a URL to download the file
   * `GET /api/documents` — retrieve the list of files
   * `DELETE /api/documents/{id}` — delete the file

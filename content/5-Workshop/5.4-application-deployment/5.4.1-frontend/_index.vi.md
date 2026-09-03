---
title: "Xây dựng Frontend"
date: 2026-07-21
weight: 1
chapter: false
pre: " <b> 5.4.1. </b> "
---

# 5.4.1. Xây dựng Frontend

1. Khởi tạo project frontend (React, hoặc HTML/CSS/JS thuần) với 3 màn hình chính: **Đăng nhập/Đăng ký**, **Danh sách file**, và **Tải lên**.
2. Cấu hình API base URL trỏ đến tên DNS của backend ALB (được tạo ở mục 5.5.3):

```javascript
// config.js
export const API_BASE_URL = "";
```

3. Triển khai các lệnh gọi tới REST API của backend:
   * `POST /api/documents/presign-upload` — tạo metadata cho file và đường dẫn để tải file lên s3
   * `PUT "https://ten-bucket.s3.us-east-1.amazonaws.com/documents/{year}/{month}/{day}/uploadUrl"` - tải file lên s3
   * `POST /api/documents/{id}/confirm` — xác nhận file đã tải lên s3
   * `GET /api/documents/{id}/download-url` — tải file xuống
   * `GET /api/documents` - lấy danh sách file
   * `DELETE /api/documents/{id}` — xóa file


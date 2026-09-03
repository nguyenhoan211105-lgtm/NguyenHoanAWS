---
title: "Kiểm thử chức năng Upload"
date: 2026-07-21
weight: 1
chapter: false
pre: " <b> 5.6.1. </b> "
---

# 5.6.1. Kiểm thử chức năng 

## Upload
1. Mở DNS name của frontend ALB trên trình duyệt và đăng nhập (hoặc đăng ký tài khoản mới).
2. Ở màn hình **Upload**, chọn một file thử nghiệm và gửi lên.
3. Kiểm tra:
   * File xuất hiện ở màn hình **Danh sách file** với đúng tên và dung lượng.
   * Có bản ghi tương ứng trong bảng `files` trên RDS (truy vấn bằng MySQL client).
   * Object tồn tại trong S3 bucket đúng key mong đợi (kiểm tra trên S3 console).
   ![test](/images/5-Workshop/5.6-testing-cleanup/test.png)
   ![test](/images/5-Workshop/5.6-testing-cleanup/test_02.png)
   ![test](/images/5-Workshop/5.6-testing-cleanup/test_03.png)
   ![test](/images/5-Workshop/5.6-testing-cleanup/test_04.png)
   ![test](/images/5-Workshop/5.6-testing-cleanup/test_05.png)
   ![test](/images/5-Workshop/5.6-testing-cleanup/test_06.png)
## Download
1. Từ màn hình **Danh sách file**, nhấn **Download** file đã tải lên ở bước trước.
2. Kiểm tra file tải về mở được bình thường và nội dung/dung lượng khớp với file gốc.
   ![test](/images/5-Workshop/5.6-testing-cleanup/test_07.png)

## Delete
1. Từ màn hình **Danh sách file**, nhấn **Delete** file thử nghiệm.
2. Kiểm tra:
   * File không còn xuất hiện ở màn hình **Danh sách file**.
   * Bản ghi tương ứng đã bị xóa khỏi bảng `files` trên RDS.
   * Object tương ứng đã bị xóa khỏi S3 bucket.
   ![test](/images/5-Workshop/5.6-testing-cleanup/test_08.png)
   ![test](/images/5-Workshop/5.6-testing-cleanup/test_09.png)
   ![test](/images/5-Workshop/5.6-testing-cleanup/test_10.png)
   ![test](/images/5-Workshop/5.6-testing-cleanup/test_11.png)
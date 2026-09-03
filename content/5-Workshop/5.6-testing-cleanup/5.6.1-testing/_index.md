---
title: "Testing the Upload Feature"
date: 2026-07-21
weight: 1
chapter: false
pre: " <b> 5.6.1. </b> "
---

## 5.6.1. Testing the Feature

# Upload
1. Open the frontend ALB's DNS name in a browser and log in (or register a new account).
2. On the **Upload** screen, select a test file and submit.
3. Verify:
   * The file appears in the **File List** screen with the correct name and size.
   * A matching row exists in the `files` table in RDS (query via your MySQL client).
   * The object exists in the S3 bucket under the expected key (check the S3 console).
   ![test](/images/5-Workshop/5.6-testing-cleanup/test.png)
   ![test](/images/5-Workshop/5.6-testing-cleanup/test_02.png)
   ![test](/images/5-Workshop/5.6-testing-cleanup/test_03.png)
   ![test](/images/5-Workshop/5.6-testing-cleanup/test_04.png)
   ![test](/images/5-Workshop/5.6-testing-cleanup/test_05.png)
   ![test](/images/5-Workshop/5.6-testing-cleanup/test_06.png)

# Download
1. From the **File List** screen, click **Download** on the file uploaded in the previous step.
2. Verify the downloaded file opens correctly and its content and size match the original file.
   ![test](/images/5-Workshop/5.6-testing-cleanup/test_07.png)

# Delete
1. From the **File List** screen, click **Delete** on the test file.
2. Verify:
   * The file no longer appears in the **File List** screen.
   * The corresponding row has been removed from the `files` table in RDS.
   * The object has been removed from the S3 bucket.
   ![test](/images/5-Workshop/5.6-testing-cleanup/test_08.png)
   ![test](/images/5-Workshop/5.6-testing-cleanup/test_09.png)
   ![test](/images/5-Workshop/5.6-testing-cleanup/test_10.png)
   ![test](/images/5-Workshop/5.6-testing-cleanup/test_11.png)

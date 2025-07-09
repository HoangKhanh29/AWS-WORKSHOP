---
title : "OPTION 1: Hệ thống Cơ bản"
date: 2025-06-18
weight : 3 
chapter : false
pre : " <b> 3. </b> "
---

Trong **Option 1**, chúng ta sẽ xây dựng một hệ thống thông báo file cơ bản sử dụng kiến trúc serverless. Hệ thống này sẽ tự động gửi email thông báo mỗi khi có file mới được upload lên S3 bucket.

**Kiến trúc hệ thống:**
- **S3 Bucket**: Lưu trữ file và tạo event khi có file mới
- **Lambda Function**: Xử lý event từ S3 và gửi thông báo
- **SNS Topic**: Gửi email thông báo đến người dùng

**Luồng hoạt động:**
1. User upload file lên S3 Bucket
2. S3 tạo event và trigger Lambda Function
3. Lambda xử lý event và gửi message đến SNS Topic
4. SNS gửi email thông báo đến subscriber

![serverless-upload-notification](/images/serverless-upload-notification.png)

### Nội dung
3.1. [Tạo S3 Bucket](3.1-Create-S3-Bucket/) \
3.2. [Tạo SNS Topic](3.2-Create-SNS-Topic/) \
3.3. [Tạo Lambda Function](3.3-Create-Lambda-Function/)
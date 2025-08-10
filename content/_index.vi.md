---
title : "Serverless File System"
date: 2025-06-18
weight : 1 
chapter : false
---
# Xử lý dữ liệu thời gian thực với Kinesis, Lambda và S3

### Tổng quan

Workshop này hướng dẫn bạn xây dựng một hệ thống thông báo và quản lý tệp serverless sử dụng các dịch vụ AWS. Có hai cấp độ triển khai:

- Option 1 (Cơ bản): Xử lý sự kiện tải file lên S3, kích hoạt Lambda Function, và gửi thông báo qua SNS đến email.
- Option 2 (Nâng cao): Hệ thống mở rộng với DynamoDB, SQS, API Gateway, CloudWatch và giao diện web để quản lý tệp đầy đủ tính năng.

Khuyến nghị: Bắt đầu với Option 1 để nắm các khái niệm serverless cơ bản, sau đó chuyển sang Option 2 để khám phá các tính năng nâng cao.

![ConnectPrivate](/images/log-arrc.jpg) 

### Nội dung

### Content
 1. [Introduction](1-introduce/)
 2. [Preparation](2-Prerequiste/)
 3. [Setting-create-s3](3-setting-create-s3/)
 4. [Setting-up-kinesis](4-setting-up-kinesis/)
 5. [Logging-with-cloudwatch](5-logging-with-cloudwatch/)
 6. [Cleaning-up-resources](6-cleanup/)
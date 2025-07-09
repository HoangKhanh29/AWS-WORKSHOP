---
title : "Serverless File System"
date: 2025-06-18
weight : 1 
chapter : false
---
# Xây dựng Hệ thống Thông báo và Quản lý File Serverless với AWS S3, Lambda, SNS, DynamoDB và API Gateway

### Tổng quan

Workshop này hướng dẫn bạn xây dựng một hệ thống thông báo và quản lý tệp serverless sử dụng các dịch vụ AWS. Có hai cấp độ triển khai:

- Option 1 (Cơ bản): Xử lý sự kiện tải file lên S3, kích hoạt Lambda Function, và gửi thông báo qua SNS đến email.
- Option 2 (Nâng cao): Hệ thống mở rộng với DynamoDB, SQS, API Gateway, CloudWatch và giao diện web để quản lý tệp đầy đủ tính năng.

Khuyến nghị: Bắt đầu với Option 1 để nắm các khái niệm serverless cơ bản, sau đó chuyển sang Option 2 để khám phá các tính năng nâng cao.

![aws_serverless_workshop_landscape](/images/aws_serverless_workshop_landscape.png) 

### Nội dung

 1. [Giới thiệu](1-introduce/)
 2. [Các bước chuẩn bị](2-Prerequiste/)
 3. [OPTION 1: Hệ thống Cơ bản](3-Option_1/).
 4. [OPTION 2: Hệ thống Nâng Cao](4.Option_2/)
 5. [Test Hệ thống](5-Test-System/)
 6. [Dọn dẹp tài nguyên](6-cleanup/)
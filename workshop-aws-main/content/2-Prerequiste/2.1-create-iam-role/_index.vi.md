---
title : "Tạo IAM"
date: 2025-06-18
weight : 1
chapter : false
pre : " <b> 2.1 </b> "
---

Trong bước này, chúng ta cần tạo IAM Role, gán quyền **S3 Full Access**, **Kinesis Full Access** và **CloudWatch Full Access**. Gán role `data-role` cho cả ba Lambda function: **Producer**, **Customer#1** và **Customer#2** để đảm bảo khả năng truy cập các dịch vụ cần thiết.

Sau khi hoàn thành bước này, sơ đồ kiến trúc tổng quan sẽ như sau:

## Tạo IAM Role

1. Truy cập [Create IAM Role](https://us-east-1.console.aws.amazon.com/iam/homeregion=ap-southeast-1#/roles/create)  
    - Nhấp vào **IAM**.  
    - Nhấp **Create Role**.  
    - Chọn **AWS service**, sau đó chọn **Lambda** để xác nhận.  

![ConnectPrivate](/images/2.prerequisite/A-1.jpg)  
![ConnectPrivate](/images/2.prerequisite/A-2.jpg)  
![ConnectPrivate](/images/2.prerequisite/A-3.png)  

2. Truy cập [Add permission](https://us-east-1.console.aws.amazon.com/iam/home?region=ap-southeast-1#/roles/create?trustedEntityType=AWS_SERVICE&selectedService=Lambda&selectedUseCase=Lambda)  
    - Chọn **CloudWatchFullAccess**.  
    - Chọn **AmazonS3FullAccess**.  
    - Chọn **AmazonKinesisFullAccess**.  

![ConnectPrivate](/images/2.prerequisite/A-4.png)  
![ConnectPrivate](/images/2.prerequisite/A-5.png)  
![ConnectPrivate](/images/2.prerequisite/A-6.png)  

3. Truy cập [Name, review, and create](https://us-east-1.console.aws.amazon.com/iam/home?region=ap-southeast-1#/roles/create?trustedEntityType=AWS_SERVICE&selectedService=Lambda&selectedUseCase=Lambda)  
    - Đặt tên **data-streaming-system-role**.  
    - Nhấp **Create Role**.  

![ConnectPrivate](/images/2.prerequisite/A-7.png)  
![ConnectPrivate](/images/2.prerequisite/A-8.png)  
![ConnectPrivate](/images/2.prerequisite/A-9.png)  

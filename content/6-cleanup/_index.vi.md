---
title : "Dọn dẹp tài nguyên"
date: 2025-06-18
weight : 6
chapter : false
pre : " <b> 6. </b> "
---

Chúng ta sẽ thực hiện các bước sau để xóa các tài nguyên đã tạo trong bài thực hành này.

## Xóa S3 Bucket
Vào [Amazon S3](https://ap-southeast-1.console.aws.amazon.com/s3/home?region=ap-southeast-1)  
  - Click **Instances**.  
  - Click tên **jinmeister-datasource**.  
  - Nhập lại tên S3 sau đó xóa.  
  - Click **Delete bucket**.  
  ![ConnectPrivate](/images/6.clean/Delete-S3-1.png)  
  ![ConnectPrivate](/images/6.clean/Delete-S3-2.png)  
  ![ConnectPrivate](/images/6.clean/Delete-S3-3.png)  

## Xóa Lambda
Vào [Lambda](https://ap-southeast-1.console.aws.amazon.com/lambda/home?region=ap-southeast-1#/applications)  
  - Click **Applications**.  
  - Chọn **Producer**, **Consumer#1** và **Consumer#2**.  
  - Click **Actions** sau đó nhập **Delete**.  
  ![ConnectPrivate](/images/6.clean/Delete-lambda.png)  

## Xóa IAM role
  - Click **Roles**.  
  - Click role **namedata-streaming-system-role** sau đó click **Delete**, nhập lại tên và xóa.  
  ![ConnectPrivate](/images/6.clean/Delete-Iam1.png)  
  ![ConnectPrivate](/images/6.clean/Delete-Iam2.png)  

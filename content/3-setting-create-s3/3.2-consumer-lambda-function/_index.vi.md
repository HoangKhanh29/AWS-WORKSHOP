---
title : "Lambda Function cho Consumer"
date: 2025-06-18
weight : 2
chapter : false
pre : " <b> 3.2 </b> "
---

1. Truy cập [Create S3](https://ap-southeast-1.console.aws.amazon.com/s3/home?region=ap-southeast-1).  
    - Vào bucket **jinmeister-datasource**.  
    - Nhấp **Properties**.  
    - Nhấp **Event Notifications**.  
    - Nhấp **Create event notification**.  
    ![ConnectPrivate](/images/3.s3/B-10.png)  
    ![ConnectPrivate](/images/3.s3/C-1.1.png)  
    ![ConnectPrivate](/images/3.s3/C-2.2.png)  
    ![ConnectPrivate](/images/3.s3/C-3.png)  

2. Vào **Create Event Notification**  
    - Name: **data-upload** / `.txt`.  
    - Chọn **All object create events**.  
    - Chọn **Lambda Function**.  
    - Nhấp **choose from your Lambda function**.  
    - Lambda function: **producer**.  
    ![ConnectPrivate](/images/3.s3/C-4.1.png)  
    ![ConnectPrivate](/images/3.s3/C-5.png)  
    ![ConnectPrivate](/images/3.s3/C-6.png)  
    ![ConnectPrivate](/images/3.s3/C-7.1.png)  

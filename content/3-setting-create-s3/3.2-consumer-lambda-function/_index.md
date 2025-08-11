---
title : "Cosumer Lambda Function"
date: 2025-06-18
weight : 2
chapter : false
pre : " <b> 3.2 </b> "
---

 1. Go to [Create S3](https://ap-southeast-1.console.aws.amazon.com/s3/home?region=ap-southeast-1).
    - Go to jinmeister-datasource.
    - Click Properties
    - Click Event Notifications
    - Click Create event notification
    ![ConnectPrivate](/images/3.s3/B-10.png)  
    ![ConnectPrivate](/images/3.s3/C-1.1.png)
    ![ConnectPrivate](/images/3.s3/C-2.2.png)  
    ![ConnectPrivate](/images/3.s3/C-3.png)

2. Go to **Create Event Notification**
    - Name: data-upload / .txt .
    - Click All object create events.
    - Click Lambada Function.
    - Click choose from your Lambda function.
    - Lambda function: producer.
    ![ConnectPrivate](/images/3.s3/C-4.1.png)
    ![ConnectPrivate](/images/3.s3/C-5.png)
    ![ConnectPrivate](/images/3.s3/C-6.png)
    ![ConnectPrivate](/images/3.s3/C-7.1.png)


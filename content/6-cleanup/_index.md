---
title : "Clean up resources"
date: 2025-06-18
weight : 6
chapter : false
pre : " <b> 6. </b> "
---

We will take the following steps to delete the resources we created in this exercise.

## Delete S3 Bucket
Go to [Amazon S3](https://ap-southeast-1.console.aws.amazon.com/s3/home?region=ap-southeast-1)
  - Click **Instances**.
  - Click Name **jinmeister-datasource**.
  - Enter the S3 name and then delete.
  - Click Delete bucket.
  ![ConnectPrivate](/images/6.clean/Delete-S3-1.png)  
  ![ConnectPrivate](/images/6.clean/Delete-S3-2.png)  
  ![ConnectPrivate](/images/6.clean/Delete-S3-3.png)  

## Delete Lambda
Go to [Lambda](https://ap-southeast-1.console.aws.amazon.com/lambda/home?region=ap-southeast-1#/applications)
  - Click **Applications**.
  - Click to select **Producer**, **Consumer#1** and **Consumer#2**.
  - Click **Actions** then enter **Delete**.
  ![ConnectPrivate](/images/6.clean/Delete-lambda.png) 

## Delete IAM role
  - Click **Roles**.
  - Click Roles **namedata-streaming-system-role** then Click **Delete**, Re-enter the name and delete
  ![ConnectPrivate](/images/6.clean/Delete-Iam1.png) 
  ![ConnectPrivate](/images/6.clean/Delete-Iam2.png) 
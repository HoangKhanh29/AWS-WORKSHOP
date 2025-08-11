---
title : "Create Iam"
date: 2025-06-18
weight : 1
chapter : false
pre : " <b> 2.1 </b> "
---
In this step, we need to create the IM role, assign permissions to S3 Full Access, Kinesis Full Access, and CloudWatch Full Access. Assign the data-role to all three Lambda functions: Producer, Customer#1, and Customer#2 to ensure access to the necessary services.

The architecture overview after you complete this step will be as follows:
## Create IAM role

1. Go to [Create IAM Role](https://us-east-1.console.aws.amazon.com/iam/homeregion=ap-southeast-1#/roles/create)
    - Click Iam.
    - Click Create Role.
    - Click AWS service, then click Lambda to confirm. 
   
![ConnectPrivate](/images/2.prerequisite/A-1.jpg) 
![ConnectPrivate](/images/2.prerequisite/A-2.jpg)
![ConnectPrivate](/images/2.prerequisite/A-3.png)

2. Go to [Add permission](https://us-east-1.console.aws.amazon.com/iam/home?region=ap-southeast-1#/roles/create?trustedEntityType=AWS_SERVICE&selectedService=Lambda&selectedUseCase=Lambda)
    - Click **CloudWatchFullAccess**.
    - Click **AmazonS3FullAccess**.
    - Click **AmazonKinesisFullAccess**.

![ConnectPrivate](/images/2.prerequisite/A-4.png) 
![ConnectPrivate](/images/2.prerequisite/A-5.png)
![ConnectPrivate](/images/2.prerequisite/A-6.png)

3. Go to [Name, review, and create](https://us-east-1.console.aws.amazon.com/iam/home?region=ap-southeast-1#/roles/create?trustedEntityType=AWS_SERVICE&selectedService=Lambda&selectedUseCase=Lambda)
    - Name data-streaming-system-role..
    - Click Create Role

![ConnectPrivate](/images/2.prerequisite/A-7.png) 
![ConnectPrivate](/images/2.prerequisite/A-8.png)
![ConnectPrivate](/images/2.prerequisite/A-9.png)
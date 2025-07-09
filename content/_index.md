---
title : "Serverless File System"
date: 2025-06-18
weight : 1 
chapter : false
---
# Build a Serverless File Notification and Management System with AWS S3, Lambda, SNS, DynamoDB, and API Gateway

### Overall
This workshop guides you through building a serverless notification and file management system using AWS services. There are two levels of deployment:

- Option 1 (Basic): Process file upload events to S3, trigger a Lambda Function, and send notifications via SNS to email.
- Option 2 (Advanced): An expanded system with DynamoDB, SQS, API Gateway, CloudWatch, and a web interface for full-featured file management.management.

Recommendation: Start with Option 1 to understand basic serverless concepts, then move to Option 2 to explore advanced features.

![ConnectPrivate](/images/aws_serverless_workshop_landscape.png) 

### Content
 1. [Introduction](1-introduce/)
 2. [Preparation](2-prerequiste/)
 3. [OPTION 1: Basic System](3-Option_1/)
 4. [OPTION 2: Advanced System](4.Option_2/)
 5. [Test System](5-Test-System/)
 6. [Resource Cleanup](6-cleanup/)
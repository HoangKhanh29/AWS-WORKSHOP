---
title : "OPTION 1: Basic System"
date: 2025-06-18
weight : 3 
chapter : false
pre : " <b> 3. </b> "
---

In **Option 1**, we will build a basic file notification system using serverless architecture. This system will automatically send email notifications whenever a new file is uploaded to the S3 bucket.

**System Architecture:**
- **S3 Bucket**: Store files and generate events when new files are added
- **Lambda Function**: Process events from S3 and send notifications
- **SNS Topic**: Send email notifications to users

**Workflow:**
1. User uploads file to S3 Bucket
2. S3 creates event and triggers Lambda Function
3. Lambda processes event and sends message to SNS Topic
4. SNS sends email notification to subscribers

![serverless-upload-notification](/images/serverless-upload-notification.png)

### Contents
3.1. [Create S3 Bucket](3.1-Create-S3-Bucket/) \
3.2. [Create SNS Topic](3.2-Create-SNS-Topic/) \
3.3. [Create Lambda Function](3.3-Create-Lambda-Function/)
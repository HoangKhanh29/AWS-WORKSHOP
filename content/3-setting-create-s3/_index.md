---
title : "Setting Create S3"
date: 2025-06-18
weight : 3 
chapter : false
pre : " <b> 3. </b> "
---

In this step, S3 Bucket: You create an S3 bucket named jinmeister-datasource. The bucket is versioned, ensuring that object versions are stored. Bucket encryption is enabled to secure data at rest. Event Notifications: In S3, an event notification named data-upload is created, which triggers the producer Lambda function whenever a new .txt file is uploaded to the bucket. This setup ensures that any new file upload triggers data processing.

### Contents
3.1. [Create S3](3.1-Create-S3-Bucket/) \
3.2. [Consumer Lambda Function](3.2-Create-SNS-Topic/) \
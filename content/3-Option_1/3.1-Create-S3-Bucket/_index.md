---
title : "Create S3 Bucket"
date: 2025-06-18
weight : 1 
chapter : false
pre : " <b> 3.1. </b> "
---

1. Search for **S3** in **AWS Console** and select **S3** service.
![Picture1](/images/3.1/image1.png)

2. On the **S3** page, click **Create bucket**:
![Picture2](/images/3.1/image2.png)
- **AWS Region**: Confirm it's **Asia Pacific (Singapore) ap-southeast-1**. (If wrong, change it immediately).
- **Bucket name**: `yourname-serverless-workshop-2025` (replace yourname with your name).
    - This is a globally unique name for your **Bucket**.
    - **IMPORTANT**: Bucket name must be lowercase, no spaces, only lowercase letters, numbers and hyphens (-).
- **Object Ownership**: Select **ACLs enabled** and **Bucket owner preferred**.
![Picture3](/images/3.1/image3.png)
![Picture4](/images/3.1/image4.png)

- **Block Public Access settings** for this bucket: 
    - Keep default (ALL options are **CHECKED**). We don't want this bucket to be publicly accessible from the Internet as it's only used to trigger **Lambda**.
- Other options (**Versioning**, **Tags**, **Default encryption**, **Advanced settings**): Keep default.
![Picture5](/images/3.1/image5.png)
- **Versioning**: Disabled

3. Click **Create bucket**.
![Picture6](/images/3.1/image6.png)
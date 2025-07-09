---
title : "Create SNS Topic"
date: 2025-06-18
weight : 2
chapter : false
pre : " <b> 3.2. </b> "
---

1. Search for **SNS** and select **Amazon SNS (Simple Notification Service)**.
![Picture8](/images/3.2/image8.png)

2. Click **Create topic**:
![Picture9](/images/3.2/image9.png)
- **Type**: Standard.
- **Name**: `FileUploadNotifications`.
![Picture10](/images/3.2/image10.png)

3. Click **Create topic** and **Copy ARN** for later use (example: `arn:aws:sns:ap-southeast-1:123456789012:FileUploadNotifications`)
![Picture12](/images/3.2/image12.png)

4. Create subscription:
- Click **Create subscription**.
![Picture13](/images/3.2/image13.png)
- **Protocol**: Email.
- **Endpoint**: Enter your email address.
- Click **Create subscription**.
![Picture16](/images/3.2/image16.png)
![Picture14](/images/3.2/image14.png)

5. Check your email and click **Confirm subscription**. (If you don't see the email, check spam folder!)
![Picture18](/images/3.2/image18.png)
![Picture20](/images/3.2/image20.png)
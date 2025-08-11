---
title : "Logg With CloudWatch"
date: 2025-06-18
weight : 5
chapter : false
pre : " <b> 5. </b> "
---

1. Create new file **Test.txt.**
![ConnectPrivate](/images/5.log-cloudwatch/file-test.png)
2. Go to **Amazon S3**
    - Click **Objects**.
    - Click **Upload**.
    ![ConnectPrivate](/images/5.log-cloudwatch/E-1.png)
    - Click **Add files** then Click file **test.file** previously created file
    ![ConnectPrivate](/images/5.log-cloudwatch/E-3.png)
    ![ConnectPrivate](/images/5.log-cloudwatch/E-4.png)
    ![ConnectPrivate](/images/5.log-cloudwatch/E-2.png)
3. Go back lambda **Producer**
    - Click log streams.
    - Select a timed log stream that matches the time you uploaded the file to check.
    ![ConnectPrivate](/images/5.log-cloudwatch/E-5.png)
    ![ConnectPrivate](/images/5.log-cloudwatch/E-6.png)
    - Go to back lambda **Cosumer#1** and **consumer#2**
    - Select a timed log stream that matches the time you uploaded the file to check.
    ![ConnectPrivate](/images/5.log-cloudwatch/E-7.png)
    ![ConnectPrivate](/images/5.log-cloudwatch/E-8.png)
    - A new file was successfully added to an S3 bucket
    ![ConnectPrivate](/images/5.log-cloudwatch/E-9.png)
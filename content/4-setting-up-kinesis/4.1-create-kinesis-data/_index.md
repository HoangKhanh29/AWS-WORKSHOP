---
title : "Create Kinesis Data"
date: 2025-06-18
weight : 1
chapter : false
pre : " <b> 4.1 </b> "
---

## Create Kinesis Data

1. Go to [Create Kinesis](https://ap-southeast-1.console.aws.amazon.com/kinesis/home?region=ap-southeast-1#/streams/create)
    - Search **Kinesis**.
    - Click **Create data stream**.
    ![ConnectPrivate](/images/4.kinesis/C-8.png)
    ![ConnectPrivate](/images/4.kinesis/C-9.png)

2. Go to **Data stream configuration**
    - Name: **jinmeister-data-stream**.
    - Click **Provisioned**.
    - Provisioned shards : 2.
    ![ConnectPrivate](/images/4.kinesis/C-10.1.png)

3. Go to **jinmeister-data-stream**
    - Complate **Create Kinesis**
    - Click **Configuration**
    - Click **Encryption** and Click **Edit**
    ![ConnectPrivate](/images/4.kinesis/C-10.2.png)
    ![ConnectPrivate](/images/4.kinesis/D-2.png)
    - Click **Enable server-side encryption**
    - Click **Save Changes**
    ![ConnectPrivate](/images/4.kinesis/D-2.2.png)
    ![ConnectPrivate](/images/4.kinesis/D-3.3.png)
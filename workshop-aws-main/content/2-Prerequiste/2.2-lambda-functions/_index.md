---
title : "Create Lambda Functions"
date: 2025-06-18
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

## Create Lambda Functions
In this step, after creating Role, we will create Lambda, producer and select data-role to perform the execution role. This function will listen for events from S3, read data from objects uploaded in S3, and send this data to the Kinesis stream. Lambda function for consumers: You create two additional Lambda functions for two consumers, customer #1 and customer #2, to process data from the Kinesis stream.

1. Go to [Lambda](https://ap-southeast-1.console.aws.amazon.com/lambda/home?region=ap-southeast-1#/create/function?firstrun=true)
    - Search **Lambda**.
    - Click **Lambda**, then click **Create a function** to confirm.

![ConnectPrivate](/images/2.prerequisite/B-1.png)
![ConnectPrivate](/images/2.prerequisite/B-2.png)

2. Go to [Create function](https://ap-southeast-1.console.aws.amazon.com/lambda/home?region=ap-southeast-1#/create/function?firstrun=true&intent=authorFromScratch)
    - Create:producer,customer#1,customer#2 /Name: **producer,customer#1,customer#2**.
    - Click **Node.js 20.x**
    - Click **Use an existing role**
    - Click **data-streaming-system-role**

![ConnectPrivate](/images/2.prerequisite/B-3.png)
![ConnectPrivate](/images/2.prerequisite/B-4.png)
![ConnectPrivate](/images/2.prerequisite/B-5.png)
![ConnectPrivate](/images/2.prerequisite/B-6.png)
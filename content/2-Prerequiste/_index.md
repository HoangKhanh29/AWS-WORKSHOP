---
title : "Preparation"
date: 2025-06-18
weight : 2
chapter : false
pre : " <b> 2. </b> "
---

## Preparation

{{% notice info %}}
You need to prepare the initial AWS resources, including creating an IAM Role with the necessary permissions for Kinesis and Lambda Functions.
{{% /notice %}}

To allow Lambda Functions to manage and process data from Kinesis and store data in S3, we need to set up an IAM Role that grants permissions for these services. In this preparation step, we will first create an IAM Role to ensure that Lambda has the required permissions to work with Kinesis and S3. After that, we will proceed to configure services like Kinesis.

### Content
2.1. [Create IAM Role](2.1-create-iam-role/) \
2.2. [Create Lambada Functions](2.2-lambda-functions/)
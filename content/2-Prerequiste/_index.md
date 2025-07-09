---
title : "Prerequisites"
date: 2025-06-18
weight : 2
chapter : false
pre : " <b> 2. </b> "
---

## Preparation Overview

To successfully complete this workshop, you need to prepare all prerequisites regarding **AWS** account, working environment, and basic knowledge. This section will provide detailed step-by-step preparation guidance.

## 1. AWS Account

### Account Requirements:
- **AWS Account** that has been verified (can be Free Tier)
- **Credit card** registered (for verification, no charges if within Free Tier)
- **Email access** to receive notifications from **AWS**

### AWS Free Tier Coverage:
This workshop is designed to run entirely within **AWS Free Tier**:

| Service | Free Tier Limit | Workshop Usage |
|---------|----------------|----------------|
| **S3** | 5GB storage, 20,000 GET requests | < 1GB, < 100 requests |
| **Lambda** | 1M requests/month, 400,000 GB-seconds | < 1,000 requests |
| **SNS** | 1,000 email notifications | < 50 notifications |
| **DynamoDB** | 25GB storage, 25 RCU/WCU | < 1GB, minimal operations |
| **API Gateway** | 1M API calls | < 100 calls |
| **CloudWatch** | 10 custom metrics, 5GB logs | < 5 metrics, < 1GB logs |

{{% notice info %}}
**Estimated cost**: $0 if within Free Tier, < $1 USD if exceeding Free Tier limits.
{{% /notice %}}

### Setting up IAM Permissions:

To complete this workshop, your **AWS** account needs the following permissions:

#### **Minimum Required Permissions:**
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:CreateBucket",
                "s3:DeleteBucket",
                "s3:PutObject",
                "s3:GetObject",
                "s3:PutBucketNotification",
                "lambda:CreateFunction",
                "lambda:DeleteFunction",
                "lambda:UpdateFunctionCode",
                "lambda:AddPermission",
                "sns:CreateTopic",
                "sns:DeleteTopic",
                "sns:Subscribe",
                "sns:Publish",
                "iam:CreateRole",
                "iam:AttachRolePolicy",
                "iam:PassRole"
            ],
            "Resource": "*"
        }
    ]
}
```

#### **Recommended Approach:**
- Use **Administrator Access** for workshop (easiest)
- Or create **Custom Policy** with above permissions
- Avoid using **Root Account** for security best practices

## 2. Working Environment

### Browser Requirements:
- **Modern browser**: Chrome 90+, Firefox 88+, Safari 14+, Edge 90+
- **JavaScript enabled**
- **Cookies enabled** for **AWS Console**
- **Pop-up blocker disabled** for AWS domains

### Network Requirements:
- **Stable internet connection** (minimum 1 Mbps)
- **Access to AWS endpoints** (not blocked by firewall)
- **HTTPS support** (TLS 1.2+)

### Recommended Tools:
- **Text editor** with syntax highlighting (VS Code, Sublime Text...)
- **JSON formatter** extension or online tool
- **AWS CLI** (optional, for advanced users)

## 3. Basic Knowledge

### **AWS Fundamentals:**
You should understand the following concepts:

#### **AWS Regions and Availability Zones:**
- **Region**: Geographical area with multiple data centers
- **AZ**: Isolated data center within a region
- **Workshop region**: **ap-southeast-1 (Singapore)**

#### **AWS Services Overview:**
- **Compute**: EC2, Lambda, Fargate
- **Storage**: S3, EBS, EFS
- **Database**: RDS, DynamoDB, ElastiCache
- **Networking**: VPC, CloudFront, Route 53
- **Security**: IAM, KMS, Secrets Manager

### **JSON and REST APIs:**
```json
{
    "eventVersion": "2.1",
    "eventSource": "aws:s3",
    "eventName": "ObjectCreated:Put",
    "eventTime": "2025-01-15T10:30:00.000Z",
    "s3": {
        "bucket": {
            "name": "my-serverless-bucket"
        },
        "object": {
            "key": "uploads/document.pdf",
            "size": 1024
        }
    }
}
```

### **Python Basics (for Lambda):**
```python
import json
import boto3

def lambda_handler(event, context):
    # Process S3 event
    bucket = event['Records'][0]['s3']['bucket']['name']
    key = event['Records'][0]['s3']['object']['key']
    
    # Business logic here
    print(f"File {key} uploaded to {bucket}")
    
    return {
        'statusCode': 200,
        'body': json.dumps('Success')
    }
```

## 4. AWS Console Configuration

### Region Setup:
1. Log in to **AWS Console**
2. Select region **Asia Pacific (Singapore) - ap-southeast-1**
3. **IMPORTANT**: All resources must be created in the same region

### Console Navigation:
- **Services menu**: Find services quickly
- **Recently visited**: Access previously used services
- **Favorites**: Pin frequently used services
- **Resource Groups**: Organize related resources

### Billing Setup:
1. Go to **Billing Dashboard**
2. Enable **Free Tier Usage Alerts**
3. Set up **Budget Alerts** (recommended: $5 threshold)
4. Review **Cost Explorer** to track spending

## 5. Email Configuration

### SNS Email Setup:
- **Valid email address** to receive notifications
- **Access to email** to confirm subscriptions
- **Check spam folder** if not receiving emails
- **Whitelist AWS domains**: 
  - `@sns.amazonaws.com`
  - `@aws.amazon.com`

### Email Testing:
Before starting the workshop, test email delivery:
1. Create test **SNS Topic**
2. Subscribe your email
3. Confirm subscription
4. Send test message
5. Verify email received

## 6. Troubleshooting Common Issues

### **Permission Errors:**
```
AccessDenied: User is not authorized to perform action
```
**Solution**: Check IAM permissions, ensure correct policies attached

### **Region Mismatch:**
```
Resource not found in specified region
```
**Solution**: Verify all resources created in **ap-southeast-1**

### **Free Tier Exceeded:**
```
Request would exceed Free Tier limits
```
**Solution**: Check **Billing Dashboard**, clean up unused resources

### **Email Not Received:**
- Check spam/junk folder
- Verify email address spelling
- Check email provider blocking AWS emails
- Try different email provider (Gmail, Outlook)

## 7. Pre-Workshop Checklist

Before starting the workshop, please verify:

### ✅ **Account Setup:**
- [ ] **AWS Account** active and verified
- [ ] **Credit card** added (for verification)
- [ ] **IAM permissions** configured
- [ ] **Billing alerts** set up

### ✅ **Environment:**
- [ ] **Browser** updated and compatible
- [ ] **Internet connection** stable
- [ ] **AWS Console** accessible
- [ ] **Region** set to **ap-southeast-1**

### ✅ **Knowledge:**
- [ ] Read the **Introduction** section
- [ ] Understand basic **AWS concepts**
- [ ] Familiar with **JSON format**
- [ ] **Email** ready to receive notifications

### ✅ **Tools:**
- [ ] **Text editor** available
- [ ] **AWS Console** bookmarked
- [ ] **Workshop materials** downloaded/accessible

## 8. Reference Documentation

### **AWS Documentation:**
- [AWS Lambda Developer Guide](https://docs.aws.amazon.com/lambda/)
- [AWS S3 Event Notifications](https://docs.aws.amazon.com/AmazonS3/latest/userguide/EventNotifications.html)
- [AWS SNS Developer Guide](https://docs.aws.amazon.com/sns/)
- [Amazon API Gateway Developer Guide](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html)
- [Amazon DynamoDB Developer Guide](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/)
- [Amazon SQS Developer Guide](https://docs.aws.amazon.com/sqs/)
- [Amazon CloudWatch Developer Guide](https://docs.aws.amazon.com/cloudwatch/)

### **Best Practices:**
- [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/)
- [Serverless Application Lens](https://docs.aws.amazon.com/wellarchitected/latest/serverless-applications-lens/)
- [AWS Security Best Practices](https://aws.amazon.com/architecture/security-identity-compliance/)

{{% notice tip %}}
If you encounter issues during preparation, please refer to **AWS Support** or **AWS Community Forums** for assistance.
{{% /notice %}}
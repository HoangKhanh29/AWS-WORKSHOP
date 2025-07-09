---
title : "Các bước chuẩn bị"
date: 2025-06-18
weight : 2
chapter : false
pre : " <b> 2. </b> "
---

## Tổng quan Chuẩn bị

Để thực hiện workshop thành công, bạn cần chuẩn bị đầy đủ các điều kiện tiên quyết về tài khoản **AWS**, môi trường làm việc, và kiến thức cơ bản. Phần này sẽ hướng dẫn chi tiết từng bước chuẩn bị.

## 1. Tài khoản AWS

### Yêu cầu Tài khoản:
- **AWS Account** đã được verify (có thể là Free Tier)
- **Credit card** đã được đăng ký (cho verification, không bị charge nếu trong Free Tier)
- **Email access** để nhận notifications từ **AWS**

### AWS Free Tier Coverage:
Workshop này được thiết kế để chạy hoàn toàn trong **AWS Free Tier**:

| Service | Free Tier Limit | Workshop Usage |
|---------|----------------|----------------|
| **S3** | 5GB storage, 20,000 GET requests | < 1GB, < 100 requests |
| **Lambda** | 1M requests/month, 400,000 GB-seconds | < 1,000 requests |
| **SNS** | 1,000 email notifications | < 50 notifications |
| **DynamoDB** | 25GB storage, 25 RCU/WCU | < 1GB, minimal operations |
| **API Gateway** | 1M API calls | < 100 calls |
| **CloudWatch** | 10 custom metrics, 5GB logs | < 5 metrics, < 1GB logs |

{{% notice info %}}
**Ước tính chi phí**: $0 nếu trong Free Tier, < $1 USD nếu vượt Free Tier limits.
{{% /notice %}}

### Thiết lập IAM Permissions:

Để thực hiện workshop, tài khoản **AWS** của bạn cần có các permissions sau:

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
- Sử dụng **Administrator Access** cho workshop (dễ nhất)
- Hoặc tạo **Custom Policy** với permissions trên
- Tránh sử dụng **Root Account** cho security best practices

## 2. Môi trường Làm việc

### Browser Requirements:
- **Modern browser**: Chrome 90+, Firefox 88+, Safari 14+, Edge 90+
- **JavaScript enabled**
- **Cookies enabled** cho **AWS Console**
- **Pop-up blocker disabled** cho AWS domains

### Network Requirements:
- **Stable internet connection** (minimum 1 Mbps)
- **Access to AWS endpoints** (không bị firewall block)
- **HTTPS support** (TLS 1.2+)

### Recommended Tools:
- **Text editor** với syntax highlighting (VS Code, Sublime Text...)
- **JSON formatter** extension hoặc online tool
- **AWS CLI** (optional, cho advanced users)

## 3. Kiến thức Cơ bản

### **AWS Fundamentals:**
Bạn nên hiểu các concepts sau:

#### **AWS Regions và Availability Zones:**
- **Region**: Geographical area với multiple data centers
- **AZ**: Isolated data center trong một region
- **Workshop region**: **ap-southeast-1 (Singapore)**

#### **AWS Services Overview:**
- **Compute**: EC2, Lambda, Fargate
- **Storage**: S3, EBS, EFS
- **Database**: RDS, DynamoDB, ElastiCache
- **Networking**: VPC, CloudFront, Route 53
- **Security**: IAM, KMS, Secrets Manager

### **JSON và REST APIs:**
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

### **Python Basics (cho Lambda):**
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

## 4. Cấu hình AWS Console

### Thiết lập Region:
1. Đăng nhập **AWS Console**
2. Chọn region **Asia Pacific (Singapore) - ap-southeast-1**
3. **QUAN TRỌNG**: Tất cả resources phải tạo trong cùng region

### Console Navigation:
- **Services menu**: Tìm services nhanh
- **Recently visited**: Access services đã dùng
- **Favorites**: Pin frequently used services
- **Resource Groups**: Organize related resources

### Billing Setup:
1. Vào **Billing Dashboard**
2. Enable **Free Tier Usage Alerts**
3. Set up **Budget Alerts** (recommended: $5 threshold)
4. Review **Cost Explorer** để track spending

## 5. Email Configuration

### SNS Email Setup:
- **Valid email address** để nhận notifications
- **Access to email** để confirm subscriptions
- **Check spam folder** nếu không nhận được emails
- **Whitelist AWS domains**: 
  - `@sns.amazonaws.com`
  - `@aws.amazon.com`

### Email Testing:
Trước khi bắt đầu workshop, test email delivery:
1. Tạo test **SNS Topic**
2. Subscribe email của bạn
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

Trước khi bắt đầu workshop, hãy kiểm tra:

### ✅ **Account Setup:**
- [ ] **AWS Account** đã active và verified
- [ ] **Credit card** đã được add (cho verification)
- [ ] **IAM permissions** đã được cấu hình
- [ ] **Billing alerts** đã được setup

### ✅ **Environment:**
- [ ] **Browser** updated và compatible
- [ ] **Internet connection** stable
- [ ] **AWS Console** accessible
- [ ] **Region** set to **ap-southeast-1**

### ✅ **Knowledge:**
- [ ] Đã đọc phần **Introduction**
- [ ] Hiểu basic **AWS concepts**
- [ ] Familiar với **JSON format**
- [ ] **Email** ready để receive notifications

### ✅ **Tools:**
- [ ] **Text editor** available
- [ ] **AWS Console** bookmarked
- [ ] **Workshop materials** downloaded/accessible

## 8. Tài liệu Tham khảo

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
Nếu gặp vấn đề trong quá trình chuẩn bị, hãy tham khảo **AWS Support** hoặc **AWS Community Forums** để được hỗ trợ.
{{% /notice %}}
---
title : "Resource Cleanup"
date: 2025-06-18
weight : 6
chapter : false
pre : " <b> 6. </b> "
---

After completing the workshop, you need to clean up **AWS** resources to avoid unexpected charges.

## 1. Delete S3 Buckets
- Go to **AWS Console** → **S3**
- Select the buckets you created:
  - `yourname-serverless-files-2025`
  - `yourname-serverless-website-2025`
- For each bucket:
  - **Empty bucket** → **Confirm**
  - **Delete bucket** → **Confirm**

{{% notice warning %}}
**S3 Buckets** must be empty before they can be deleted.
{{% /notice %}}

## 2. Delete Lambda Functions
- **Console** → **Lambda**
- Select the functions you created:
  - `s3FileUploaderNotifier`
  - `FileProcessor` (if exists)
  - `UploadHandler` (if exists)
- **Actions** → **Delete function**
- **Confirm** deletion

## 3. Delete SNS Topic and Subscriptions
- **Console** → **SNS** → **Topics**
- Select topic `FileUploadNotifications`
- **Delete** → **Confirm**
- Go to **Subscriptions**, delete email subscription if remaining

## 4. Delete DynamoDB Table (Option 2)
- **Console** → **DynamoDB** → **Tables**
- Select table `FileMetadata`
- **Actions** → **Delete table**
- **Confirm deletion**

## 5. Delete SQS Queue (Option 2)
- **Console** → **SQS** → **Queues**
- Select queue `FileProcessingQueue`
- **Delete** → **Confirm**

## 6. Delete API Gateway (Option 2)
- **Console** → **API Gateway** → **APIs**
- Select **API** `FileUploadAPI`
- **Actions** → **Delete API**
- **Confirm deletion**

## 7. Delete CloudWatch Resources
- **Console** → **CloudWatch**
- **Dashboards**: Delete `ServerlessDashboard` (if exists)
- **Log groups**: Delete **Lambda function** log groups
  - `/aws/lambda/s3FileUploaderNotifier`
  - `/aws/lambda/FileProcessor`

## 8. Delete IAM Roles (Optional)
- **Console** → **IAM** → **Roles**
- Find auto-created roles:
  - `s3FileUploaderNotifier-role-xxxxxxxx`
  - Other **Lambda**-related roles
- **Delete** role if not used for other purposes

{{% notice tip %}}
Auto-created **IAM roles** by **Lambda** can be kept if you plan to reuse them.
{{% /notice %}}

## 9. Check Billing
- Go to **Billing Dashboard** → **Cost Explorer**
- **Filter** by services: **S3**, **Lambda**, **SNS**, **DynamoDB**, **SQS**, **API Gateway**
- Confirm no resources are generating charges
- Check **Free Tier Usage** to ensure within limits

## 10. Final Verification
✅ **Cleanup Checklist:**
- [ ] **S3 Buckets** deleted
- [ ] **Lambda Functions** deleted
- [ ] **SNS Topic** and **Subscriptions** deleted
- [ ] **DynamoDB Table** deleted 
- [ ] **SQS Queue** deleted 
- [ ] **API Gateway** deleted 
- [ ] **CloudWatch Logs** deleted
- [ ] **IAM Roles** deleted (if needed)
- [ ] **Billing Dashboard** shows no charges

{{% notice info %}}
Some resources may take a few minutes to completely disappear from the console after deletion.
{{% /notice %}}
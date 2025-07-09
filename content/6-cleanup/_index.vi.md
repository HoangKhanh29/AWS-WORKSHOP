---
title : "Dọn dẹp tài nguyên"
date: 2025-06-18
weight : 6
chapter : false
pre : " <b> 6. </b> "
---

Sau khi hoàn thành workshop, bạn cần dọn dẹp các tài nguyên **AWS** để tránh phát sinh chi phí không mong muốn.

## 1. Xóa S3 Buckets
- Vào **AWS Console** → **S3**
- Chọn các buckets đã tạo:
  - `yourname-serverless-files-2025`
  - `yourname-serverless-website-2025`
- Với mỗi bucket:
  - **Empty bucket** → **Confirm**
  - **Delete bucket** → **Confirm**

{{% notice warning %}}
**S3 Bucket** phải rỗng trước khi có thể xóa được.
{{% /notice %}}

## 2. Xóa Lambda Functions
- **Console** → **Lambda**
- Chọn các functions đã tạo:
  - `s3FileUploaderNotifier`
  - `FileProcessor` (nếu có)
  - `UploadHandler` (nếu có)
- **Actions** → **Delete function**
- **Confirm** xóa

## 3. Xóa SNS Topic và Subscriptions
- **Console** → **SNS** → **Topics**
- Chọn topic `FileUploadNotifications`
- **Delete** → **Confirm**
- Vào **Subscriptions**, xóa email subscription nếu còn

## 4. Xóa DynamoDB Table (Option 2)
- **Console** → **DynamoDB** → **Tables**
- Chọn table `FileMetadata`
- **Actions** → **Delete table**
- **Confirm deletion**

## 5. Xóa SQS Queue (Option 2)
- **Console** → **SQS** → **Queues**
- Chọn queue `FileProcessingQueue`
- **Delete** → **Confirm**

## 6. Xóa API Gateway (Option 2)
- **Console** → **API Gateway** → **APIs**
- Chọn **API** `FileUploadAPI`
- **Actions** → **Delete API**
- **Confirm deletion**

## 7. Xóa CloudWatch Resources
- **Console** → **CloudWatch**
- **Dashboards**: Xóa `ServerlessDashboard` (nếu có)
- **Log groups**: Xóa log groups của **Lambda functions**
  - `/aws/lambda/s3FileUploaderNotifier`
  - `/aws/lambda/FileProcessor`

## 8. Xóa IAM Roles (Tùy chọn)
- **Console** → **IAM** → **Roles**
- Tìm các roles được tạo tự động:
  - `s3FileUploaderNotifier-role-xxxxxxxx`
  - Các roles khác liên quan đến **Lambda**
- **Delete** role nếu không sử dụng cho mục đích khác

{{% notice tip %}}
**IAM roles** được tạo tự động bởi **Lambda** có thể được giữ lại nếu bạn có kế hoạch tái sử dụng.
{{% /notice %}}

## 9. Kiểm tra Billing
- Vào **Billing Dashboard** → **Cost Explorer**
- **Filter** theo các services: **S3**, **Lambda**, **SNS**, **DynamoDB**, **SQS**, **API Gateway**
- Xác nhận không còn tài nguyên nào đang phát sinh chi phí
- Kiểm tra **Free Tier Usage** để đảm bảo trong giới hạn

## 10. Xác nhận hoàn tất
✅ **Checklist dọn dẹp:**
- [ ] **S3 Buckets** đã xóa
- [ ] **Lambda Functions** đã xóa  
- [ ] **SNS Topic** và **Subscriptions** đã xóa
- [ ] **DynamoDB Table** đã xóa 
- [ ] **SQS Queue** đã xóa 
- [ ] **API Gateway** đã xóa 
- [ ] **CloudWatch Logs** đã xóa
- [ ] **IAM Roles** đã xóa (nếu cần)
- [ ] **Billing Dashboard** không còn charges

{{% notice info %}}
Một số tài nguyên có thể mất vài phút để hoàn toàn biến mất khỏi console sau khi xóa.
{{% /notice %}}
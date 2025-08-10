---
title : "Chuẩn bị"
date: 2025-06-18
weight : 2
chapter : false
pre : " <b> 2. </b> "
---

## Chuẩn bị

{{% notice info %}}
Bạn cần chuẩn bị các tài nguyên AWS ban đầu, bao gồm việc tạo một IAM Role với các quyền cần thiết cho Kinesis và Lambda Functions.
{{% /notice %}}

Để cho phép Lambda Functions quản lý và xử lý dữ liệu từ Kinesis cũng như lưu trữ dữ liệu vào S3, chúng ta cần thiết lập một IAM Role cấp quyền cho các dịch vụ này. Trong bước chuẩn bị này, trước tiên chúng ta sẽ tạo một IAM Role để đảm bảo Lambda có đầy đủ quyền làm việc với Kinesis và S3. Sau đó, chúng ta sẽ tiến hành cấu hình các dịch vụ như Kinesis.

### Nội dung
 1. [Tạo IAM Role](2.1-create-iam-role/)
 2. [Tạo Lambda Functions](2.2-lambda-functions/)

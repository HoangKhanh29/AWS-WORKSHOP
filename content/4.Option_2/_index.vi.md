---
title : "OPTION 2: Hệ thống Nâng cao"
date: 2025-06-18
weight : 4
chapter : false
pre : " <b> 4. </b> "
---

Trong **Option 2**, chúng ta mở rộng hệ thống cơ bản với các dịch vụ **AWS** bổ sung để tạo ra một nền tảng quản lý file serverless toàn diện với database, queuing, API endpoints và monitoring.

**Kiến trúc mở rộng:**
- **DynamoDB**: Lưu trữ metadata file và trạng thái xử lý
- **SQS Queue**: Tách biệt xử lý và xử lý khối lượng lớn
- **API Gateway**: REST API cho tích hợp bên ngoài
- **CloudWatch Dashboard**: Giám sát và metrics thời gian thực
- **Web Interface**: Giao diện upload file thân thiện

**Lợi ích bổ sung:**
- **Khả năng mở rộng**: Xử lý hàng nghìn upload đồng thời
- **Độ tin cậy**: Message queuing ngăn mất dữ liệu
- **Giám sát**: Thông tin chi tiết và cảnh báo thời gian thực
- **Tích hợp**: REST API cho hệ thống bên thứ ba
- **Trải nghiệm người dùng**: Giao diện web chuyên nghiệp

![serverless-upload-notification](/images/serverless_architecture_diagram.png)

### Nội dung
4.1. [Tạo DynamoDB Table](4.1-DynamoDB-Table/) \
4.2. [Tạo SQS Queue](4.2-SQS-Queue/) \
4.3. [Enhanced Lambda Function](4.3-Enhanced-Lambda-Function-with-DynamoDB/) \
4.4. [Tạo API Gateway](4.4-API-Gateway/) \
4.5. [Xây dựng Web Interface](4.5-Web-Interface/) \
4.6. [Thiết lập CloudWatch Dashboard](4.6-CloudWatch-Dashboard/)
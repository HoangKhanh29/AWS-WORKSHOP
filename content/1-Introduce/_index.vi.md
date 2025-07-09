---
title : "Giới thiệu"
date: 2025-06-18
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---

## Tổng quan Workshop

Workshop này hướng dẫn xây dựng **Hệ thống Thông báo File Serverless** sử dụng kiến trúc event-driven trên **AWS**. Hệ thống sẽ tự động gửi email thông báo mỗi khi có file mới được upload lên **S3**, không cần quản lý server.

## Kiến trúc Serverless là gì?

**Serverless Computing** là mô hình điện toán đám mây nơi nhà cung cấp dịch vụ (AWS) quản lý hoàn toàn infrastructure, cho phép developers tập trung vào code thay vì quản lý servers.

### Đặc điểm chính:
- **No Server Management**: Không cần cấu hình, patch, hoặc maintain servers
- **Auto Scaling**: Tự động scale từ 0 đến hàng nghìn requests
- **Pay-per-Use**: Chỉ trả tiền khi code thực sự chạy
- **High Availability**: Built-in fault tolerance và disaster recovery
- **Event-Driven**: Phản hồi tự động với các events từ hệ thống

## Event-Driven Architecture

**Event-Driven Architecture (EDA)** là pattern thiết kế nơi các components giao tiếp thông qua events thay vì direct calls.

### Lợi ích của EDA:
- **Loose Coupling**: Components độc lập, dễ maintain và scale
- **Asynchronous Processing**: Xử lý không đồng bộ, tăng performance
- **Resilience**: Một component fail không ảnh hưởng toàn hệ thống
- **Scalability**: Dễ dàng thêm/bớt components theo nhu cầu

## Kiến trúc Hệ thống

### Core Components:

#### 1. **Amazon S3 (Simple Storage Service)**
- **Vai trò**: Event source và file storage
- **Chức năng**: 
  - Lưu trữ files với 99.999999999% (11 9's) durability
  - Tự động trigger events khi có file upload
  - Hỗ trợ versioning và lifecycle management
- **Event Types**: ObjectCreated, ObjectRemoved, ObjectRestore...

#### 2. **AWS Lambda**
- **Vai trò**: Event processor và business logic
- **Chức năng**:
  - Serverless compute service
  - Tự động scale từ 0 đến 1000+ concurrent executions
  - Hỗ trợ nhiều runtime: Python, Node.js, Java, Go...
  - Pay-per-request pricing model
- **Triggers**: S3 events, API Gateway, SNS, SQS, CloudWatch...

#### 3. **Amazon SNS (Simple Notification Service)**
- **Vai trò**: Message delivery service
- **Chức năng**:
  - Pub/Sub messaging pattern
  - Hỗ trợ multiple protocols: Email, SMS, HTTP, SQS...
  - Message filtering và fanout capabilities
  - Dead Letter Queue cho error handling

### Advanced Components (Option 2):

#### 4. **Amazon DynamoDB**
- **Vai trò**: NoSQL database cho metadata
- **Đặc điểm**:
  - Fully managed NoSQL database
  - Single-digit millisecond latency
  - Auto-scaling read/write capacity
  - Global Tables cho multi-region replication

#### 5. **Amazon SQS (Simple Queue Service)**
- **Vai trò**: Message queuing service
- **Lợi ích**:
  - Decouple components
  - Handle traffic spikes
  - Ensure message delivery
  - Dead Letter Queue support

#### 6. **Amazon API Gateway**
- **Vai trò**: REST API endpoint
- **Tính năng**:
  - Request/response transformation
  - Authentication & authorization
  - Rate limiting & throttling
  - API versioning & deployment stages

#### 7. **Amazon CloudWatch**
- **Vai trò**: Monitoring và logging
- **Capabilities**:
  - Metrics collection & visualization
  - Log aggregation & analysis
  - Alarms & notifications
  - Custom dashboards

## Luồng Xử lý (Data Flow)

### Option 1 - Basic Flow:
```
User Upload → S3 Bucket → S3 Event → Lambda Function → SNS Topic → Email Notification
```

### Option 2 - Advanced Flow:
```
User Upload → S3 Bucket → S3 Event → Lambda Function → DynamoDB (metadata)
                                                   → SQS Queue → Processing Lambda
                                                   → SNS Topic → Email Notification
API Gateway ← Web Interface ← CloudWatch Dashboard ← Monitoring
```

## Ưu điểm của Hệ thống

### 1. **Cost Efficiency**
- **No idle costs**: Chỉ trả tiền khi có traffic
- **Free tier**: AWS cung cấp free tier generous cho các services
- **Automatic optimization**: AWS tự động optimize infrastructure

### 2. **Scalability**
- **Horizontal scaling**: Tự động scale theo demand
- **No capacity planning**: Không cần dự đoán traffic
- **Global reach**: Deploy across multiple regions dễ dàng

### 3. **Reliability**
- **High availability**: 99.99% uptime SLA
- **Fault tolerance**: Built-in redundancy
- **Disaster recovery**: Multi-AZ deployment

### 4. **Developer Productivity**
- **Focus on business logic**: Không cần quản lý infrastructure
- **Rapid development**: Quick deployment và iteration
- **Rich ecosystem**: Nhiều managed services tích hợp

## Use Cases Thực tế

### 1. **Content Management Systems**
- Tự động resize images khi upload
- Generate thumbnails và previews
- Virus scanning cho uploaded files

### 2. **Data Processing Pipelines**
- ETL workflows cho big data
- Real-time analytics
- Machine learning inference

### 3. **IoT Applications**
- Sensor data processing
- Real-time alerting
- Device management

### 4. **E-commerce Platforms**
- Order processing workflows
- Inventory management
- Customer notifications

## Hai Phương án Triển khai

### **Option 1: Hệ thống Cơ bản**
- **Mục tiêu**: Học các concepts cơ bản
- **Components**: S3 + Lambda + SNS
- **Thời gian**: 30-45 phút
- **Phù hợp**: Beginners, POC projects

### **Option 2: Hệ thống Nâng cao**
- **Mục tiêu**: Production-ready system
- **Components**: Full serverless stack
- **Thời gian**: 2-3 giờ
- **Phù hợp**: Advanced users, enterprise solutions

## Kiến thức Tiên quyết

### **Cơ bản**:
- Hiểu biết về cloud computing concepts
- Kinh nghiệm với AWS Console
- Kiến thức cơ bản về JSON và REST APIs

### **Nâng cao**:
- Programming experience (Python preferred)
- Understanding của distributed systems
- Database design principles

## Chuẩn bị Workshop

Trước khi bắt đầu, hãy đảm bảo bạn có:
- **AWS Account** với appropriate permissions
- **Email address** để nhận notifications
- **Stable internet connection**
- **Modern web browser**

{{% notice info %}}
Workshop này được thiết kế để chạy trong **AWS Free Tier**. Tổng chi phí ước tính < $1 USD nếu thực hiện đúng hướng dẫn.
{{% /notice %}}
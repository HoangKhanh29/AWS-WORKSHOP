---
title : "Tạo Lambda Function"
date: 2025-06-18
weight : 3
chapter : false
pre : " <b> 3.3. </b> "
---

1. Tìm kiếm Lambda và chọn AWS Lambda.
- Trong thanh tìm kiếm, gõ Lambda.
- Chọn Lambda từ danh sách kết quả.
- Xác nhận Region: Đảm bảo bạn vẫn đang ở ap-southeast-1.
![Picture21](/images/3.3/image21.png)
2. Nhấn Create function:
![Picture22](/images/3.3/image22.png)
- Author from scratch: Chọn mục này.
- Function name: Đặt tên cho hàm của bạn (ví dụ: `s3FileUploaderNotifier`).
- Runtime: Chọn Python 3.9 (hoặc phiên bản Python mới nhất có sẵn).
- Architecture: Để mặc định x86_64
![Picture23](/images/3.3/image23.png)
- Execution role: Chọn Create a new role with basic Lambda permissions. (AWS sẽ tự động tạo một IAM Role cơ bản cho Lambda có quyền ghi log vào CloudWatch).
3. Nhấn **Create function**.
![Picture24](/images/3.3/image24.png)
![Picture25](/images/3.3/image25.png)
4. Cấp quyền SNS cho IAM Role của Lambda (RẤT QUAN TRỌNG!):
- Sau khi Function được tạo, bạn sẽ được đưa đến trang chi tiết của Function.
- Vào tab Configuration (ở phía trên, gần tên Function).
- Ở menu bên trái, chọn Permissions.
- Dưới phần "Execution role", bạn sẽ thấy Role name (ví dụ: s3FileUploaderNotifier-role-xxxxxxxx). Nhấp vào TÊN ROLE NÀY.
![Picture26](/images/3.3/image26.png)
- Một tab mới sẽ mở ra, đưa bạn đến trang IAM (Identity and Access Management). Đây là nơi quản lý quyền hạn.
- Trong trang IAM Role, nhấn nút Add permissions -> Attach policies.
![Picture27](/images/3.3/image27.png)
- Trong ô tìm kiếm, gõ SNS và chọn chính sách AmazonSNSFullAccess (Hoặc AmazonSNSPublishAccess nếu có và bạn muốn giới hạn quyền hơn). 

{{% notice info %}}
Chính sách này cấp cho Lambda quyền để gửi tin nhắn đến SNS Topic. Không có quyền này, Lambda sẽ báo lỗi.
{{% /notice %}}

- Nhấn nút Add permissions (ở góc dưới bên phải).
![Picture28](/images/3.3/image28.png)
![Picture29](/images/3.3/image29.png)
5.	Dán Code Lambda Function: 
- Quay lại tab trình duyệt của Lambda Function.
- Cuộn xuống phần Code source.
- Bạn sẽ thấy một đoạn code Python mẫu. Xóa toàn bộ code mẫu này.
![Picture30](/images/3.3/image30.png)
- Dán đoạn code Python sau đây vào:
```python
import json
import os
import boto3

# Khởi tạo SNS client
sns_client = boto3.client('sns')
SNS_TOPIC_ARN = os.environ.get('SNS_TOPIC_ARN')

def lambda_handler(event, context):
    print("Received S3 event:", json.dumps(event))
    
    for record in event['Records']:
        bucket_name = record['s3']['bucket']['name']
        file_key = record['s3']['object']['key']
        event_name = record['eventName']
        event_time = record['eventTime']
        
        # Tạo nội dung thông báo
        message = f"""🔔 Thông báo: File mới được upload!
        
📁 Bucket: {bucket_name}
📄 File: {file_key}
🎯 Event: {event_name}
⏰ Time: {event_time}

🔗 Link: https://s3.console.aws.amazon.com/s3/v2/buckets/{bucket_name}/objects/?prefix={file_key}&region={os.environ.get('AWS_REGION')}"""
        
        subject = f"🚀 File Upload Alert: {file_key}"
        
        try:
            response = sns_client.publish(
                TopicArn=SNS_TOPIC_ARN,
                Message=message,
                Subject=subject
            )
            print("SNS Response:", response)
        except Exception as e:
            print(f"Error: {e}")
    
    return {
        'statusCode': 200,
        'body': json.dumps('Successfully processed S3 event')
    }
```
- Nhấn nút màu cam Deploy (ở phía trên của phần "Code source") để lưu và triển khai code lên Lambda.
![Picture31](/images/3.3/image31.png)
6. Cấu hình biến môi trường:
- Vẫn trong tab Configuration của hàm Lambda.
- Ở menu bên trái, chọn Environment variables.
- Nhấn nút Edit.
![Picture32](/images/3.3/image32.png)
- Nhấn Add environment variable.
- Key: Nhập SNS_TOPIC_ARN
- Value: Dán ARN của SNS Topic bạn đã copy ở 3.2. (Ví dụ: arn:aws:sns:ap-southeast-1:123456789012:FileUploadedNotifications).
- Nhấn nút Save.
![Picture33](/images/3.3/image33.png)
![Picture34](/images/3.3/image34.png)
7. Cấu hình Trigger cho Lambda (Kết nối S3 với Lambda)
- Trong trang Lambda Function của bạn (s3FileUploaderNotifier): 
    - Trong phần "Function overview" (sơ đồ đồ họa ở trên cùng), nhấn nút Add trigger.
    ![Picture35](/images/3.3/image35.png)
- Cấu hình Trigger: 
    - Select a source: Chọn S3 từ danh sách dịch vụ.
    - Bucket: Chọn S3 Bucket bạn đã tạo ở Bước 2 (ví dụ: yourname-hutech-serverless-files-2025).
    - Event types: Chọn All object create events (điều này có nghĩa là mọi sự kiện tạo mới hoặc ghi đè một tệp trong bucket sẽ kích hoạt Lambda).
    ![Picture36](/images/3.3/image36.png)
    - Recursive invocation: Đánh dấu chọn (checkbox) I acknowledge that enabling this trigger may result in recursive invocations... (Đây là cảnh báo của AWS, trong trường hợp này là an toàn vì code của chúng ta không gây ra vòng lặp vô hạn).
    - Enable trigger: Đánh dấu chọn (checkbox này thường đã được chọn sẵn).
- Thêm Trigger: 
    - Nhấn nút màu cam Add.
    ![Picture37](/images/3.3/image37.png)
- Kiểm tra: Sau khi thêm, bạn sẽ thấy S3 Bucket của bạn xuất hiện trong phần "Triggers" của hàm Lambda.
![Picture38](/images/3.3/image38.png)
![Picture39](/images/3.3/image39.png)


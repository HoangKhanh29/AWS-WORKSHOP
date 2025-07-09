---
title : "Tạo SNS Topic"
date: 2025-06-18
weight : 2
chapter : false
pre : " <b> 3.2. </b> "
---

1. Tìm kiếm **SNS** và chọn **Amazon SNS (Simple Notification Service)**.
![Picture8](/images/3.2/image8.png)

2. Nhấn **Create topic**:
![Picture9](/images/3.2/image9.png)
- **Type**: Standard.
- **Name**: `FileUploadNotifications`.
![Picture10](/images/3.2/image10.png)

3. Nhấn **Create topic** và **Copy ARN** để dùng sau (ví dụ: `arn:aws:sns:ap-southeast-1:123456789012:FileUploadNotifications`)
![Picture12](/images/3.2/image12.png)

4. Tạo subscription:
- Nhấn **Create subscription**.
![Picture13](/images/3.2/image13.png)
- **Protocol**: Email.
- **Endpoint**: Nhập email của bạn.
- Nhấn **Create subscription**.
![Picture16](/images/3.2/image16.png)
![Picture14](/images/3.2/image14.png)

5. Kiểm tra email và nhấn **Confirm subscription**. (nếu không thấy mail thì kiểm tra thư rác!)
![Picture18](/images/3.2/image18.png)
![Picture20](/images/3.2/image20.png)
---
title : "Tạo Lambda Functions"
date: 2025-06-18
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

## Tạo Lambda Functions
Trong bước này, sau khi tạo Role, chúng ta sẽ tạo Lambda **producer** và chọn **data-role** để làm execution role.  
Hàm này sẽ lắng nghe sự kiện từ S3, đọc dữ liệu từ các object được tải lên S3 và gửi dữ liệu này đến Kinesis stream.  

Đối với Lambda function dành cho consumers: bạn sẽ tạo thêm hai Lambda function cho hai consumer — **customer #1** và **customer #2** — để xử lý dữ liệu từ Kinesis stream.

1. Truy cập [Lambda](https://ap-southeast-1.console.aws.amazon.com/lambda/home?region=ap-southeast-1#/create/function?firstrun=true)  
    - Tìm kiếm **Lambda**.  
    - Nhấp **Lambda**, sau đó nhấp **Create a function** để xác nhận.  

![ConnectPrivate](/images/2.prerequisite/B-1.png)  
![ConnectPrivate](/images/2.prerequisite/B-2.png)  

2. Truy cập [Create function](https://ap-southeast-1.console.aws.amazon.com/lambda/home?region=ap-southeast-1#/create/function?firstrun=true&intent=authorFromScratch)  
    - Tạo: **producer**, **customer#1**, **customer#2** / Name: **producer**, **customer#1**, **customer#2**.  
    - Chọn **Node.js 20.x**  
    - Chọn **Use an existing role**  
    - Chọn **data-streaming-system-role**  

![ConnectPrivate](/images/2.prerequisite/B-3.png)  
![ConnectPrivate](/images/2.prerequisite/B-4.png)  
![ConnectPrivate](/images/2.prerequisite/B-5.png)  
![ConnectPrivate](/images/2.prerequisite/B-6.png)  

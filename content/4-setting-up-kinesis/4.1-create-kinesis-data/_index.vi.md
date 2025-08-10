---
title : "Tạo Kinesis Data"
date: 2025-06-18
weight : 1
chapter : false
pre : " <b> 4.1 </b> "
---

## Tạo Kinesis Data

1. Truy cập [Tạo Kinesis](https://ap-southeast-1.console.aws.amazon.com/kinesis/home?region=ap-southeast-1#/streams/create)  
    - Tìm kiếm **Kinesis**.  
    - Nhấp **Create data stream**.  
    ![ConnectPrivate](/images/4.kinesis/C-8.png)  
    ![ConnectPrivate](/images/4.kinesis/C-9.png)  

2. Vào **Data stream configuration**  
    - Tên: **jinmeister-data-stream**.  
    - Chọn **Provisioned**.  
    - Số lượng provisioned shards: **2**.  
    ![ConnectPrivate](/images/4.kinesis/C-10.1.png)  

3. Vào **jinmeister-data-stream**  
    - Hoàn tất **Create Kinesis**.  
    - Nhấp **Configuration**.  
    - Nhấp **Encryption** và chọn **Edit**.  
    ![ConnectPrivate](/images/4.kinesis/C-10.2.png)  
    ![ConnectPrivate](/images/4.kinesis/D-2.png)  
    - Chọn **Enable server-side encryption**.  
    - Nhấp **Save Changes**.  
    ![ConnectPrivate](/images/4.kinesis/D-2.2.png)  
    ![ConnectPrivate](/images/4.kinesis/D-3.3.png)  

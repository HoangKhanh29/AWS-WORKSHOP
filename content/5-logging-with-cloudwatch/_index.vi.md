---
title : "Ghi log với CloudWatch"
date: 2025-06-18
weight : 5
chapter : false
pre : " <b> 5. </b> "
---

1. Tạo file mới **Test.txt**.  
![ConnectPrivate](/images/5.log-cloudwatch/file-test.png)

2. Vào **Amazon S3**  
    - Click **Objects**.  
    - Click **Upload**.  
    ![ConnectPrivate](/images/5.log-cloudwatch/E-1.png)  
    - Click **Add files** sau đó chọn file **test.file** vừa tạo.  
    ![ConnectPrivate](/images/5.log-cloudwatch/E-3.png)  
    ![ConnectPrivate](/images/5.log-cloudwatch/E-4.png)  
    ![ConnectPrivate](/images/5.log-cloudwatch/E-2.png)  

3. Quay lại Lambda **Producer**  
    - Click **Log streams**.  
    - Chọn một log stream theo thời gian trùng với thời điểm bạn upload file để kiểm tra.  
    ![ConnectPrivate](/images/5.log-cloudwatch/E-5.png)  
    ![ConnectPrivate](/images/5.log-cloudwatch/E-6.png)  
    - Quay lại Lambda **Consumer#1** và **Consumer#2**  
    - Chọn một log stream theo thời gian trùng với thời điểm bạn upload file để kiểm tra.  
    ![ConnectPrivate](/images/5.log-cloudwatch/E-7.png)  
    ![ConnectPrivate](/images/5.log-cloudwatch/E-8.png)  
    - Một file mới đã được thêm thành công vào S3 bucket.  
    ![ConnectPrivate](/images/5.log-cloudwatch/E-9.png)  

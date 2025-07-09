---
title : "Tạo S3 Bucket"
date: 2025-06-18
weight : 1 
chapter : false
pre : " <b> 3.1. </b> "
---

1. Tìm kiếm **S3** trong **AWS Console** và chọn dịch vụ **S3**.
![Picture1](/images/3.1/image1.png)

2. Trên trang **S3**, nhấn **Create bucket**:
![Picture2](/images/3.1/image2.png)
- **AWS Region**: Xác nhận lại là **Asia Pacific (Singapore) ap-southeast-1**. (Nếu sai, hãy đổi lại ngay).
- **Bucket name**: `yourname-serverless-workshop-2025` (thay yourname bằng tên của bạn).
    - Đây là tên duy nhất trên toàn cầu cho **Bucket** của bạn.
    - **QUAN TRỌNG**: Tên bucket phải viết thường, không có khoảng trắng, chỉ có thể chứa chữ cái thường, số và dấu gạch ngang (-).
- **Object Ownership**: Chọn **ACLs enabled** và **Bucket owner preferred**.
![Picture3](/images/3.1/image3.png)
![Picture4](/images/3.1/image4.png)

- **Block Public Access settings** for this bucket: 
    - Để mặc định (TẤT CẢ các tùy chọn đều được **ĐÁNH DẤU CHỌN**). Chúng ta không muốn bucket này có thể truy cập công khai từ Internet vì nó chỉ dùng để kích hoạt **Lambda**.
- Các tùy chọn còn lại (**Versioning**, **Tags**, **Default encryption**, **Advanced settings**): Để mặc định.
![Picture5](/images/3.1/image5.png)
- **Versioning**: Disabled

3. Nhấn **Create bucket**.
![Picture6](/images/3.1/image6.png)
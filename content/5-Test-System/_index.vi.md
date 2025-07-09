---
title : "Test Hệ thống "
date: 2025-06-18
weight : 5
chapter : false
pre : " <b> 5. </b> "
---
- Upload file
![Picture100](/images/5/image100.png)
- Kiểm tra SQS queue có message
![Picture103](/images/5/image103.png)
![Picture104](/images/5/image104.png)
![Picture105](/images/5/image105.png)
![Picture106](/images/5/image106.png)
- Kiểm tra email notification
![Picture107](/images/5/image107.png)
- Vào CloudWatch → Dashboards
- Xem metrics realtime
![Picture108](/images/5/image108.png)
![Picture109](/images/5/image109.png)
- Kiểm tra logs của Lambda functions
    - Monitor → view CloundWatch logs
    - Click vào Log stream để xem đến Log even
![Picture45](/images/5/image45.png)
![Picture46](/images/5/image46.png)
- Vào DynamoDB → Tables → FileMetadata
- Scan table để xem all records
- Query by fileId để test performance
![Picture101](/images/5/image101.png)

{{% notice tip %}}
Khi bạn nhấn Run, DynamoDB sẽ trả về các mục (items) đang có trong bảng, ví dụ như thông tin metadata của file: tên file, kích thước, thời gian upload, trạng thái…
{{% /notice %}}

-  Kết quả phía dưới sẽ hiển thị:
- Số lượng item tìm thấy (ví dụ: 3 items)
- Hiệu suất truy xuất (RCU – Read Capacity Units tiêu tốn)
- Các giá trị tương ứng từ bảng
![Picture102](/images/5/image102.png)
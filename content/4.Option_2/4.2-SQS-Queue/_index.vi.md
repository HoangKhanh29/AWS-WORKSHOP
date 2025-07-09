---
title : "SQS Queue (Message queuing)"
date: 2025-06-18
weight : 1
chapter : false
pre : " <b> 4.2. </b> "
---
1. Tìm kiếm "SQS" → Create queue
![Picture52](/images/4.2/image52.png)
![Picture53](/images/4.2/image53.png)
2. Cấu hình:
- Type: Standard queue
- Name: ``FileProcessingQueue``
- Visibility timeout: 30 seconds
- Trong Access policy, choose method → Basic → Only the queue owner
- Create queue
![Picture54](/images/4.2/image54.png)
![Picture55](/images/4.2/image55.png)
![Picture56](/images/4.2/image56.png)
![Picture57](/images/4.2/image57.png)
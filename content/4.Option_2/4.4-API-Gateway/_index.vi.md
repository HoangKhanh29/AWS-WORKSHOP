---
title : "API Gateway"
date: 2025-06-18
weight : 4
chapter : false
pre : " <b> 4.4. </b> "
---
1. Tạo API Gateway:
- Tìm kiếm "API Gateway" → Create API
![Picture67](/images/4.4/image67.png)
![Picture68](/images/4.4/image68.png)
- Lướt xuống dưới chọn REST API → Build
![Picture69](/images/4.4/image69.png)
- New API → Name: ``FileUploadAPI``
![Picture70](/images/4.4/image70.png)
2. Tạo Resource & Method:
- Actions → Create Resource
![Picture71](/images/4.4/image71.png)
- Resource Name: upload
![Picture72](/images/4.4/image72.png)
- Actions → Create Method 
![Picture73](/images/4.4/image73.png)
- Method type: POST
- Integration type: Lambda Function
- Lambda Function: Chọn function đã tạo
![Picture74](/images/4.4/image74.png)
![Picture75](/images/4.4/image75.png)
3. Deploy API:
- Actions → Deploy API
![Picture76](/images/4.4/image76.png)
- Stage: prod
- Copy Invoke URL
![Picture77](/images/4.4/image77.png)
![Picture78](/images/4.4/image78.png)
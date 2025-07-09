---
title : "DynamoDB Table (Lưu metadata files)"
date: 2025-06-18
weight : 1
chapter : false
pre : " <b> 4.1. </b> "
---
1. Tìm kiếm "DynamoDB" → Create table
![Picture47](/images/4.1/image47.png)
![Picture48](/images/4.1/image48.png)
2. Cấu hình:
- Table name: ``FileMetadata``
- Partition key: fileId (String)
- Sort key: timestamp (Number)
- Billing mode: On-demand
- Create table
![Picture49](/images/4.1/image49.png)
![Picture50](/images/4.1/image50.png)
![Picture51](/images/4.1/image51.png)
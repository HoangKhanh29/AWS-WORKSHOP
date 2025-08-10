---
title : "Hệ thống Kinesis"
date: 2025-06-18
weight : 4
chapter : false
pre : " <b> 4. </b> "
---

Kinesis Stream: Bạn tạo một data stream có tên **jinmeister-datasource-stream** để xử lý dữ liệu từ Lambda.  
Kinesis được cấu hình để tự động mở rộng dựa trên số lượng shard, cân bằng giữa khả năng đọc và ghi.  
Tính năng mã hóa phía máy chủ (server-side encryption) được bật để tăng cường bảo mật, đảm bảo dữ liệu trong stream được mã hóa.

### Nội dung
4.1. [Tạo Kinesis](4.1-create-kinesis-data/) \
4.2. [Cập nhật Lambda](4.2-update-lambda/) \

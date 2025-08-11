---
title : "Giới thiệu"
date: 2025-06-18
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---
## Giới thiệu

**Xây dựng Hệ thống Streaming Dữ liệu Thời gian Thực với AWS Kinesis**, Lambda Functions và S3 Bucket là một cách tiếp cận serverless để trích xuất, biến đổi và tải (ETL) dữ liệu theo thời gian thực. Trong mô hình này, Amazon Kinesis Data Streams sẽ thu thập dữ liệu streaming, AWS Lambda sẽ xử lý và biến đổi dữ liệu đó, và kết quả cuối cùng sẽ được lưu trữ trong Amazon S3 bucket để phân tích thêm hoặc lưu trữ lâu dài.

Việc sử dụng hệ thống này mang lại nhiều lợi ích so với các phương pháp truyền thống:

- **Không cần quản lý máy chủ**: AWS Lambda tự động mở rộng quy mô dựa trên lượng dữ liệu đến từ Kinesis streams, loại bỏ nhu cầu quản lý máy chủ.
- **Xử lý dữ liệu thời gian thực**: Dữ liệu được xử lý ngay khi đến Kinesis, cho phép biến đổi và phân tích tức thì.
- **Tiết kiệm chi phí**: Bạn chỉ trả tiền cho những gì mình sử dụng với AWS Lambda và S3, giúp giảm chi phí hạ tầng so với máy chủ truyền thống.
- **Tăng cường bảo mật**: Dữ liệu được xử lý trong môi trường an toàn, giảm thiểu rủi ro như lộ cổng dịch vụ hoặc phải quản lý khóa SSH.
- **Giám sát toàn diện**: AWS CloudWatch tích hợp liền mạch, cung cấp nhật ký và số liệu chi tiết để giám sát toàn bộ quá trình ETL.
- **Dễ dàng truy cập**: Dữ liệu đã xử lý được lưu trữ trong Amazon S3, dễ dàng tích hợp với các dịch vụ AWS khác cho việc phân tích hoặc lưu trữ lâu dài.

Bằng cách tận dụng Kinesis, Lambda và S3, bạn có thể tạo ra một giải pháp ETL thời gian thực có khả năng mở rộng, tiết kiệm chi phí và an toàn — mà không cần phải quản lý hạ tầng truyền thống phức tạp.

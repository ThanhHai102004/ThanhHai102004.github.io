---
title: "Build Backend API with API Gateway and Lambda"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

# XÂY DỰNG BACKEND API VỚI API GATEWAY VÀ LAMBDA

Backend sử dụng **Amazon API Gateway** để nhận request từ frontend và **AWS Lambda** để xử lý logic ticket.

### Nội dung thực hiện

1. Tạo các HTTP API route cho các tính năng ticket.
2. Cấu hình JWT Authorizer để bảo vệ các API.
3. Kết nối API Gateway với Lambda backend.
4. Kiểm thử các request từ frontend đến backend.

![](/images/5-Workshop/5.6-BuildBackendAPIwithAPIGatewayandLambda/api-overview.jpg)
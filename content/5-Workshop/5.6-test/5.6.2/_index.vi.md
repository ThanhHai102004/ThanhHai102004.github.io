---
title: "Cấu hình JWT Authorizer"
date: 2024-01-01
weight: 2
chapter: false
pre: "  5.6.2  "
---

JWT Authorizer được cấu hình để API Gateway chỉ chấp nhận các yêu cầu hợp lệ từ người dùng đã được xác thực thông qua Cognito.

### Các bước thực hiện

Tạo một JWT Authorizer trong API Gateway.

Cấu hình thông tin nhà phát hành (issuer) từ Cognito User Pool.

Gắn authorizer vào các route được bảo vệ.

Kiểm tra các yêu cầu có kèm theo token hợp lệ và không hợp lệ.

![](/images/5-Workshop/5.6-BuildBackendAPIwithAPIGatewayandLambda/jwt-authorizer.jpg)
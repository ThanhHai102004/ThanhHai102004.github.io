---
title: "Tạo HTTP API Routes"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

Tôi tạo các route API phục vụ chức năng quản lý ticket.

![](/images/5-Workshop/5.6-BuildBackendAPIwithAPIGatewayandLambda/routes.jpg)

### Các route chính

POST /tickets: tạo ticket mới.

GET /tickets: lấy danh sách ticket.

GET /tickets/{ticketId}: tra cứu một ticket.

PATCH /tickets/{ticketId}: cập nhật trạng thái và ghi chú.

DELETE /tickets/{ticketId}: xóa ticket.
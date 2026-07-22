---
title: "Store Ticket Data with DynamoDB"
date: 2024-01-01
weight: 7
chapter: false
pre: "  5.7.  "
---

Amazon DynamoDB được sử dụng để lưu trữ dữ liệu phiếu hỗ trợ (ticket) và thông tin kết nối WebSocket.

### Các bước thực hiện

Tạo bảng CampusSupportTickets để chứa dữ liệu phiếu hỗ trợ.

Thiết kế các thuộc tính như ticketId, userId, email, category, priority, status, adminNote, createdAt và updatedAt.

Hàm Lambda ghi dữ liệu phiếu hỗ trợ vào DynamoDB khi người dùng gửi phiếu.

Quản trị viên (Admin) đọc, cập nhật hoặc xóa phiếu hỗ trợ thông qua API.

![](/images/5-Workshop/5.7-StoreTicketDatawithDynamoDB/ticket-table-overview.jpg)


![](/images/5-Workshop/5.7-StoreTicketDatawithDynamoDB/ticket-items.jpg)
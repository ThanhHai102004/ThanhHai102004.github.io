---
title: "Cấu hình Thông báo và Giám sát"
date: 2024-01-01
weight: 9
chapter: false
pre: "  5.9.  "
---

Hệ thống sử dụng Amazon SES để gửi thông báo qua email và Amazon CloudWatch để ghi log, theo dõi lỗi và giám sát backend.

### Nội dung triển khai

Cấu hình định danh (identity) SES để gửi email thử nghiệm.

Lambda gửi email khi các ticket được tạo hoặc cập nhật.

CloudWatch Logs ghi lại các yêu cầu, lỗi và kết quả xử lý của Lambda.

Xác thực log khi frontend gọi các API.

![](/images/5-Workshop/5.9-ConfigureNotificationandMonitoring/ses-dashboard.png)

![](/images/5-Workshop/5.9-ConfigureNotificationandMonitoring/cloudwatch-dashboard.png)
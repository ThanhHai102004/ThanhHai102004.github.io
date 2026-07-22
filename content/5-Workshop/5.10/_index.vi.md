---
title: "Bảo mật và Quyền IAM"
date: 2024-01-01
weight: 9
chapter: false
pre: " <b> 5.10. </b> "
---

AWS IAM được sử dụng để cấp cho Lambda quyền truy cập vào các dịch vụ cần thiết như DynamoDB, S3, SES và CloudWatch.

### Các bước thực hiện

Tạo Vai trò (Role) IAM cho Lambda.

Cấp quyền truy cập vào các bảng DynamoDB.

Cấp quyền đọc/ghi các tệp đính kèm trong S3.

Cấp quyền ghi nhật ký (logs) vào CloudWatch.

Giữ cho các quyền tuân thủ nguyên tắc đặc quyền tối thiểu (least-privilege).

![](/images/5-Workshop/5.10-SecurityandIAMPermissions/iam-roles.png)

![](/images/5-Workshop/5.10-SecurityandIAMPermissions/iam-dashboard.png)

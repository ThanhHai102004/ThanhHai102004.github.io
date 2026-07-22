---
title: "Lưu trữ tệp đính kèm với Amazon S3"
date: 2024-01-01
weight: 8
chapter: false
pre: "  5.8.  "
---

Amazon S3 được sử dụng để lưu trữ các tệp đính kèm của ticket như ảnh chụp màn hình sự cố hoặc tài liệu hỗ trợ.

### Các bước thực hiện

Tạo một S3 bucket riêng tư để chứa các tệp đính kèm.

Lambda tạo các URL có chữ ký trước (presigned URL) để tải lên hoặc tải xuống.

Frontend tải các tệp lên S3 thông qua URL đã được tạo.

Khóa đối tượng (object key) của S3 được lưu trữ cùng với bản ghi ticket trong DynamoDB.

![](/images/5-Workshop/5.8-StoreAttachmentswithAmazonS3/s3-bucket.png)

![](/images/5-Workshop/5.8-StoreAttachmentswithAmazonS3/uploaded-files.png)
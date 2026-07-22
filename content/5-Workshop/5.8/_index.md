---
title: "Store Attachments with Amazon S3"
date: 2024-01-01
weight: 8
chapter: false
pre: " <b> 5.8. </b> "
---

Amazon S3 is used to store ticket attachments such as issue screenshots or supporting documents.

### Implementation steps

1. Create a private S3 bucket for attachments.
2. Lambda generates presigned URLs for upload or download.
3. The frontend uploads files to S3 through the generated URL.
4. The S3 object key is stored with the ticket record in DynamoDB.

![](/images/5-Workshop/5.8-StoreAttachmentswithAmazonS3/s3-bucket.png)

![](/images/5-Workshop/5.8-StoreAttachmentswithAmazonS3/uploaded-files.png)
---
title: "Security and IAM Permissions"
date: 2024-01-01
weight: 9
chapter: false
pre: " <b> 5.10. </b> "
---

AWS IAM is used to grant Lambda access to required services such as DynamoDB, S3, SES, and CloudWatch.

### Implementation steps

1. Create IAM Role for Lambda.
2. Grant permissions to access DynamoDB tables.
3. Grant permissions to read/write attachment files in S3.
4. Grant permissions to write logs to CloudWatch.
5. Keep permissions aligned with the least-privilege principle.

![](/images/5-Workshop/5.10-SecurityandIAMPermissions/iam-roles.png)

![](/images/5-Workshop/5.10-SecurityandIAMPermissions/iam-dashboard.png)

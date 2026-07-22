---
title: "Configure Notification and Monitoring"
date: 2024-01-01
weight: 9
chapter: false
pre: " <b> 5.9. </b> "
---

The system uses Amazon SES for email notifications and Amazon CloudWatch for logs, error tracking, and backend monitoring.

### Implementation content

1. Configure SES identity for test email sending.
2. Lambda sends emails when tickets are created or updated.
3. CloudWatch Logs records requests, errors, and Lambda processing results.
4. Validate logs when the frontend calls APIs.

![](/images/5-Workshop/5.9-ConfigureNotificationandMonitoring/ses-dashboard.png)

![](/images/5-Workshop/5.9-ConfigureNotificationandMonitoring/cloudwatch-dashboard.png)
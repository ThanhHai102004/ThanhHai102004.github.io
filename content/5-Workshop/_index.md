---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

### Project overview

This workshop documents the implementation process of Campus IT Support Ticket Portal, a serverless helpdesk web system for receiving and managing IT support requests in a campus environment.

**Deployed website:** https://main.d37atxjbyyp60m.amplifyapp.com/

The completed system allows users to register, sign in, submit support tickets, upload attachments, track ticket history, and receive status updates. Administrators can view all tickets, search and filter requests, update ticket status, add processing notes, delete tickets, and receive alerts for high-priority issues.

The frontend is deployed publicly through AWS Amplify Hosting and is integrated with GitHub for automatic build and deployment.

### Architecture

The system uses a serverless architecture on AWS. The frontend communicates with Amazon Cognito for authentication and sends authenticated requests to Amazon API Gateway. API Gateway validates Cognito JWT tokens before invoking AWS Lambda functions.

Lambda handles ticket operations, authorization checks, attachment processing, and integration with Amazon DynamoDB and Amazon S3. The system also uses Amazon SES, Amazon CloudWatch, AWS IAM, and real-time notification components such as DynamoDB Streams and WebSocket API.

![Sơ đồ](/images/2-Proposal/sodoDA.jpg)

### AWS services used

## AWS Services Used

| Service | Role in Workshop |
| :--- | :--- |
| AWS Amplify Hosting | Hosts the frontend and automatically deploys updates from GitHub |
| Amazon Cognito | Handles registration, login, logout, JWT tokens, and `Users`/`Admins` groups |
| Amazon API Gateway | Provides HTTP API and WebSocket API for frontend-backend communication |
| AWS Lambda | Processes ticket business logic, permission checks, notifications, and WebSocket events |
| Amazon DynamoDB | Stores ticket data and WebSocket connection information |
| Amazon S3 | Stores ticket attachments in a private bucket |
| Amazon SES | Sends ticket confirmation emails, alerts, and status change notifications |
| Amazon CloudWatch | Stores Lambda/API logs and supports system debugging and monitoring |
| AWS IAM | Enforces least-privilege permissions between Lambda and other AWS services |

### Implementation content

1. [Project Overview](5.1-Workshop-overview)
2. [Architecture Overview](5.2-Prerequiste/)
3. [Prerequisites](5.3-S3-vpc/)
4. [Deploy Frontend with AWS Amplify](5.4-S3-onprem/)
5. [Configure Authentication with Amazon Cognito](5.5-Policy/)
6. [Build Backend API with API Gateway and Lambda](5.6-Cleanup/)
7. [Store Ticket Data with DynamoDB]()
8. [Store Attachments with Amazon S3]()
9. [Configure Notification and Monitoring]()
10. [Security and IAM Permissions]()
11. [Testing the System]()
12. [System Screenshots and Result]()
13. [Resource and Cost Check]()
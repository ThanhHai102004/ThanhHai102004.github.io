---
title : "Project Overview"
date : 2024-01-01 
weight : 1 
chapter : false
pre : " <b> 5.1. </b> "
---

### Campus IT Support Ticket Portal
+ **Campus IT Support Ticket Portal** is a serverless helpdesk system designed for educational environments. It allows students and staff to submit IT support requests, track their processing status, and receive notifications when a ticket is created or updated.

The system also provides an administration interface for the IT support team. Administrators can receive, search, classify, update, add processing notes to, and delete tickets. Data displayed on the interface can be synchronized in real time without requiring the user to reload the page.

The project frontend is deployed using **AWS Amplify Hosting** at:

[Access Campus IT Support Ticket Portal](https://main.d37atxjbyyp60m.amplifyapp.com/)

### 1. Project Objectives

The project was developed to achieve the following objectives:

- Provide a centralized channel for students and staff to submit IT support requests.
- Support common issue categories such as WiFi, accounts, software, and devices.
- Allow users to track their ticket history and processing status.
- Allow users to attach images, PDF documents, and other related files.
- Send confirmation emails when tickets are created.
- Send notifications when ticket statuses or processing notes change.
- Synchronize ticket data in real time through WebSocket connections.
- Provide an administration dashboard for monitoring and processing tickets.
- Apply a serverless architecture to reduce server-management requirements.
- Automatically build and deploy the frontend from GitHub using AWS Amplify Hosting.

### 2. Target Users

The system supports two primary user groups.

#### Users

Users can be students or staff members of the educational institution. Their main functions include:

- Registering an account.
- Signing in and signing out.
- Submitting IT support requests.
- Selecting an issue category and priority level.
- Attaching files to a ticket.
- Receiving a ticket ID after submission.
- Looking up a ticket by its ID.
- Viewing previously submitted requests.
- Receiving email notifications and real-time status updates.

#### Administrators

Administrators are members of the IT support team. Their main functions include:

- Viewing the system overview dashboard.
- Viewing all submitted tickets.
- Searching and filtering tickets.
- Viewing ticket details and attachments.
- Updating ticket statuses.
- Adding processing notes.
- Deleting tickets.
- Receiving alerts for High and Critical priority tickets.

### 3. Main Technologies and AWS Services

The project uses the following technologies and services:

- **Hugo, HTML, CSS, and JavaScript**: used to build the frontend interface.
- **GitHub:** used for source-code management and version control.
- **AWS Amplify Hosting:** used for frontend hosting and CI/CD deployment.
- **Amazon Cognito:** used for registration, authentication, sign-out, and authorization.
- **Amazon API Gateway:** used to provide HTTP APIs and WebSocket APIs.
- **AWS Lambda:** used to process ticket logic, notifications, and WebSocket connections.
- **Amazon DynamoDB:** used to store tickets and WebSocket connection information.
- **Amazon S3:** used to store attachments in a private bucket.
- **Amazon SES:** used to send confirmation and notification emails.
- **Amazon CloudWatch:** used for logging and system monitoring.
- **AWS IAM:** used to manage service roles and access permissions.

### 4. Project Logo

The project uses the name Campus Support – Helpdesk Portal, representing a centralized technical support portal for an educational environment.

![project logo](/images/5-Workshop/5.1-Project%20Overview/project-logo.jpg)

### 5. Guest Interface

Before authentication, users can view the system introduction and access the sign-in and registration functions.

The interface displays the support request form, issue-information fields, and guidance to help users provide sufficient information to the IT support team.

![homepage](/images/5-Workshop/5.1-Project%20Overview/guest-homepage.jpg)

### 6. Authenticated User Interface

After successfully signing in through Amazon Cognito, the authenticated account information is displayed in the navigation bar.

Some form fields can be automatically populated using the authenticated user’s information. Users can submit tickets, view previously submitted requests, and receive status updates without reloading the page.

![](/images/5-Workshop/5.1-Project%20Overview/user-homepage.jpg)

### 7. Administrator Interface

The administrator page provides a dashboard containing an overview of the system, including:

- Total number of tickets.
- Number of tickets being processed.
- Number of high-priority tickets.
- Number of resolved tickets.

Administrators can search and filter tickets by status, priority, or issue category. They can also view ticket details, access attachments, update ticket statuses, and delete tickets.

Ticket data is retrieved from Amazon DynamoDB through Amazon API Gateway and AWS Lambda.

![](/images/5-Workshop/5.1-Project%20Overview/admin-dashboard.jpg)

### 8.Current Project Results

The project has produced a functional serverless helpdesk system with the following major components:

A publicly deployed frontend.

User registration, authentication, and sign-out.

User and Admin authorization.

An HTTP API for creating, reading, updating, and deleting tickets.

An Amazon DynamoDB database.

Private attachment storage using Amazon S3.

Asynchronous email notifications using Amazon SES.

Real-time updates through WebSocket connections.

Logging and monitoring through Amazon CloudWatch.

A CI/CD workflow from GitHub to AWS Amplify Hosting.

The next section presents the overall system architecture and the data flow between the project components.





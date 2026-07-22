---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

#  Campus IT Support Ticket Portal
## Serverless Helpdesk System on AWS for School IT Support

### 1. Project Overview
Campus IT Support Ticket Portal is a serverless helpdesk system designed for school environments. The system allows students and staff to submit IT support requests, track the history and processing status of tickets, and receive notifications when tickets are created or updated. Additionally, it provides an administrative interface for the IT team to receive, categorize, update, add processing notes, and delete tickets when necessary.

The frontend is publicly hosted using AWS Amplify Hosting and connected to GitHub to automatically build and deploy whenever source code changes occur. Users register and log in via the Amazon Cognito Hosted UI. The backend is built using Amazon API Gateway, AWS Lambda, Amazon DynamoDB, Amazon S3, Amazon SES, Amazon CloudWatch, and AWS IAM.

The project goes beyond standard CRUD ticket functionalities. The system also supports file attachments via S3 Presigned URLs, asynchronous email sending using Amazon SES, and real-time user interface updates through DynamoDB Streams combined with a WebSocket API.

### 2. Problem Statement & Solution
*Problem Statement*

In school environments, IT support requests are often reported via messaging apps, phone calls, emails, or direct conversations. This approach has several limitations:

- Requests can be forgotten, duplicated, or lack a clear processing history.
- The IT department lacks a centralized queue to prioritize issue resolution.
- Users find it difficult to track whether their tickets are in New, In Progress, Resolved, or Closed states.
- Admins need a clear interface to view ticket details, update statuses, and log resolution notes.
- Evidence files like error screenshots are often sent separately, complicating ticket management.

*Solution*

Campus IT Support Ticket Portal addresses these issues by providing a centralized helpdesk system with two main user roles:
- Users: Log in, submit tickets, upload attachments, and track their tickets.
- Admins: View all tickets, filter lists, view details, update statuses, add processing notes, and delete tickets.
- The application leverages managed AWS services to handle hosting, authentication, APIs, backend logic, databases, file storage, authorization, and monitoring.

### 3. Solution Architecture
#### Overall Architecture Diagram


![Sơ đồ](/images/2-Proposal/sodoDA.jpg)


#### Architecture Description
Users and administrators access the frontend hosted on AWS Amplify Hosting. When authentication is required, the browser is redirected to the Amazon Cognito Hosted UI. Upon successful authentication, Cognito issues a JWT token to the frontend.

The frontend sends the JWT token in requests to the Amazon API Gateway HTTP API. The API Gateway uses a JWT Authorizer to validate the token before forwarding requests to the CampusSupportTicketService Lambda. The Lambda processes ticket business logic, validates User/Admin permissions, stores data in the CampusSupportTickets DynamoDB table, and generates S3 Presigned URLs to upload or download attachments within a private bucket.

When a ticket is created or updated, DynamoDB Streams trigger the CampusSupportNotificationService. This Lambda sends emails via Amazon SES and dispatches real-time events through the API Gateway WebSocket API. WebSocket connection information is managed by the CampusSupportWebSocketService and stored in the CampusSupportConnections DynamoDB table.

### 4. AWS Services Used
- **AWS Amplify Hosting:** Hosts the frontend and handles automatic builds and deployments from GitHub.
- **Amazon Cognito Hosted UI:** Manages registration, login, logout, and user sessions.
- **Cognito Groups:** Authorizes accounts into User and Admin groups.
- **API Gateway HTTP API:** Provides endpoints for ticket creation, reading, updating, and deletion operations.
- **API Gateway JWT Authorizer:** Validates JWT tokens from Cognito before allowing API calls.
- **API Gateway WebSocket API** Sends real-time updates to User/Admin browsers.
- **AWS Lambda:** Handles ticket business logic, notifications, WebSockets, and permission checks.
- **Amazon DynamoDB:** Stores ticket data and WebSocket connection information.
- **DynamoDB Streams:** Detects ticket creation or update events to trigger notifications.
- **Amazon S3:** Stores file attachments in a private bucket.
- **S3 Presigned URL:** Allows temporary file uploading/downloading without making the bucket public.
- **Amazon SES:** ends confirmation emails, high-priority ticket alerts, and status change updates.
- **Amazon CloudWatch:** Stores Lambda/API logs and supports debugging and error tracking.
- **AWS IAM:** Enforces least-privilege permissions between Lambda and other AWS services.

### 5. Core Features
#### User-Facing Features
- Register, log in, and log out using Amazon Cognito.
- Submit support requests categorized by WiFi, accounts, software, or hardware.
- Select priority levels and input issue descriptions.
- Attach PDF, PNG, JPG, or WebP files.
- Receive a ticket code upon submission.
- Look up tickets using their code.
- View history of submitted requests.
- Receive confirmation emails and real-time status updates.

#### Administrator-Facing Features
- View a dashboard displaying total tickets, in-progress tickets, high-priority tickets, and resolved tickets.
- Search and filter tickets by status, priority, or issue category.
- View ticket details and file attachments.
- Update statuses and add processing notes.
- Delete tickets from the system within the demo scope.
- Receive email alerts when High or Critical tickets are created.
- Automatically update the ticket list upon changes without requiring page reloads.

### 6. Implemented APIs
![Api](/images/2-Proposal/Api.jpg)

### 7. Core Data Model
#### Bảng CampusSupportTickets 
![Campussupportticket](/images/2-Proposal/campusticket.jpg)

### 8. Testing Plan

| Test Case | Expected Result |
| :--- | :--- |
| User registers and logs in | Cognito authenticates successfully, and the account belongs to the Users group |
| User submits a valid ticket | Ticket is saved to DynamoDB, and a ticket code is returned |
| User uploads an attachment file | File is uploaded to S3 via a Presigned URL |
| User looks up a ticket | System returns the correct ticket information |
| Admin views the dashboard | Ticket lists and metrics display correctly |
| Admin updates status | DynamoDB is updated, and a MODIFY event is triggered |
| Admin deletes a ticket | Ticket is deleted from DynamoDB |
| Ticket is created | SES sends a confirmation email to the verified address |
| High/Critical ticket is created | SES sends an alert email to the IT team |
| Ticket is modified | WebSocket sends an event so the interface updates without reloading |
| Request lacks JWT | API Gateway rejects the request |
| Regular user calls admin API | Lambda rejects the operation |
| Backend encounters an error | CloudWatch Logs record the error for debugging |

### 9. Cost Estimation

| Service | Estimated Cost/Month | Notes |
| :--- | :--- | :--- |
| AWS Amplify Hosting | ~$0-2 | Low frontend traffic |
| Amazon Cognito | ~$0 | Suitable for demo users within the free tier |
| API Gateway HTTP/WebSocket API | ~$0-2 | Depends on request volume and realtime connections |
| AWS Lambda | ~$0-1 | Runs based on requests/events |
| Amazon DynamoDB | ~$0-2 | Small ticket data volume, uses on-demand capacity |
| Amazon S3 | ~$0-1 | Small file attachment storage size |
| Amazon SES | ~$0-1 | Low demo email volume |
| Amazon CloudWatch | ~$0-1 | Basic logging for Lambda/API |
| **Total** | **~$0-10/month** | Depends on traffic, file size, and email volume |

### 10. Risks and Limitations

| Risk/Limitation | Impact | Mitigation Strategy |
| :--- | :--- | :--- |
| SES is in Sandbox mode | Can only send emails to verified addresses | Request production access if deploying live |
| Cognito group misconfiguration | Users/Admins might have incorrect permissions | Validate group claims inside Lambda |
| Overly broad IAM roles | Increases security risks | Apply the principle of least privilege |
| S3 bucket accidentally made public | Attachment files could be exposed | Keep buckets private and use Presigned URLs |
| Misconfigured CORS | Frontend cannot invoke APIs | Configure CORS based on the Amplify domain |
| WebSocket connection timeout | Interface stops receiving realtime updates | Remove broken connection IDs and reconnect when necessary |
| Forgetting to clean up resources | Incurs unexpected costs | Monitor the Billing Dashboard and document cleanup steps |

### 11. Expected Results
The project aims to deliver a complete serverless helpdesk system tailored for a junior cloud portfolio project, achieving the following outcomes:
- Public deployment of the frontend using AWS Amplify Hosting.
- User and Admin authentication and authorization via Amazon Cognito.
- API protection powered by a JWT Authorizer.
- Lambda functions handling ticket business logic and access control.
- DynamoDB storing ticket entries and WebSocket connections.
- S3 managing private file attachments securely through Presigned URLs.
- SES handling confirmation and notification emails.
- WebSockets enabling real-time user interface updates.
- CloudWatch providing error observation and debugging capabilities.
- IAM enforcing the minimum necessary permissions for each Lambda function.
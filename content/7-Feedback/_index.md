---
title: "Sharing and Feedback"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 7. </b> "
---

# SHARING AND FEEDBACK

## Learning and Implementation Experience
During the internship, I started by learning AWS fundamentals and core services, then gradually moved to more advanced topics such as serverless, security, databases, serverless computing, CI/CD, monitoring, and cost control. Writing weekly worklogs helped me review what I learned, identify difficulties, and complete missing parts before finalizing the report.

My main project was **Campus IT Support Ticket Portal**, a web-based system for submitting and managing IT support requests in a campus environment. The system includes two main user tiers: users can submit tickets, track their status, and upload attachments; administrators can view ticket lists, filter requests, update status, add resolution notes, and delete tickets when needed.

The most important point of this project is that it was built with a serverless architecture on AWS. The frontend is deployed with **AWS Amplify Hosting**, authentication is handled by **Amazon Cognito**, APIs are managed by **Amazon API Gateway**, backend logic runs on **AWS Lambda**, data is stored in **Amazon DynamoDB**, attachments are stored in **Amazon S3**, notifications use **Amazon SES**, logs are monitored through **Amazon CloudWatch**, and all permissions are controlled by **AWS IAM**.

Through this project, I understood that a complete cloud application is not only about creating individual services. The more important part is designing the connection flow between services, applying suitable permissions, testing each function carefully, and documenting the implementation clearly enough for others to understand.

## Knowledge Gained

- I understood how a frontend can be hosted and automatically deployed through **AWS Amplify Hosting**.
- I learned how **Amazon Cognito** supports sign up, sign in, JWT tokens, and authorization through `Users`/`Admins` groups.
- I understood the role of **API Gateway** in receiving requests, validating JWT tokens, and forwarding requests to **AWS Lambda**.
- I practiced implementing server operations with **AWS Lambda**, including create, read, update, and delete functions.
- I learned how to store NoSQL data in **Amazon DynamoDB** and manage attachments with **Amazon S3**.
- I became familiar with email notifications using **Amazon SES** and real-time updates flows using **Amazon DynamoDB Streams / WebSocket**.
- I learned to use **Amazon CloudWatch** to inspect errors and monitor backend activity.
- I became more aware of **AWS least privilege** and cost monitoring through **Billing Dashboard**.

## Difficulties

During implementation, I faced several difficulties when connecting services together. For example, the Cognito and JWT Authorizer flow was easy to miss-configured at first because the frontend, API Gateway, and Lambda all needed to handle the token and user permissions correctly. Separating normal user permissions from admin permissions also required careful testing to prevent users from accessing administrative functions.

Another challenge was backend debugging. When a frontend request did not work as expected, I had to check multiple layers such as API Gateway configuration, Lambda logs, DynamoDB data, IAM permissions, and CORS settings. As I became more familiar with CloudWatch Logs, I would identify issues faster and test the system step-by-step.

Documentation also took considerable time because the Working, Proposal, Blogs Posted, Workshop, Self-Assessment, and Sharing and Feedback sections needed to be consistent with one another. When the architecture or project content changed, related documentation sections also had to be updated to avoid inconsistency.

## Feedback and Suggestions

From my experience, the workshop-based learning format is suitable for students because it combines theory with hands-on practice. However, to learn more effectively, learners should record notes while implementing, capture screenshots after important steps, and update the architecture diagram as references if project changes.

I also realized that cleanup and Billing Dashboard monitoring should be prepared carefully. New AWS learners may focus on creating resources and forget to check whether resources are still running after practice. Cost monitoring should become a habit from the beginning.

If I continue developing this project, I would be interest the following items:

- Build a dashboard for ticket statistics by status, priority, and category.
- Improve the admin interface for filtering and batching tickets, income cleaner.
- Add and logs for administrative actions.
- Complete custom domain configuration of the domain and domain verification process allow it.
- Define IAM policies so service-on-service permissions are more strictly controlled.

## Conclusion

Overall, the internship gave me a more practical view of how to build a serverless application on AWS. I not only learned how to use individual AWS services, but also understood system flow design, access control, error monitoring, cost management, and technical documentation. This experience gave me a stronger foundation to continue learning cloud computing and building AWS projects in the future.
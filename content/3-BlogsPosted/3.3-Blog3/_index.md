---
title: "Blog 3: Learning Serverless, Authentication, Monitoring, and Security on AWS"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

After practicing core AWS services, I moved on to the serverless components to build the Campus IT Support Ticket Portal project. This was the stage where I learned the most, because the services no longer stood in isolation; instead, they had to be connected into a complete workflow: the frontend calls the API, the API validates the token, the backend processes the business logic, data is saved to the database, files are stored in storage, and errors are tracked through logs.

The service I got acquainted with first was AWS Lambda. At first, it took me some time to shift my mindset. With traditional servers, backend applications usually run continuously. With Lambda, functions only execute when triggered by a request or an event. This approach fits functions like creating tickets, updating ticket statuses, retrieving ticket lists, or handling file attachments perfectly.

When writing logic for Lambda, I realized that a function should not shoulder too many responsibilities. A function is much easier to control when it has a clear workflow: receiving the request, validating input data, processing the business logic, calling DynamoDB or S3 if necessary, and returning a response. Packing too much mixed logic into one place makes debugging a nightmare, especially when errors only show up in CloudWatch Logs.

API Gateway was the next component I practiced. This is where the frontend communicates with the backend. I created routes corresponding to the system's features, such as submitting tickets, fetching ticket lists, updating statuses, or deleting tickets. While configuring the API, I had to pay close attention to HTTP methods, CORS, and how routes invoke Lambda functions. There were times when the frontend faced CORS errors when calling the API, which helped me understand that just because a frontend is running doesn't mean the API is ready for browser calls.

The authentication part took up much more time than I anticipated. I used Amazon Cognito to manage user registration, login, and User/Admin authorization. Initially, JWT tokens were a bit abstract because they travel through multiple steps: the user logs in, Cognito returns a token, the frontend stores and attaches the token when calling APIs, and API Gateway uses a JWT Authorizer to verify the token before letting the request pass through.

Once I grasped that flow, I saw how Cognito makes the project much cleaner. Regular users only need to submit and view their own tickets. Admins require broader permissions to view ticket lists, update statuses, add resolution notes, or delete tickets. From there, I drew a clear line between authentication and authorization. Authentication answers the question "who is the user," while authorization answers "what is this user allowed to do."

For ticket data, I used DynamoDB. Unlike RDS, DynamoDB forced me to think ahead about how the application would query the data. For the Ticket Portal, the primary operations include creating tickets, fetching tickets by user, administrative listing, updating statuses, and deleting tickets. Once these operations were defined, designing items and keys in DynamoDB became much more straightforward.

S3 was utilized for file attachments. I did not want to store files directly inside the database because that would bloat the ticket data and complicate management. A much more logical approach is to store files in S3, while DynamoDB only retains metadata like file names or object keys. This keeps the ticket items lightweight while ensuring the system still knows which file belongs to which ticket.

Monitoring proved to be a genuinely practical skill during project development. When the backend throws an error, without checking logs, you are practically guessing in the dark. CloudWatch Logs helped me verify whether the Lambda function was invoked, whether the request body was correct, and whether the error stemmed from input validation, IAM permissions, DynamoDB, or S3. There was a time when the error wasn't in the core code but rather in the Lambda role's permissions, and I only discovered it after reading the logs.

Security was another area I had to review multiple times. I checked Lambda IAM roles, DynamoDB access permissions, S3 bucket rules, CORS settings, and routes requiring tokens. For a student project, it might not reach full production grade, but I still wanted the system to have a sensible permission structure: regular users shouldn't perform admin tasks, buckets shouldn't be publicly exposed carelessly, and the backend shouldn't hold overly broad privileges.

A small yet crucial task at the end of the learning process was resource cleanup and Billing checks. After every session of creating or testing resources, I reviewed what was still active. This helped prevent unexpected cost generation and gave me a clearer understanding of which resources truly belonged to the project.

My key takeaway from this phase is that serverless does not mean simpler in terms of architectural thinking. It reduces server management overhead, but it demands a deep understanding of each service's responsibility. API Gateway acts as the API gateway, Lambda processes logic, Cognito manages identities, DynamoDB stores data, S3 stores files, CloudWatch supports error observation, and IAM controls access permissions.

After stitching these parts together, I gained a better grasp of how a cloud application operates end-to-end. This also made it easier for me to write workshops clearly, as every deployment step had a specific purpose rather than just blindly following instructions: deploying the frontend, configuring logins, setting up APIs, writing backend code, storing data, testing user/admin roles, inspecting logs, and cleaning up resources.

Published blog link: [AWS Study Group VN](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2219706598794300/)

## References
- [AWS Lambda Deverloper Guide](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)
- [Amazon API Gateway REST API](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-rest-api.html)
- [Amazon Cognito Deverloper Guide](https://docs.aws.amazon.com/cognito/latest/developerguide/what-is-amazon-cognito.html)
- [What is Amazon DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html)
- [Sending Lambda logs to CloudWatch Logs](https://docs.aws.amazon.com/lambda/latest/dg/monitoring-cloudwatchlogs.html)
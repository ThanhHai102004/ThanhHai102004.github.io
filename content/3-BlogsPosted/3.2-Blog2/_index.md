---
title: "Blog 2: Practicing Core AWS Services: EC2, S3, VPC, and Databases"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

After becoming more familiar with the AWS account and the management console, I moved on to practicing core services. This was the stage where I started to see that AWS is not just a disjointed list of services, but rather a collection of building blocks that can be combined to form a complete system. The services I focused on the most include EC2, S3, VPC, Security Groups, IAM, and databases like RDS/Aurora.

I started with EC2 because it is the service that best visualizes the concept of cloud compute. When launching an instance, I had to choose the AMI, instance type, key pair, network, and security group. At first, these selections seemed like mere configuration steps, but through more hands-on practice, I realized that each choice directly affects how the instance behaves. The AMI determines the operating system, the instance type determines the compute resources, and the security group dictates what inbound traffic the instance is allowed to receive.

One key takeaway from working with EC2 is that creating resources is extremely fast, but managing them requires careful attention. After finishing my tests, I had to check whether the instances were still running, whether they had public IPs, and whether the security groups had overly permissive open ports. These small tasks helped me build the habit of reviewing resources after every practice session.

Next, I studied Amazon S3. Initially, I thought S3 was simply a place to upload files, but upon diving deeper, I realized it involves data organization and access control. I practiced creating buckets, uploading objects, checking object keys, toggling public access settings, and observing how bucket policies or IAM permissions affect access rights.

S3 helped me understand a crucial principle: data should not be made public unless strictly necessary. In my Ticket Portal project, file attachments could be error screenshots or user-submitted documents. These files should not be accessible by everyone. A more secure approach is to store files in S3 while the application controls access via the backend and IAM roles.

VPC proved to be significantly more challenging than EC2 and S3. Concepts like subnets, route tables, internet gateways, and security groups were initially easy to confuse. I had to review the materials multiple times and practice step-by-step to understand how traffic flows. When a resource failed to connect, I couldn't just look in one place; I had to check subnets, route tables, security groups, and how the resource was positioned within the network topology.

Through VPC practice, I gained a clearer understanding of why network design heavily impacts security. Not every resource should be exposed to the internet. If a database only serves the backend, it should be protected within an appropriate network boundary instead of being publicly open. Although my final project relied heavily on serverless services, the knowledge of VPC helped me understand how AWS organizes networking environments and how to approach real-world system architecture design.

I also practiced with Amazon RDS and Aurora to understand relational databases on AWS. Compared to self-hosting a database on a server, RDS significantly reduces operational overhead, but that does not mean configuration can be ignored. I still had to pay attention to database engines, instance sizes, backups, networking, and security. This taught me that managed services do not completely replace design thinking; rather, they eliminate repetitive operational tasks.

When comparing RDS to DynamoDB, I began to see that choosing a database must be driven by how the application accesses data. RDS is well-suited for relational data, SQL queries, and operations requiring joins. DynamoDB is better tailored for predictable access patterns, high performance, and serverless models. For a ticketing system where operations like creating tickets, viewing lists, updating statuses, and deleting tickets are well-defined, DynamoDB was a logical choice for my final project.

During this phase, I also continued participating in workshops via the AWS Study Group. The most valuable aspect was getting to manually provision resources, configure them, test, and troubleshoot errors. Some mistakes were quite simple, such as picking the wrong region, missing security group rules, or lacking IAM role permissions, but those exact errors helped me truly understand how the services work. Relying solely on documentation would have made it much harder to retain these lessons for long.

After practicing these core services, I developed a clearer perspective on each layer of a cloud system. EC2 explains compute, S3 explains storage, VPC explains networking, RDS/Aurora explains relational databases, while IAM and Billing serve as constant reminders that security and cost management must always go hand in hand with deployment.

This phase laid a solid foundation for my transition to serverless. Once I understood traditional compute, storage, networking, and databases, it became much easier to conceptualize how services like API Gateway, Lambda, Cognito, DynamoDB, S3, and CloudWatch integrate into a complete application.

Published blog link: [AWS Study Group VN](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2219703182127975/)

## References
- [Amazon EC2 Usrer Guide](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html)
- [What is Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html)
- [What is Amazon VCP](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html)
- [Amazon RDS User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html)
- [Amazon Aura User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/CHAP_AuroraOverview.html)
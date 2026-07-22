---
title: "Blog 1: Learning AWS from Account Creation, IAM, to Cost Control"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

When I first started learning AWS, I used to think the hardest part would be deploying a running system on the cloud. However, after practicing for a few initial sessions, I realized that the first things to master are actually the very basics: creating an account correctly, understanding the region in use, knowing where to check costs, and avoiding granting overly broad permissions to resources.

The first thing I did was log into the AWS Management Console and get familiar with the interface. At first, I felt quite overwhelmed because the console has numerous services, each with its own dashboard and naming convention. I had to manually search for services like EC2, S3, IAM, Billing, and CloudWatch to gradually get used to their locations. One small habit that helped me avoid mistakes later on is always checking the region in the top-right corner before creating any resources. There were times I couldn't find a resource, only to realize I was looking in the wrong region.

After getting familiar with the console, I began paying more attention to the Billing Dashboard. This is an area that I believe AWS students should check frequently. When working locally, a configuration error usually just wastes time fixing it. On the cloud, if you create resources and forget to delete them, costs can actually incur. Therefore, I formed the habit of checking Billing, Free Tier, and the list of created resources after every practice session.

During my studies, I noticed certain services can easily incur costs if not managed carefully, such as EC2 instances, NAT Gateways, Load Balancers, Route 53 domains, or long-term data storage. I didn't use all of those services in my final project, but knowing about them beforehand made me more cautious when reading workshops or following guides. To me, cost control is no longer a secondary task, but an integral part of responsible cloud learning.

The next topic I studied was IAM. Initially, IAM felt dry because many concepts look similar: users, groups, roles, and policies. It took me a while to distinguish that a user represents a human identity, a group is used to bundle permissions for multiple users, a role is typically assumed by services, and a policy describes the allowed permissions. Once I understood these concepts, I saw why AWS always emphasizes the principle of least privilege.

During practice, there were times when I wanted to grant broad permissions just to get things done quickly. But relating this to the Ticket Portal project, I realized that approach was unsafe. For example, a Lambda function that only needs to read/write tickets in DynamoDB should not have full Administrator access. If Lambda only uploads attachments to a specific S3 bucket, its role permissions should also be restricted to that bucket. Learning IAM early on helped me view security as part of the design, rather than just a formality added at the end of a project.

I also practiced creating an EC2 instance to understand traditional compute on AWS. When launching an instance, I had to choose the AMI, instance type, key pair, security group, and network settings. These steps helped me understand how a virtual server on AWS is configured. Even though my final project relied more on serverless architecture, EC2 remained a valuable topic because it gave me a foundational baseline to compare against Lambda.

A minor error I encountered while learning EC2 was misconfiguring the security group, which prevented me from accessing the instance as intended. From that mistake, I learned that creating a resource doesn't mean it is immediately ready for use. Network rules, ports, inbound traffic, and access permissions all directly impact the outcome of your practice. Such minor mistakes helped me remember lessons much longer than just reading documentation.

Aside from foundational services, I also briefly explored Amazon Bedrock. I didn't use Bedrock as a core service in my project, but this section showed me that AWS offers more than just infrastructure like servers, storage, or databases. AWS also provides various higher-level managed services tailored for modern application and AI use cases.

Reflecting on the initial phase, my takeaway is that learning AWS should not start with trying to use a massive number of services all at once. First, you need to know how to use an account securely, check costs, understand IAM, and navigate the console. These tasks sound simple, but skipping them makes it easy to run into hard-to-control errors when building larger projects.

To me, this stage felt like laying the groundwork. Once I became comfortable with the console, knew how to check Billing, and understood the basics of IAM, I felt much more confident moving on to core services like EC2, S3, VPC, RDS, and eventually the serverless services used for the Campus IT Support Ticket Portal project.

Published blog link: [AWS Study Group VN](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2219698898795070/)

## References
- [Getting started with AWS](https://docs.aws.amazon.com/whitepapers/latest/aws-overview/getting-started-with-aws.html)
- [AWS Management Console](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/what-is.html)
- [AWS Billing and Cost Management](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/billing-what-is.html)
- [Security best practice IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
- [Amazon EC2 Usrer Guide](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html)
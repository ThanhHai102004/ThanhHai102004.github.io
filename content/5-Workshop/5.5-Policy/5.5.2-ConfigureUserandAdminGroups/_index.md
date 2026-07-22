---
title : "Configure User and Admin Groups"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.5.2 </b> "
---
The system uses Cognito Groups to separate normal users and administrators.


#### Implementation steps

Create the Users group for ticket submitters.

Create the Admins group for IT administrators.

Assign test accounts to the correct group.

Backend Lambda reads group information from JWT claims for permission checks.


![](/images/5-Workshop/5.5-ConfigureAuthenticationwithAmazonCognito/user-groups.jpg)
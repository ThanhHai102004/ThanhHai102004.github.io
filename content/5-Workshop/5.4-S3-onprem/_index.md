---
title : "Deploy Frontend with AWS Amplify"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---
The system frontend is deployed with AWS Amplify Hosting. Amplify is connected to GitHub so the frontend can be built and deployed automatically whenever the source code changes.

#### Implementation steps

Open AWS Amplify Console and create a new application.

Connect Amplify to the project GitHub repository.

Select the main branch for deployment.

Review build settings and start deployment.

After deployment succeeds, open the default Amplify domain to validate the website.

![](/images/5-Workshop/5.4-DeployFrontendwithAWSAmplify/amplify-hosting.jpg)

![](/images/5-Workshop/5.4-DeployFrontendwithAWSAmplify/deployment-success.jpg)

### Result

The website is publicly available at: https://main.d37atxjbyyp60m.amplifyapp.com/

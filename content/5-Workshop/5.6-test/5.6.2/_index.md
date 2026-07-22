---
title: "Configure JWT Authorizer"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.6.2 </b> "
---

JWT Authorizer is configured so API Gateway only accepts valid requests from users authenticated through Cognito.

### Implementation steps

Create a JWT Authorizer in API Gateway.

Configure issuer information from Cognito User Pool.

Attach the authorizer to protected routes.

Test requests with and without a valid token.

![](/images/5-Workshop/5.6-BuildBackendAPIwithAPIGatewayandLambda/jwt-authorizer.jpg)
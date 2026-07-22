---
title: "Connect API Gateway to Lambda"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.6.3 </b> "
---

API Gateway is integrated with Lambda so valid requests can be forwarded to the backend for processing.

### Implementation steps

Create Lambda integration for API Gateway.

Attach the integration to ticket routes.

Verify that Lambda receives events from API Gateway.

Monitor Lambda logs when the frontend calls the API.

![](/images/5-Workshop/5.6-BuildBackendAPIwithAPIGatewayandLambda/lambda-integration.jpg)

![](/images/5-Workshop/5.6-BuildBackendAPIwithAPIGatewayandLambda/lambda-code.jpg)
---
title: "Create HTTP API Routes"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

I created API routes for ticket-management functions.

![](/images/5-Workshop/5.6-BuildBackendAPIwithAPIGatewayandLambda/routes.jpg)

### Main routes

POST /tickets: create a new ticket.

GET /tickets: get ticket list.

GET /tickets/{ticketId}: look up one ticket.

PATCH /tickets/{ticketId}: update status and notes.

DELETE /tickets/{ticketId}: delete a ticket.
---
title: "Store Ticket Data with DynamoDB"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

Amazon DynamoDB is used to store ticket data and WebSocket connection information.

### Implementation steps

1. Create the CampusSupportTickets table for ticket data.
2. Design attributes such as ticketId, userId, email, category, priority, status, adminNote, createdAt, and updatedAt.
3. Lambda writes ticket data to DynamoDB when users submit tickets.
4. Admins read, update, or delete tickets through the API.

![](/images/5-Workshop/5.7-StoreTicketDatawithDynamoDB/ticket-table-overview.jpg)


![](/images/5-Workshop/5.7-StoreTicketDatawithDynamoDB/ticket-items.jpg)
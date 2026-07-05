---
title: "Module 8: Notifications Pipeline"
weight: 8
pre: "<b>5.8. </b>"
---

## Module 8: Notifications Pipeline

**Member:** Huy

### 8.1 SNS Topic Setup

![SNS overview](/images/workshop/64.png)

**Step 1:** AWS Console → SNS → Topics → Create topic

![Create topic](/images/workshop/65.png)
![Topic type](/images/workshop/66.png)
![Topic created](/images/workshop/67.png)

- Type: Standard
- Name: `budget-tracket-notifications-dev`
- Create topic
- Copy Topic ARN: `arn:aws:sns:ap-southeast-1:<account>:budget-tracket-notifications-dev`

**Step 2:** Create Email Subscription

![Create subscription](/images/workshop/68.png)
![Email subscription details](/images/workshop/69.png)

- Create subscription
- Protocol: Email
- Endpoint: `your-email@example.com`
- Create subscription
- Check your inbox → Confirm the SNS subscription

### 8.2 SQS Queue Setup

![SQS overview](/images/workshop/70.png)

**Step 1:** AWS Console → SQS → Create queue

![Create queue](/images/workshop/71.png)
![Queue configuration](/images/workshop/72.png)
![Queue created](/images/workshop/73.png)

- Queue name: `budget-tracket-notifications-dev`
- Type: Standard
- Configuration:
  - Message retention period: 4 days
  - Visibility timeout: 30 seconds
  - Receive message wait time: 20 seconds
- Create queue
- Copy the Queue URL

**Step 2:** Dead Letter Queue

![Create DLQ](/images/workshop/74.png)

- Create queue
- Queue name: `budget-tracket-notifications-dev-dlq`
- Create queue

**Step 3:** Set Redrive Policy

![Redrive policy setting](/images/workshop/75.png)
![Redrive policy saved](/images/workshop/76.png)

- SQS Queue → Edit → Dead letter queue
- Enable redrive policy: Yes
- Dead letter queue: select the DLQ
- Maximum receives: 3
- Save

### 8.3 EventBridge Rule for Monthly Summary

![EventBridge overview](/images/workshop/77.png)

**Step 1:** AWS Console → EventBridge → Rules → Create rule

![Create rule](/images/workshop/78.png)
![Rule details](/images/workshop/79.png)

- Name: `BudgetTracketMonthlySummary`
- Event bus: default
- Next

**Step 2:** Schedule
- Schedule pattern: Cron
- Cron expression: `cron(0 1 1 * ? *)` (1 AM on the 1st of each month)
- Next

**Step 3:** Target
- Target types: AWS service
- Select a target: Lambda function
- Function: `BudgetTracket-MonthlySummaryFunction-dev`
- Create rule

### 8.4 NotificationFunction Lambda

```
// BudgetTracket.Lambda/Functions/NotificationFunction.cs
```

![NotificationFunction implementation](/images/workshop/80.png)

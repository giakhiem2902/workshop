---
title: "Module 10: Monitoring & Operations"
weight: 10
pre: "<b>5.10. </b>"
---

## Module 10: Monitoring & Operations

**Member:** Whole team

### 10.1 CloudWatch Logs

![CloudWatch log groups](/images/workshop/81.png)
![Log group details](/images/workshop/82.png)

AWS Console → CloudWatch → Log groups

Log groups created automatically:
- `/aws/lambda/BudgetTracket-AuthFunction-dev`
- `/aws/lambda/BudgetTracket-TransactionFunction-dev`
- `/aws/lambda/BudgetTracket-BudgetFunction-dev`
- `/aws/lambda/BudgetTracket-ReportFunction-dev`
- `/aws/lambda/BudgetTracket-AiFunction-dev`
- `/aws/lambda/BudgetTracket-ProfileFunction-dev`
- `/aws/lambda/BudgetTracket-NotificationFunction-dev`
- `/aws/lambda/BudgetTracket-MonthlySummaryFunction-dev`

### 10.2 CloudWatch Metrics & Alarms

**Step 1:** Create an Alarm for Lambda Errors

![Create alarm](/images/workshop/83.png)

- CloudWatch → Alarms → Create alarm
- Metric: Lambda → Errors
- Function: `BudgetTracket-AuthFunction-dev`
- Statistic: Sum
- Period: 5 minutes
- Threshold: >= 5
- Action: Send SNS notification
- Create alarm

Meaning: if AuthFunction has ≥ 5 errors in 5 minutes, send an email alert.

**Step 2:** Create an Alarm for DynamoDB

- Metric: DynamoDB → ConsumedWriteCapacityUnits
- Table: `BudgetTracket-dev`
- Threshold: >= 80% of provisioned capacity
- Create alarm (same steps as above)

Meaning: alert when approaching the DynamoDB write limit.

### 10.3 WAF Monitoring

![WAF monitoring dashboard](/images/workshop/84.png)

- WAF & Shield → Web ACLs → `BudgetTracketWAF`
- Monitoring tab
- View blocked requests by rule

### 10.4 Lambda Performance Insights

Get Lambda invocation metrics:

![Lambda performance metrics](/images/workshop/85.png)

Output:

![Lambda metrics output](/images/workshop/86.png)

---
title: "Module 8: Notifications Pipeline"
weight: 8
pre: "<b>5.8. </b>"
---

## Module 8: Notifications Pipeline

**Thành viên:** Huy

### 8.1 SNS Topic Setup

![Tổng quan SNS](/images/workshop/64.png)

**Bước 1:** AWS Console → SNS → Topics → Create topic

![Create topic](/images/workshop/65.png)
![Loại topic](/images/workshop/66.png)
![Topic đã tạo](/images/workshop/67.png)

- Type: Standard
- Name: `budget-tracket-notifications-dev`
- Create topic
- Copy Topic ARN: `arn:aws:sns:ap-southeast-1:<account>:budget-tracket-notifications-dev`

**Bước 2:** Create Email Subscription

![Create subscription](/images/workshop/68.png)
![Chi tiết email subscription](/images/workshop/69.png)

- Create subscription
- Protocol: Email
- Endpoint: `your-email@example.com`
- Create subscription
- Check inbox → Confirm SNS subscription

### 8.2 SQS Queue Setup

![Tổng quan SQS](/images/workshop/70.png)

**Bước 1:** AWS Console → SQS → Create queue

![Create queue](/images/workshop/71.png)
![Cấu hình queue](/images/workshop/72.png)
![Queue đã tạo](/images/workshop/73.png)

- Queue name: `budget-tracket-notifications-dev`
- Type: Standard
- Configuration:
  - Message retention period: 4 days
  - Visibility timeout: 30 seconds
  - Receive message wait time: 20 seconds
- Create queue
- Copy Queue URL

**Bước 2:** Dead Letter Queue

![Tạo DLQ](/images/workshop/74.png)

- Create queue
- Queue name: `budget-tracket-notifications-dev-dlq`
- Create queue

**Bước 3:** Set Redrive Policy

![Thiết lập redrive policy](/images/workshop/75.png)
![Đã lưu redrive policy](/images/workshop/76.png)

- SQS Queue → Edit → Dead letter queue
- Enable redrive policy: Yes
- Dead letter queue: Select DLQ
- Maximum receives: 3
- Save

### 8.3 EventBridge Rule for Monthly Summary

![Tổng quan EventBridge](/images/workshop/77.png)

**Bước 1:** AWS Console → EventBridge → Rules → Create rule

![Create rule](/images/workshop/78.png)
![Chi tiết rule](/images/workshop/79.png)

- Name: `BudgetTracketMonthlySummary`
- Event bus: default
- Next

**Bước 2:** Schedule
- Schedule pattern: Cron
- Cron expression: `cron(0 1 1 * ? *)` (1 AM ngày 1 mỗi tháng)
- Next

**Bước 3:** Target
- Target types: AWS service
- Select a target: Lambda function
- Function: `BudgetTracket-MonthlySummaryFunction-dev`
- Create rule

### 8.4 NotificationFunction Lambda

```
// BudgetTracket.Lambda/Functions/NotificationFunction.cs
```

![Cài đặt NotificationFunction](/images/workshop/80.png)

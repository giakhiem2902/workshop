---
title: "Module 3: IAM, Infrastructure Foundation"
weight: 3
pre: "<b>5.3. </b>"
---

## Module 3: IAM, Infrastructure Foundation

**Member:** Chung

### 3.1 Create IAM Roles & Policies

**Step 1: Lambda Execution Role**

AWS Console → IAM → Roles → Create role

![Create role](/images/workshop/8.png)

- Select trusted entity: AWS service
- Use case: Lambda
- Click Lambda
- Next

![Select Lambda use case](/images/workshop/9.png)

**Step 2: Add Permissions**

Attach policies:
- `AWSLambdaBasicExecutionRole` (CloudWatch Logs)
- `AmazonDynamoDBFullAccess`
- `AmazonS3FullAccess`
- `AmazonSNSFullAccess`
- `AmazonSQSFullAccess`
- `SecretsManagerReadWrite`

Next → Role name: `BudgetTracketLambdaRole` → Create role

![Attach permissions policies](/images/workshop/10.png)
![Role created](/images/workshop/11.png)

- Copy ARN: `arn:aws:iam::<account-id>:role/BudgetTracketLambdaRole` (used in Module 5)

**Step 3: API Gateway Invocation Policy (Add inline policy)**

Policy editor: JSON

![Inline policy JSON editor](/images/workshop/12.png)

- Policy name: `LambdaApiGatewayInvoke`

### 3.2 Route 53 - DNS Setup

Route 53 no longer offers free custom domain registration. Instead of buying a domain + Route 53, we simply use the automatic CloudFront domain.

> Note: Left blank for now, revisit after the CloudFront distribution is created.

### 3.3 WAFv2 Setup

![WAFv2 setup](/images/workshop/13.png)
![WAFv2 web ACL](/images/workshop/14.png)

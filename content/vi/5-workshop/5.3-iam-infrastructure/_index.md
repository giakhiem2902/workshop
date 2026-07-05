---
title: "Module 3: IAM, Infrastructure Foundation"
weight: 3
pre: "<b>5.3. </b>"
---

## Module 3: IAM, Infrastructure Foundation

**Thành viên:** Chung

### 3.1 Create IAM Roles & Policies

**Bước 1: Lambda Execution Role**

AWS Console → IAM → Roles → Create role

![Create role](/images/workshop/8.png)

- Select trusted entity: AWS service
- Use case: Lambda
- Click Lambda
- Next

![Chọn use case Lambda](/images/workshop/9.png)

**Bước 2: Thêm Permissions**

Attach policies:
- `AWSLambdaBasicExecutionRole` (CloudWatch Logs)
- `AmazonDynamoDBFullAccess`
- `AmazonS3FullAccess`
- `AmazonSNSFullAccess`
- `AmazonSQSFullAccess`
- `SecretsManagerReadWrite`

Next → Role name: `BudgetTracketLambdaRole` → Create role

![Gắn permissions policies](/images/workshop/10.png)
![Role đã được tạo](/images/workshop/11.png)

- Copy ARN: `arn:aws:iam::<account-id>:role/BudgetTracketLambdaRole` (dùng cho Module 5)

**Bước 3: API Gateway Invocation Policy (Add inline policy)**

Policy editor: JSON

![Inline policy JSON editor](/images/workshop/12.png)

- Policy name: `LambdaApiGatewayInvoke`

### 3.2 Route 53 - DNS Setup

Hiện nay, Route 53 đã không còn tạo được domain riêng miễn phí. Thay vì mua domain + Route 53, chỉ cần dùng CloudFront domain tự động.

> Note: Tạm để trống, quay lại sau khi có CloudFront distribution.

### 3.3 WAFv2 Setup

![Thiết lập WAFv2](/images/workshop/13.png)
![Web ACL của WAFv2](/images/workshop/14.png)

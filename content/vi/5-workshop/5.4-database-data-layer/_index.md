---
title: "Module 4: Database & Data Layer"
weight: 4
pre: "<b>5.4. </b>"
---

## Module 4: Database & Data Layer

**Thành viên:** Khiêm

### 4.1 DynamoDB Table Creation

![Danh sách bảng DynamoDB](/images/workshop/15.png)

**Bước 1:** AWS Console → DynamoDB → Tables → Create table

![Create table](/images/workshop/16.png)

- Table name: `BudgetTracket-dev`
- Partition key (PK): `userId` (String) — Sort key (SK): `entityId` (String)
- Example items:
  - PK: `USER#user123`, SK: `PROFILE`
  - PK: `USER#user123`, SK: `TXN#2026-01-15#txn001`
  - PK: `USER#user123`, SK: `BUDGET#2026-01#Food`

**Bước 2:** Create table

![Table đã tạo](/images/workshop/17.png)

**Bước 3:** Wait for status = ACTIVE

```
# Verify via CLI
aws dynamodb describe-table --table-name BudgetTracket-dev --region ap-southeast-1
```

![Trạng thái table ACTIVE](/images/workshop/18.png)

### 4.2 DynamoDB Schema Details

Sample Items:

```json
{
  "userId": { "S": "user#abc123" },
  "entityId": { "S": "PROFILE" },
  "email": { "S": "user@example.com" },
  "name": { "S": "John Doe" },
  "currency": { "S": "VND" },
  "notifyBudgetAlert": { "BOOL": true },
  "notifyMonthlyReport": { "BOOL": true },
  "notifyAnomaly": { "BOOL": false },
  "createdAt": { "S": "2026-01-15T10:30:00Z" },
  "updatedAt": { "S": "2026-01-15T10:30:00Z" }
}
```

```json
{
  "userId": { "S": "user#abc123" },
  "entityId": { "S": "TXN#2026-01-15#txn001" },
  "type": { "S": "expense" },
  "description": { "S": "Lunch at Pho restaurant" },
  "amount": { "N": "150000" },
  "category": { "S": "food" },
  "date": { "S": "2026-01-15" },
  "note": { "S": "Business lunch" },
  "receiptUrl": { "S": "s3://bucket/receipts/txn001.jpg" }
}
```

### 4.3 S3 Buckets

![Tổng quan S3 buckets](/images/workshop/19.png)

**Bước 1:** AWS Console → S3 → Create bucket

![Create bucket](/images/workshop/20.png)

**Bucket 1: Frontend Hosting**
- Bucket name: `budget-tracket-frontend-dev` (phải globally unique)
- Region: `ap-southeast-1`
- Block all public access: Uncheck (cho CloudFront public access)
- Create bucket

![Bucket frontend đã tạo](/images/workshop/21.png)

**Bước 2:** Enable Static Website Hosting

![Bucket properties](/images/workshop/22.png)
![Cấu hình static website hosting](/images/workshop/23.png)
![Static website hosting đã bật](/images/workshop/24.png)

- Click vào bucket → Properties → Static website hosting → Edit
- Enable
- Index document: `index.html`
- Error document: `index.html` (cho React routing)
- Save

**Bucket 2: Receipt Storage**

![Bucket receipts](/images/workshop/25.png)

- Bucket name: `budget-tracket-receipts-dev`
- Region: `ap-southeast-1`
- Block all public access: Check (chỉ pre-signed URLs)
- Create bucket

**Bước 3:** Add lifecycle policy (xóa receipts cũ)

![Lifecycle rules](/images/workshop/26.png)

- Click vào bucket → Management → Lifecycle rules → Create lifecycle rule

![Create lifecycle rule](/images/workshop/27.png)

- Rule name: `DeleteOldReceipts`
- Apply to all objects
- Expiration: 180 days
- Create rule

### 4.4 Secrets Manager

![Tổng quan Secrets Manager](/images/workshop/28.png)

**Bước 1:** AWS Console → Secrets Manager → Store a new secret

![Store a new secret](/images/workshop/29.png)

**Secret 1: Gemini API Key**

![Key/value của secret](/images/workshop/30.png)

- Secret type: Other type of secret
- Key/value: `GEMINI_API_KEY` = `<your-gemini-api-key>`
- Secret name: `budget-tracket/gemini-api-key`
- Store secret
- Copy ARN (dùng cho Lambda environment)

**Secret 2: Cognito Config** (tạo sau Module 7)
- Key/value: `COGNITO_USER_POOL_ID: <pool-id>`, `COGNITO_CLIENT_ID: <client-id>`
- Secret name: `budget-tracket/cognito-config`

### 4.5 Verify via AWS CLI

Check DynamoDB table:

![Kiểm tra DynamoDB qua CLI](/images/workshop/31.png)

```
aws dynamodb list-tables --region ap-southeast-1
```

Check S3 buckets:

```
aws s3 ls
```

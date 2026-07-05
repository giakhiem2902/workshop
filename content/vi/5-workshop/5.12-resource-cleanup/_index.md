---
title: "Module 12: Resource Cleanup"
weight: 12
pre: "<b>5.12. </b>"
---

## Module 12: Resource Cleanup

**Người phụ trách:** Chung — **Thời gian:** 30 phút

### 12.1 Delete CloudFormation Stack

Delete SAM stack (deletes all AWS resources):

```
aws cloudformation delete-stack \
  --stack-name budget-tracket-dev \
  --region ap-southeast-1
```

Wait for deletion:

```
aws cloudformation wait stack-delete-complete \
  --stack-name budget-tracket-dev \
  --region ap-southeast-1
```

### 12.2 Manual Cleanup (if needed)

Delete S3 buckets:
```
aws s3 rb s3://budget-tracket-frontend-dev --force
aws s3 rb s3://budget-tracket-receipts-dev --force
```

Delete DynamoDB table:
```
aws dynamodb delete-table --table-name BudgetTracket-dev
```

Delete SNS topic:
```
aws sns delete-topic --topic-arn arn:aws:sns:ap-southeast-1:<account>:budget-tracket-notifications-dev
```

Delete SQS queue:
```
aws sqs delete-queue --queue-url https://sqs.ap-southeast-1.amazonaws.com/<account>/budget-tracket-notifications-dev
```

Delete CloudFront distribution:
```
aws cloudfront delete-distribution --id <DISTRIBUTION_ID>
```

Delete Route 53 hosted zone:
```
aws route53 delete-hosted-zone --id /hostedzone/<ZONE_ID>
```

Delete WAF:
```
aws wafv2 delete-web-acl --name BudgetTracketWAF --scope REGIONAL --region ap-southeast-1
```

### Checklist — Verification

After each module, run these checks:

- [x] Module 1: Team understands architecture
- [x] Module 2: All tools installed & AWS CLI configured
- [x] Module 3: IAM roles created & verified
- [x] Module 4: DynamoDB table active, S3 buckets created, Secrets stored
- [x] Module 5: API Gateway created, Lambda functions deployed
- [x] Module 6: Cognito User Pool active, React app builds & runs
- [x] Module 7: JWT validation working, CloudFront distribution created
- [x] Module 8: SNS/SQS/EventBridge running, notifications delivered
- [x] Module 9: Unit & E2E tests passing
- [x] Module 10: CloudWatch logs & alarms visible
- [x] Module 11: SAM deployment successful
- [x] Module 12: Cleanup confirmed

### Useful AWS CLI Commands

List all Lambda functions:

![Danh sách Lambda functions](/images/workshop/89.png)

List all DynamoDB tables:

![Danh sách DynamoDB tables](/images/workshop/90.png)

List API Gateway APIs:

![Danh sách API Gateway APIs](/images/workshop/91.png)

---

*Last Updated: 2026-07-05 — Workshop Status: Ready for implementation*

### References (Tài liệu tham khảo)

- AWS Serverless – AWS Documentation
- AWS Lambda – Giới thiệu
- Amazon API Gateway – Giới thiệu
- Amazon DynamoDB – Tổng quan
- Amazon Cognito – Giới thiệu
- Amazon CloudFront – Giới thiệu
- Amazon S3 – Giới thiệu
- Amazon Route 53 – Giới thiệu
- AWS WAF – Giới thiệu
- Amazon SNS – Giới thiệu
- Amazon SQS – Giới thiệu
- Amazon EventBridge – Giới thiệu
- Amazon CloudWatch – Giới thiệu
- AWS Secrets Manager – Giới thiệu
- DynamoDB Data Modeling – Single Table Design
- MDN HTTP Status Codes
- Auth0 – Phân biệt ID Token và Access Token
- OAuth Refresh Tokens
- AWS IAM Best Practices – Least Privilege
- Gemini API Developer Competition – FinanMe App
- Atlassian – Các loại kiểm thử phần mềm
- AWS Prescriptive Guidance – AWS SAM (IaC)
- AWS Compute Blog – Tối ưu chi phí serverless
- DynamoDB Global Tables – AWS Documentation

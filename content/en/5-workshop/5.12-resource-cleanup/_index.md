---
title: "Module 12: Resource Cleanup"
weight: 12
pre: "<b>5.12. </b>"
---

## Module 12: Resource Cleanup

**Owner:** Shared (Chung) — **Time:** 30 minutes

### 12.1 Delete CloudFormation Stack

Delete the SAM stack (this deletes all AWS resources):

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

Delete the DynamoDB table:
```
aws dynamodb delete-table --table-name BudgetTracket-dev
```

Delete the SNS topic:
```
aws sns delete-topic --topic-arn arn:aws:sns:ap-southeast-1:<account>:budget-tracket-notifications-dev
```

Delete the SQS queue:
```
aws sqs delete-queue --queue-url https://sqs.ap-southeast-1.amazonaws.com/<account>/budget-tracket-notifications-dev
```

Delete the CloudFront distribution:
```
aws cloudfront delete-distribution --id <DISTRIBUTION_ID>
```

Delete the Route 53 hosted zone:
```
aws route53 delete-hosted-zone --id /hostedzone/<ZONE_ID>
```

Delete the WAF:
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

![List Lambda functions](/images/workshop/89.png)

List all DynamoDB tables:

![List DynamoDB tables](/images/workshop/90.png)

List API Gateway APIs:

![List API Gateway APIs](/images/workshop/91.png)

---

*Last Updated: 2026-07-05 — Workshop Status: Ready for implementation*

### References

- AWS Serverless – AWS Documentation
- AWS Lambda – Introduction
- Amazon API Gateway – Introduction
- Amazon DynamoDB – Overview
- Amazon Cognito – Introduction
- Amazon CloudFront – Introduction
- Amazon S3 – Introduction
- Amazon Route 53 – Introduction
- AWS WAF – Introduction
- Amazon SNS – Introduction
- Amazon SQS – Introduction
- Amazon EventBridge – Introduction
- Amazon CloudWatch – Introduction
- AWS Secrets Manager – Introduction
- DynamoDB Data Modeling – Single Table Design
- MDN HTTP Status Codes
- Auth0 – ID Token vs Access Token
- OAuth Refresh Tokens
- AWS IAM Best Practices – Least Privilege
- Gemini API Developer Competition – FinanMe App
- Atlassian – Types of software testing
- AWS Prescriptive Guidance – AWS SAM (IaC)
- AWS Compute Blog – Optimizing serverless costs
- DynamoDB Global Tables – AWS Documentation

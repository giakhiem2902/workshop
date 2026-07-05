---
title: "Module 1: Introduction"
weight: 1
pre: "<b>5.1. </b>"
---

## Budget Tracker Workshop — AWS Console Implementation Guide

### 1. Budget Tracker Overview

Budget Tracker is a personal finance management platform built on AWS Serverless (React + C# .NET 8 Lambda + DynamoDB), integrated with AI for transaction categorization and a financial-advice chatbot via the Google Gemini API (`gemini-2.5-flash`).

Request flow: React frontend → API Gateway (JWT via Cognito Authorizer) → Lambda business logic → DynamoDB/S3 for data storage, with a notification pipeline via SNS + SQS + EventBridge sending emails to users.

### Team Assignment — 4 Members, 1 Shared Account

| Member | Area | Workshop Sections |
|---|---|---|
| Chung | IAM + Route 53 + WAFv2 (Infrastructure Foundation) | 3 |
| Khiem | DynamoDB + Secrets Manager + S3 (Database & Data layer) + Cognito Auth & Edge | 4, 7 |
| Huy | API Gateway + Lambda Core (Transaction/Budget/Report) + Notifications (SNS/SQS/EventBridge) | 5, 8 |
| Cong | React Frontend + Cognito login flow + Gemini AI integration | 6 |

(Modules 1, 2, 9, 10 — Introduction, Prerequisites, Testing, Monitoring — were done together by the whole team.)

### 2. Production Flow

```
Client Browser
    ↓
CloudFront (WAF) → S3 (React static site)
    ↓
API Gateway (Cognito JWT Authorizer + WAF)
    ↓
AWS Lambda
    ├─ TransactionFunction / BudgetFunction / ReportFunction → DynamoDB
    ├─ ProfileFunction → DynamoDB (+ SNS subscribe for email)
    ├─ AiFunction → Google Gemini API (categorize / insights / chat)
    ├─ NotificationFunction (SQS-triggered) → SNS → User email
    └─ MonthlySummaryFunction (EventBridge cron, 1st/month) → SQS → SNS
    ↓
CloudWatch (logs, metrics, alarms on all functions)
```

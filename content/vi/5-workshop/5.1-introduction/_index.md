---
title: "Module 1: Introduction"
weight: 1
pre: "<b>5.1. </b>"
---

## Budget Tracker Workshop — AWS Console Implementation Guide

### 1. Tổng quan Budget Tracker

Budget Tracker là nền tảng quản lý tài chính cá nhân xây dựng trên AWS serverless (React + C# .NET 8 Lambda + DynamoDB), tích hợp AI phân loại giao dịch / chatbot tư vấn tài chính qua Google Gemini API (`gemini-2.5-flash`).

Request từ React frontend → API Gateway (JWT qua Cognito Authorizer) → Lambda xử lý nghiệp vụ → DynamoDB/S3 lưu dữ liệu, có pipeline thông báo qua SNS + SQS + EventBridge gửi email cho user.

### Phân công 4 thành viên — 1 account chung

| Thành viên | Khối | Mục workshop |
|---|---|---|
| Chung | IAM + Route 53 + WAFv2 (Infrastructure Foundation) | 3 |
| Khiêm | DynamoDB + Secrets Manager + S3 (Database & Data layer) + Cognito Auth & Edge | 4, 7 |
| Huy | API Gateway + Lambda Core (Transaction/Budget/Report) + Notifications (SNS/SQS/EventBridge) | 5, 8 |
| Công | React Frontend + Cognito login flow + Gemini AI integration | 6 |

(Modules 1, 2, 9, 10 — Introduction, Prerequisites, Testing, Monitoring — thực hiện chung cả nhóm)

### 2. Luồng production

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

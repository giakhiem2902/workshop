---
title: Workshop
weight: 5
pre: "<b>5. </b>"
chapter: true
---

### Chương 5

# Workshop

**Nhóm:** CCK

Budget Tracker — Hướng dẫn triển khai trên AWS Console. Các bước chi tiết mà nhóm đã thực hiện để xây dựng và triển khai ứng dụng Serverless Budget Tracker trên AWS.

**Website Budget Tracker:** [https://d3ja9nvtyjzo9o.cloudfront.net/](https://d3ja9nvtyjzo9o.cloudfront.net/)

## Phân công thành viên

| Thành viên | Khối phụ trách | Mục |
|---|---|---|
| Chung | IAM + Route 53 + WAFv2 (Infrastructure Foundation) | [5.3](/vi/5-workshop/5.3-iam-infrastructure/) |
| Khiêm | DynamoDB + Secrets Manager + S3 (Database & Data layer) + Cognito Auth & Edge | [5.4](/vi/5-workshop/5.4-database-data-layer/), [5.7](/vi/5-workshop/5.7-auth-edge-layer/) |
| Huy | API Gateway + Lambda Core (Transaction/Budget/Report) + Notifications (SNS/SQS/EventBridge) | [5.5](/vi/5-workshop/5.5-backend-lambda-api/), [5.8](/vi/5-workshop/5.8-notifications-pipeline/) |
| Công | React Frontend + Cognito login flow + Gemini AI integration | [5.6](/vi/5-workshop/5.6-frontend-auth-ai/) |

(Modules 1, 2, 9, 10, 11, 12 — Introduction, Prerequisites, Testing, Monitoring, Deployment, Cleanup — thực hiện chung cả nhóm)

## Nội dung

1. [Introduction](/vi/5-workshop/5.1-introduction/)
2. [Chuẩn bị chung](/vi/5-workshop/5.2-prerequisites/)
3. [Chung – Nền tảng IAM & VPC](/vi/5-workshop/5.3-iam-infrastructure/)
4. [Khiêm – Lớp dữ liệu & bí mật](/vi/5-workshop/5.4-database-data-layer/)
5. [Huy – Backend Core: Lambda & API](/vi/5-workshop/5.5-backend-lambda-api/)
6. [Công – Frontend, Auth & AI](/vi/5-workshop/5.6-frontend-auth-ai/)
7. [Khiêm – Xác thực & lớp Edge](/vi/5-workshop/5.7-auth-edge-layer/)
8. [Huy – Notifications Pipeline](/vi/5-workshop/5.8-notifications-pipeline/)
9. [Kiểm thử end-to-end](/vi/5-workshop/5.9-end-to-end-testing/)
10. [Giám sát & vận hành](/vi/5-workshop/5.10-monitoring-operations/)
11. [Triển khai](/vi/5-workshop/5.11-deployment/)
12. [Dọn dẹp tài nguyên](/vi/5-workshop/5.12-resource-cleanup/)

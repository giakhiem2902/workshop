---
title: "Proposal"
weight: 2
pre: "<b>2. </b>"
---

# Budget Tracker

## Personal Finance Management Web Application
### AI-Powered Expense Tracking & Financial Intelligence

Project Report — AWS Serverless + Google Gemini AI
Report date: 12/7/2026

## 1. Executive Summary

Budget Tracker is a personal finance management application designed to help users track income, spending, and budgets. The app integrates artificial intelligence through the Google Gemini API to automatically categorize transactions, analyze spending, and provide smart financial recommendations.

The platform is built on an AWS Serverless architecture, ensuring high scalability, low operating cost, and maximum reliability. The application provides:

- A real-time financial dashboard
- Transaction management with receipt upload
- Budget setup and tracking by category
- Spending reports with analytical charts
- An AI chatbot for financial advice and Q&A
- Smart email notifications (budget overruns, unusual spending)

## 2. Problem Statement

### 2.1 Current Problem

Users currently face many challenges managing personal finances:

- Manual expense entry is time-consuming
- Consistently categorizing transactions is difficult
- Lack of insight into spending habits
- No alert system when a budget is exceeded
- Hard to get personalized financial advice

### 2.2 Proposed Solution

Budget Tracker provides a comprehensive solution by:

- Automatically categorizing transactions with AI (Google Gemini)
- Displaying an intuitive dashboard with real-time data
- Automatically analyzing spending and detecting trends
- Sending alerts when spending exceeds the budget
- Providing a 24/7 AI chatbot for financial advice
- Running on AWS Serverless (low cost, high reliability)

### 2.3 Benefits & Value

Budget Tracker delivers concrete benefits:

- Saves 5-10 hours/month of manual data entry
- Improves financial discipline through automatic alerts
- Uncovers savings opportunities through spending analysis
- Helps reach financial goals faster with AI advice
- A friendly interface usable by everyone

**Cost & ROI:**

- Estimated development cost: $5,000 - $8,000 (one-time)
- Monthly operating cost: $50-100 USD (AWS + Gemini)
- ROI: as a commercial project (freemium model), payback within 6-12 months

## 3. Solution Architecture

Budget Tracker uses an AWS Serverless architecture integrated with the Google Gemini API, designed for scalability, cost optimization, and high reliability.

### 3.1 Technology Stack

| Component | Technology | Purpose |
|---|---|---|
| Frontend | ReactJS (JavaScript) + Tailwind CSS | Modern, responsive web interface |
| Backend | C# .NET 8 (ASP.NET Core) | Lambda functions handling business logic |
| Database | Amazon DynamoDB (NoSQL) | Stores user, transaction, and budget data |
| API Gateway | Amazon API Gateway (REST) | Routes requests to Lambda functions |
| Authentication | Amazon Cognito + JWT | Secure user authentication |
| Storage | Amazon S3 | Stores receipts and attachments |
| Queue | Amazon SQS | Asynchronous notification processing |
| AI | Google Gemini API | Transaction categorization, spending analysis, chatbot |
| Notifications | Amazon SNS | Sends email notifications to users |
| Monitoring | Amazon CloudWatch | Logging, metrics, alarms |
| CDN | Amazon CloudFront | Fast static-content delivery |
| DNS | Amazon Route 53 | Domain management |
| Security | AWS WAF | Protection against DDoS, SQL injection, XSS |

### 3.2 Architecture Flow

Users access the application through a web browser:

1. Route 53 resolves the domain name.
2. CloudFront delivers the React app (HTML, CSS, JS) from S3 (protected by AWS WAF).
3. The React app calls API Gateway (HTTPS REST) via Axios.
4. API Gateway routes the request to the C# .NET 8 Lambda functions.
5. Lambda handles the request: authenticates via Cognito, reads/writes DynamoDB, calls the Gemini API.
6. Asynchronous processing: Lambda sends a notification to SQS → SNS sends the email.
7. CloudWatch monitors logs and metrics.

### 3.3 Data Design (DynamoDB)

DynamoDB uses a single-table design with PK = `USER#<userId>`:

- **PROFILE**: user information and notification preferences
- **TXN#\<timestamp\>#\<id\>**: transactions (income/expense)
- **BUDGET#\<year-month\>#\<category\>**: budget by category
- **CHAT#\<timestamp\>#\<id\>**: AI chat history

### 3.4 Google Gemini AI Integration

Lambda calls the Gemini API directly (not through the AWS SDK) for 3 main tasks:

- **Auto-categorize**: suggests a category for a new transaction
- **Spending Analysis**: analyzes spending trends (natural language)
- **AI Chatbox**: real-time financial advice
- **Insights**: personalized savings suggestions

## 4. Technical Implementation

### 4.1 Development Phases

The project is divided into 4 main phases:

- **Phase 1: Research & Architecture Design** (2 weeks) — design the AWS architecture, choose the tech stack, create UI wireframes.
- **Phase 2: Setup & Infrastructure** (2 weeks) — configure AWS services (DynamoDB, S3, Lambda, Cognito), set up CI/CD.
- **Phase 3: Backend & Frontend Development** (6-8 weeks) — build Lambda handlers (C# .NET 8), React components, integrate the Gemini API.
- **Phase 4: Testing & Deployment** (3-4 weeks) — unit tests, integration tests, UAT, production deployment.

### 4.2 Detailed Technical Requirements

**Frontend (ReactJS)**
- JavaScript (no TypeScript), React Hooks, Context API / Zustand
- Tailwind CSS for a minimalist style
- Axios for HTTP requests
- Recharts for charts/reports

**Backend (C# .NET 8)**
- ASP.NET Core Web API running on AWS Lambda
- DynamoDB context (Document Model) for data access
- FluentValidation for input validation
- IHttpClientFactory for calling the Gemini API
- Dependency Injection & async/await

## 5. Timeline & Milestones

| Phase | Week | Main Content | Expected Result |
|---|---|---|---|
| Design | Week 1–2 | Architecture, wireframes, technology choices | Design document |
| Setup | Week 3–4 | AWS configuration, CI/CD, repo | Infrastructure ready |
| Backend (Phase 1) | Week 5–7 | Core Lambda handlers, DynamoDB | Working API endpoints |
| Frontend (Phase 1) | Week 5–7 | Dashboard, Transactions page | Basic React app |
| Backend (Phase 2) | Week 8–10 | Gemini integration, notifications | AI features working |
| Frontend (Phase 2) | Week 8–10 | Budgets, Reports, AI Chatbox | Complete UI |
| Testing | Week 11–12 | Unit tests, integration tests, UAT | 70%+ code coverage |
| Production Deploy | Week 13 | Production deployment, monitoring | App live |

**Key Milestones:**

- Week 2: Architecture design approved
- Week 4: AWS infrastructure ready
- Week 7: MVP (Minimum Viable Product) with core features
- Week 10: All AI features complete
- Week 13: Production deployment

## 6. Budget Estimation

### 6.1 Development Cost

| Item | Hours | Cost/Hour | Total |
|---|---|---|---|
| Backend (C# .NET 8) | 160 | $50 | $8,000 |
| Frontend (React + UI) | 120 | $45 | $5,400 |
| DevOps & Infrastructure | 40 | $55 | $2,200 |
| Testing & QA | 60 | $45 | $2,700 |
| Project Management | 30 | $60 | $1,800 |
| Documentation & Training | 20 | $40 | $800 |
| **TOTAL** | **430** | **-** | **$21,700** |

\* Assumption: US/EU team rates; may be adjusted for local rates.

### 6.2 Operating Cost (Monthly)

| AWS Service / Third-Party | Cost/Month | Parameters | Cost/Year |
|---|---|---|---|
| AWS Lambda | $5 | 50M invocations/month | $60 |
| DynamoDB | $8 | 10 GB storage, standard tier | $96 |
| S3 (Receipts Storage) | $2 | 50 GB/month | $24 |
| CloudFront (CDN) | $3 | 1 TB data transfer/month | $36 |
| API Gateway | $2 | 10M requests/month | $24 |
| CloudWatch Logs | $1 | 50 GB logs/month | $12 |
| Amazon Cognito | $0 | Free tier (50K MAU) | $0 |
| SNS Notifications | $1 | 10K emails/month | $12 |
| Google Gemini API | $20 | Pay-as-you-go (free tier available) | $240 |
| Route 53 + Others | $2 | DNS, monitoring | $24 |
| **TOTAL** | **$44** | **-** | **$528** |

\* AWS pricing based on the US Region (us-east-1); other regions may differ.

### 6.3 Cost & ROI Summary

| Item | Cost | Notes |
|---|---|---|
| Initial development | $21,700 | One-time (13 weeks) |
| Operating/month | $44 | AWS + Gemini (average) |
| Operating/year | $528 | From year 2 onward |
| Year 1 total | $22,228 | Development + operations |
| Year 2+ total | $528/year | Operations only (post-payback) |
| Break-even (freemium) | 6–12 months | If 1% of users convert → $500/month |

**ROI Strategy:**

- Freemium model: free tier for 2 users, $3-5/month for Pro
- If 1,000 Pro users are reached: $3,000-5,000/month → development payback in 5-7 months
- If run as an internal project: cap operating cost at $44/month

## 7. Risk Assessment

### 7.1 Risk Matrix

| Risk | Description | Impact | Probability | Severity |
|---|---|---|---|---|
| Timeline overrun | Development slower than planned | High | Medium | High |
| Budget overrun | Development cost exceeds $21.7K | High | Low | Medium |
| Gemini AI errors | Transactions miscategorized | Medium | Medium | High |
| Security breach | User data leaked | Very high | Low | Very high |
| Scaling issues | DynamoDB throughput insufficient | High | Low | Medium |
| Competition | Better similar apps exist | Medium | High | High |
| Gemini pricing change | Google raises API pricing | Medium | Medium | Medium |

### 7.2 Mitigation Strategies

**Risk: Timeline Overrun**
- 2-week Agile sprints, daily standups
- 15% time buffer built into the plan
- Prioritize MVP first, add features later

**Risk: Gemini AI Errors**
- Allow users to edit the suggested category
- Set a confidence score, manual review if <70%
- Fall back to a default "other" category on error

**Risk: Security Breach**
- AWS WAF protects against DDoS, SQL injection, XSS
- Cognito handles authentication and JWT tokens
- Data encryption (TLS in-transit, encryption at-rest)
- Periodic security testing (penetration testing)

**Risk: Scaling Issues**
- Start with DynamoDB on-demand (auto-scaling)
- Add a GSI (Global Secondary Index) if complex queries are needed
- Use CloudFront caching to reduce API load

## 8. Expected Outcomes

### 8.1 Technical Improvements

- **Automated Transaction Categorization**: users no longer enter categories manually; Gemini suggests them with 95% accuracy.
- **Real-Time Dashboard**: balance, spending, and budget update instantly (latency < 2 seconds).
- **Smart Analysis**: Gemini analyzes spending trends and provides savings advice.
- **24/7 AI Chatbot**: users get instant financial advice via the AI chatbox.

### 8.2 Long-Term Value

- **Scalable Platform**: the Serverless architecture allows scaling to millions of users.
- **Rich Data & Insights**: collects (anonymized) user financial data for analysis.
- **Flexible Business Model**: can grow into a freemium SaaS or B2B (banking, fintech) product.

### 8.3 Success Criteria

- Dashboard runs stably with load time < 2 seconds.
- AI features (categorize, chat, insights) work with ≥95% accuracy.
- Notifications delivered successfully by email (SNS delivery rate ≥99%).
- All API endpoints reach 99.9% uptime.
- 70%+ code coverage (unit + integration tests).
- Operating cost ≤ $50/month (3-4 active users).

## Conclusion

Budget Tracker is a modern personal finance management application that uses an AWS Serverless architecture and Gemini AI to automate and optimize the user experience. With a moderate development cost (~$21.7K) and low operating cost (~$44/month), the project has the potential to become a successful SaaS product.

The architecture is designed to be scalable, adaptable, and secure. The project will help users improve their financial discipline, uncover savings opportunities, and reach financial goals faster.

With a clear 13-week roadmap and the right team and resources, Budget Tracker can be ready for users within 3 months.

---

*Date: 12/7/2026*

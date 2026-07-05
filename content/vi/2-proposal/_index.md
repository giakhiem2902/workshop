---
title: "Proposal"
weight: 2
pre: "<b>2. </b>"
---

# Budget Tracker

## Personal Finance Management Web Application
### AI-Powered Expense Tracking & Financial Intelligence

Báo cáo Dự Án — AWS Serverless + Google Gemini AI
Ngày lập báo cáo: 12/7/2026

## 1. Tóm tắt điều hành

Budget Tracker là một ứng dụng quản lý tài chính cá nhân được thiết kế để giúp người dùng theo dõi thu nhập, chi tiêu và ngân sách. Ứng dụng tích hợp trí tuệ nhân tạo (AI) qua Google Gemini API để tự động phân loại giao dịch, phân tích chi tiêu và đưa ra gợi ý tài chính thông minh.

Nền tảng được xây dựng trên kiến trúc AWS Serverless, đảm bảo tính mở rộng cao, chi phí vận hành thấp và độ tin cậy tối đa. Ứng dụng cung cấp:

- Dashboard theo dõi tài chính thời gian thực
- Quản lý giao dịch với tính năng upload hóa đơn
- Thiết lập và theo dõi ngân sách theo danh mục
- Báo cáo chi tiêu với biểu đồ phân tích
- Chatbot AI để tư vấn tài chính và trả lời câu hỏi
- Thông báo thông minh qua email (vượt ngân sách, chi tiêu bất thường)

## 2. Tuyên bố vấn đề

### 2.1 Vấn Đề Hiện Tại

Người dùng hiện tại gặp nhiều thách thức khi quản lý tài chính cá nhân:

- Phải nhập dữ liệu chi tiêu thủ công, tốn thời gian
- Khó phân loại giao dịch một cách nhất quán
- Thiếu cái nhìn sâu sắc về các thói quen chi tiêu
- Không có hệ thống cảnh báo khi vượt ngân sách
- Khó nhận được lời khuyên tài chính được cá nhân hóa

### 2.2 Giải Pháp Đề Xuất

Budget Tracker cung cấp giải pháp toàn diện bằng cách:

- Tự động phân loại giao dịch bằng AI (Google Gemini)
- Hiển thị dashboard trực quan với dữ liệu thời gian thực
- Phân tích chi tiêu tự động và phát hiện xu hướng
- Gửi cảnh báo khi chi tiêu vượt ngân sách
- Cung cấp chatbot AI tư vấn tài chính 24/7
- Hoạt động trên AWS Serverless (chi phí thấp, độ tin cậy cao)

### 2.3 Lợi Ích & Giá Trị

Budget Tracker mang lại các lợi ích thiết thực:

- Tiết kiệm 5-10 giờ/tháng nhập dữ liệu thủ công
- Cải thiện kỷ luật tài chính nhờ cảnh báo tự động
- Phát hiện cơ hội tiết kiệm qua phân tích chi tiêu
- Đạt mục tiêu tài chính nhanh hơn nhờ lời khuyên AI
- Giao diện thân thiện, dễ sử dụng cho mọi cấp độ

**Chi Phí & ROI:**

- Chi phí phát triển ước tính: $5.000 - $8.000 (một lần)
- Chi phí vận hành hàng tháng: $50-100 USD (AWS + Gemini)
- ROI: Nếu là dự án thương mại (freemium model), hoàn vốn trong 6-12 tháng

## 3. Kiến Trúc Giải Pháp

Budget Tracker sử dụng kiến trúc AWS Serverless với tích hợp Google Gemini API, được thiết kế cho khả năng mở rộng, chi phí tối ưu và độ tin cậy cao.

### 3.1 Stack Công Nghệ

| Thành Phần | Công Nghệ | Mục Đích |
|---|---|---|
| Frontend | ReactJS (JavaScript) + Tailwind CSS | Giao diện web hiện đại, responsive |
| Backend | C# .NET 8 (ASP.NET Core) | Lambda functions xử lý business logic |
| Database | Amazon DynamoDB (NoSQL) | Lưu trữ dữ liệu người dùng, giao dịch, ngân sách |
| API Gateway | Amazon API Gateway (REST) | Định tuyến request tới Lambda functions |
| Authentication | Amazon Cognito + JWT | Xác thực người dùng an toàn |
| Storage | Amazon S3 | Lưu trữ hóa đơn và tệp đính kèm |
| Queue | Amazon SQS | Xử lý bất đồng bộ thông báo |
| AI | Google Gemini API | Phân loại giao dịch, phân tích chi tiêu, chatbot |
| Notifications | Amazon SNS | Gửi email thông báo tới người dùng |
| Monitoring | Amazon CloudWatch | Logging, metrics, alarms |
| CDN | Amazon CloudFront | Phân phối nội dung tĩnh nhanh |
| DNS | Amazon Route 53 | Quản lý tên miền |
| Security | AWS WAF | Bảo vệ chống DDoS, SQL injection, XSS |

### 3.2 Quy Trình Kiến Trúc

Người dùng truy cập ứng dụng thông qua trình duyệt web:

1. Route 53 giải quyết tên miền
2. CloudFront phân phối React app (HTML, CSS, JS) từ S3 (có AWS WAF bảo vệ)
3. React app gọi API Gateway (HTTPS REST) qua Axios
4. API Gateway định tuyến tới Lambda C# .NET 8
5. Lambda xử lý request: xác thực qua Cognito, đọc/ghi DynamoDB, gọi Gemini API
6. Xử lý bất đồng bộ: Lambda gửi thông báo vào SQS → SNS gửi email
7. CloudWatch theo dõi logs và metrics

### 3.3 Thiết Kế Dữ Liệu (DynamoDB)

DynamoDB sử dụng single table design với PK = `USER#<userId>`:

- **PROFILE**: Thông tin người dùng, tùy chọn thông báo
- **TXN#\<timestamp\>#\<id\>**: Giao dịch (thu nhập/chi tiêu)
- **BUDGET#\<year-month\>#\<category\>**: Ngân sách theo danh mục
- **CHAT#\<timestamp\>#\<id\>**: Lịch sử chat với AI

### 3.4 Tích Hợp Google Gemini AI

Lambda gọi Gemini API trực tiếp (không qua AWS SDK) với 3 tác vụ chính:

- **Auto-categorize**: Gợi ý danh mục cho giao dịch mới
- **Spending Analysis**: Phân tích xu hướng chi tiêu (ngôn ngữ tự nhiên)
- **AI Chatbox**: Tư vấn tài chính thời gian thực
- **Insights**: Gợi ý tiết kiệm cá nhân hóa

## 4. Triển Khai Kỹ Thuật

### 4.1 Các Giai Đoạn Phát Triển

Dự án được chia thành 4 giai đoạn chính:

- **Giai Đoạn 1: Nghiên Cứu & Thiết Kế Kiến Trúc** (2 tuần) — Thiết kế kiến trúc AWS, chọn tech stack, tạo wireframe giao diện.
- **Giai Đoạn 2: Setup & Cơ Sở Hạ Tầng** (2 tuần) — Cấu hình AWS services (DynamoDB, S3, Lambda, Cognito), thiết lập CI/CD.
- **Giai Đoạn 3: Phát Triển Backend & Frontend** (6-8 tuần) — Xây dựng Lambda handlers (C# .NET 8), React components, tích hợp Gemini API.
- **Giai Đoạn 4: Kiểm Thử & Triển Khai** (3-4 tuần) — Unit tests, integration tests, UAT, triển khai production.

### 4.2 Yêu Cầu Kỹ Thuật Chi Tiết

**Frontend (ReactJS)**
- JavaScript (không TypeScript), React Hooks, Context API / Zustand
- Tailwind CSS cho styling minimalist
- Axios cho HTTP requests
- Recharts cho biểu đồ/báo cáo

**Backend (C# .NET 8)**
- ASP.NET Core Web API trên AWS Lambda
- DynamoDB context (Document Model) cho data access
- FluentValidation cho input validation
- IHttpClientFactory cho gọi Gemini API
- Dependency Injection & Async/await

## 5. Lộ Trình & Mốc Triển Khai

| Giai Đoạn | Tuần | Nội Dung Chính | Kết Quả Mong Đợi |
|---|---|---|---|
| Thiết Kế | Tuần 1–2 | Kiến trúc, wireframe, lựa chọn công nghệ | Design document |
| Setup | Tuần 3–4 | Cấu hình AWS, CI/CD, repo | Hạ tầng sẵn sàng |
| Backend (Giai Đoạn 1) | Tuần 5–7 | Lambda handlers cơ bản, DynamoDB | API endpoints hoạt động |
| Frontend (Giai Đoạn 1) | Tuần 5–7 | Dashboard, Transactions page | React app cơ bản |
| Backend (Giai Đoạn 2) | Tuần 8–10 | Gemini integration, notifications | AI features hoạt động |
| Frontend (Giai Đoạn 2) | Tuần 8–10 | Budgets, Reports, AI Chatbox | UI hoàn chỉnh |
| Testing | Tuần 11–12 | Unit tests, integration tests, UAT | 70%+ code coverage |
| Production Deploy | Tuần 13 | Triển khai production, monitoring | App live |

**Các Mốc Quan Trọng:**

- Tuần 2: Phê duyệt thiết kế kiến trúc
- Tuần 4: Hạ tầng AWS sẵn sàng
- Tuần 7: MVP (Minimum Viable Product) với tính năng cơ bản
- Tuần 10: Toàn bộ tính năng AI hoàn thiện
- Tuần 13: Triển khai production

## 6. Ước Tính Ngân Sách

### 6.1 Chi Phí Phát Triển

| Khoản Mục | Giờ Công | Chi Phí/Giờ | Tổng Cộng |
|---|---|---|---|
| Backend (C# .NET 8) | 160 | $50 | $8.000 |
| Frontend (React + UI) | 120 | $45 | $5.400 |
| DevOps & Infrastructure | 40 | $55 | $2.200 |
| Testing & QA | 60 | $45 | $2.700 |
| Project Management | 30 | $60 | $1.800 |
| Documentation & Training | 20 | $40 | $800 |
| **TỔNG CỘNG** | **430** | **-** | **$21.700** |

\* Giả định: đội ngũ US/EU rates; có thể điều chỉnh theo địa phương

### 6.2 Chi Phí Vận Hành (Hàng Tháng)

| Dịch Vụ AWS / Bên Thứ Ba | Chi Phí/Tháng | Thông Số | Chi Phí/Năm |
|---|---|---|---|
| AWS Lambda | $5 | 50M invocations/tháng | $60 |
| DynamoDB | $8 | 10 GB lưu trữ, standard tier | $96 |
| S3 (Receipts Storage) | $2 | 50 GB/tháng | $24 |
| CloudFront (CDN) | $3 | 1 TB data transfer/tháng | $36 |
| API Gateway | $2 | 10M requests/tháng | $24 |
| CloudWatch Logs | $1 | 50 GB logs/tháng | $12 |
| Amazon Cognito | $0 | Free tier (50K MAU) | $0 |
| SNS Notifications | $1 | 10K emails/tháng | $12 |
| Google Gemini API | $20 | Pay-as-you-go (free tier có sẵn) | $240 |
| Route 53 + Others | $2 | DNS, monitoring | $24 |
| **TỔNG CỘNG** | **$44** | **-** | **$528** |

\* Giá AWS theo US Region (us-east-1); các region khác có thể khác

### 6.3 Tóm Tắt Chi Phí & ROI

| Khoản Mục | Chi Phí | Ghi Chú |
|---|---|---|
| Phát triển ban đầu | $21.700 | Một lần (13 tuần) |
| Vận hành/tháng | $44 | AWS + Gemini (trung bình) |
| Vận hành/năm | $528 | Đầu năm thứ 2 trở đi |
| Tổng năm 1 | $22.228 | Phát triển + vận hành |
| Tổng năm 2+ | $528/năm | Chỉ vận hành (hoàn vốn) |
| Break-even (freemium) | 6–12 tháng | Nếu 1% users convert → $500/tháng |

**Chiến Lược ROI:**

- Model freemium: free tier cho 2 người dùng, $3-5/tháng cho Pro
- Nếu đạt 1.000 Pro users: $3.000-5.000/tháng → hoàn vốn phát triển trong 5-7 tháng
- Nếu là dự án nội bộ: khống chế chi phí vận hành $44/tháng

## 7. Đánh Giá Rủi Ro

### 7.1 Ma Trận Rủi Ro

| Rủi Ro | Mô Tả | Ảnh Hưởng | Xác Suất | Mức Độ |
|---|---|---|---|---|
| Vượt Timeline | Phát triển chậm hơn kế hoạch | Cao | Trung bình | Cao |
| Vượt Ngân Sách | Chi phí phát triển vượt $21.7K | Cao | Thấp | Trung bình |
| Lỗi AI Gemini | Phân loại sai giao dịch | Trung bình | Trung bình | Cao |
| Lỗi Bảo Mật | Lọt dữ liệu người dùng | Cực cao | Thấp | Cực cao |
| Vấn Đề Scaling | DynamoDB không đủ throughput | Cao | Thấp | Trung bình |
| Sự Cạnh Tranh | Có ứng dụng tương tự tốt hơn | Trung bình | Cao | Cao |
| Thay Đổi Giá Gemini | Google tăng giá API | Trung bình | Trung bình | Trung bình |

### 7.2 Chiến Lược Giảm Thiểu Rủi Ro

**Rủi Ro: Vượt Timeline**
- Agile sprint 2 tuần, standup hàng ngày
- Lập kế hoạch dự phòng 15% thời gian
- Ưu tiên MVP trước, thêm tính năng sau

**Rủi Ro: Lỗi AI Gemini**
- Cho phép người dùng chỉnh sửa category được gợi ý
- Thiết lập confidence score, manual review nếu <70%
- Fallback về danh mục mặc định "other" nếu lỗi

**Rủi Ro: Lỗi Bảo Mật**
- AWS WAF bảo vệ DDoS, SQL injection, XSS
- Cognito xử lý authentication, JWT tokens
- Mã hóa dữ liệu (TLS in-transit, encryption at-rest)
- Kiểm tra bảo mật định kỳ (penetration testing)

**Rủi Ro: Vấn Đề Scaling**
- Bắt đầu DynamoDB on-demand (tự scale)
- Thêm GSI (Global Secondary Index) nếu cần tìm kiếm phức tạp
- CloudFront cache để giảm tải API

## 8. Kỳ Vọng & Kết Quả

### 8.1 Cải Tiến Kỹ Thuật

- **Tự Động Hóa Phân Loại Giao Dịch**: Người dùng không cần nhập danh mục thủ công, Gemini gợi ý 95% chính xác.
- **Dashboard Thời Gian Thực**: Cập nhật số dư, chi tiêu, ngân sách tức thì (latency < 2 giây).
- **Phân Tích Thông Minh**: Gemini phân tích xu hướng chi tiêu và đưa ra lời khuyên tiết kiệm.
- **Chatbot AI 24/7**: Người dùng được tư vấn tài chính tức thì qua AI chatbox.

### 8.2 Giá Trị Dài Hạn

- **Nền Tảng Mở Rộng**: Kiến trúc Serverless cho phép mở rộng tới hàng triệu người dùng.
- **Dữ Liệu & Insights Mạnh Mẽ**: Thu thập dữ liệu tài chính của người dùng để phân tích (anonymized).
- **Model Kinh Doanh Flexible**: Có thể phát triển thành freemium SaaS hoặc B2B (ngân hàng, fintech).

### 8.3 Tiêu Chí Thành Công

- Dashboard hoạt động ổn định, load time < 2 giây.
- Tính năng AI (categorize, chat, insights) hoạt động chính xác ≥95%.
- Thông báo gửi thành công tới email (SNS delivery rate ≥99%).
- Tất cả API endpoints đạt 99.9% uptime.
- 70%+ code coverage (unit + integration tests).
- Chi phí vận hành ≤ $50/tháng (3-4 người dùng hoạt động).

## Kết Luận

Budget Tracker là một ứng dụng quản lý tài chính hiện đại, sử dụng kiến trúc AWS Serverless và AI Gemini để tự động hóa và tối ưu hóa trải nghiệm người dùng. Với chi phí phát triển vừa phải (~$21.7K) và chi phí vận hành thấp (~$44/tháng), dự án có tiềm năng trở thành một sản phẩm SaaS thành công.

Kiến trúc được thiết kế để mở rộng, thích ứng và bảo mật. Dự án sẽ giúp người dùng cải thiện kỷ luật tài chính, phát hiện cơ hội tiết kiệm và đạt mục tiêu tài chính nhanh hơn.

Với lộ trình 13 tuần rõ ràng, đội ngũ và tài nguyên phù hợp, Budget Tracker có thể sẵn sàng cho người dùng trong 3 tháng.

---

*Ngày: 12/7/2026*

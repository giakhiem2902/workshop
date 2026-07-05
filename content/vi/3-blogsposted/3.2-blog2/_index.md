---
title: "Blog 2"
weight: 2
pre: "<b>3.2. </b>"
---

## Xây Dựng AI Agents Chuẩn Production Cho Tuân Thủ Tài Chính: Bài Học Từ Stripe

![Blog 2](/images/blog/blog2.png)

Case study chia sẻ cách Stripe ứng dụng thành công kiến trúc Multi-Agent (Đa đặc vụ) trên Amazon Bedrock để tự động hóa quy trình tuân thủ tài chính (như KYC, AML) trong môi trường thực tế (Production), nơi đòi hỏi độ chính xác tuyệt đối và bảo mật khắt khe.

**Các điểm chính cần nắm:**

- Áp dụng kiến trúc Multi-Agent (chia nhỏ thành Extraction Agent, Reasoning Agent, Decision & Routing) thay vì dùng một mô hình monolithic cồng kềnh, giúp tăng độ chính xác và dễ debug.
- Tích hợp kỹ thuật RAG để đối chiếu dữ liệu được trích xuất với các nguồn dữ liệu tin cậy và các quy tắc tuân thủ (Compliance Rules).
- Áp dụng cơ chế Human-in-the-loop (HITL) bắt buộc: AI tự động xử lý 80% khối lượng công việc rõ ràng, 20% các ca phức tạp được chuyển cho con người đánh giá nhằm giảm thiểu rủi ro "ảo giác" (hallucination).
- Đảm bảo tính riêng tư của dữ liệu nhạy cảm (PII), dữ liệu đầu vào/ra được mã hóa trong VPC và không chia sẻ cho bên thứ ba.

Kinh nghiệm từ Stripe là kim chỉ nam cho các kỹ sư Backend và Cloud Architect khi muốn xây dựng, mở rộng hệ thống AI đáp ứng tiêu chuẩn khắt khe của ngành Fintech mà không đánh đổi tính bảo mật.

Link: https://aws.amazon.com/vi/blogs/machine-learning/production-grade-ai-agents-for-financial-compliance-lessons-from-stripe/

**Hướng dẫn triển khai chi tiết:**

1. **Phân rã nghiệp vụ (Decompose)**: Tách luồng xử lý phức tạp thành các bước nhỏ. Thay vì viết 1 prompt dài, hãy tạo ra các Agent chuyên biệt: Agent A chuyên trích xuất text từ ảnh/PDF, Agent B chuyên đối chiếu luật.
2. **Xây dựng bộ điều phối (Orchestrator)**: Tại tầng Backend (sử dụng ASP.NET Core hoặc Spring Boot), viết logic điều phối luồng dữ liệu. Lấy kết quả (JSON) từ Agent A để làm đầu vào cho Agent B.
3. **Đánh giá độ tin cậy**: Yêu cầu Bedrock trả về một Confidence Score (điểm tin cậy) kèm theo câu trả lời.
4. **Thiết lập Human-in-the-loop (HITL)**: Viết logic kiểm tra: Nếu Confidence Score < 0.8 (ngưỡng tùy chỉnh), tự động đẩy dữ liệu đó vào một hàng đợi (như Amazon SQS).
5. **Giao diện xét duyệt**: Xây dựng một trang Dashboard để các chuyên gia (con người) vào pull dữ liệu từ SQS, đọc lý do tại sao AI phân vân và tự đưa ra quyết định cuối cùng.

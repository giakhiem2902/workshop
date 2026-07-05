---
title: "Blog 1"
weight: 1
pre: "<b>3.1. </b>"
---

## Đưa AIOps Vào Thực Tiễn: Xây Dựng Trợ Lý AI Tự Động Phân Tích AWS Health Cùng Amazon Bedrock

![Blog 1](/images/blog/blog1.png)

Bài viết giới thiệu kiến trúc đột phá ứng dụng Amazon Bedrock Agents kết hợp với AWS Health để tạo ra một hệ thống phân tích tình trạng hạ tầng tự phục vụ (Self-Service Analytics). Giải pháp này giúp chuyển hóa khối lượng log sự kiện khô khan thành các hành động khắc phục cụ thể, giải quyết triệt để bài toán "nhiễu cảnh báo" (alert fatigue).

**Các điểm chính cần nắm:**

- Hệ thống tự động thu thập sự kiện từ AWS Health qua EventBridge và lưu trữ tập trung tại Data Lake (S3 & Athena).
- Sử dụng Knowledge Base (Vector hóa qua OpenSearch) để tra cứu các tài liệu hướng dẫn xử lý sự cố (Runbooks/Playbooks) của doanh nghiệp.
- Amazon Bedrock Agents đóng vai trò điều phối, nhận câu hỏi bằng ngôn ngữ tự nhiên và chuyển hóa thành truy vấn SQL thông qua Action Groups.
- Áp dụng phương pháp RAG (Retrieval-Augmented Generation) để đưa ra câu trả lời chính xác kèm các bước khắc phục chi tiết.
- Dữ liệu được bảo mật hoàn toàn trong tài khoản AWS, không bị sử dụng để huấn luyện các mô hình nền tảng công cộng.

Tính năng và kiến trúc này đặc biệt hữu ích cho các đội ngũ DevOps/SRE trong việc rút ngắn thời gian xử lý sự cố (MTTR) và dân chủ hóa khả năng truy vấn dữ liệu hạ tầng cho mọi thành viên trong dự án.

Link: https://aws.amazon.com/vi/blogs/machine-learning/build-self-service-aws-health-analytics-to-find-actionable-health-insights-with-ai-agents-powered-by-amazon-bedrock/

**Hướng dẫn triển khai chi tiết:**

1. **Thiết lập luồng thu thập**: Tạo rule trên Amazon EventBridge để tự động capture các sự kiện từ AWS Health. Dùng AWS Lambda để parse dữ liệu thô này và lưu vào Amazon S3.
2. **Cấu hình truy vấn**: Thiết lập Amazon Athena để query trực tiếp lượng dữ liệu log vừa lưu trên S3.
3. **Tạo Knowledge Base**: Trên console của Amazon Bedrock, tạo một Knowledge Base và chỉ định nguồn dữ liệu là thư mục S3 chứa các tài liệu Runbook/Playbook nội bộ. Sử dụng Amazon OpenSearch Serverless làm database lưu trữ vector.
4. **Cấu hình Bedrock Agent**: Tạo Agent và định nghĩa các Action Groups. Liên kết Action Groups này với một hàm Lambda có nhiệm vụ thực thi các truy vấn SQL trên Athena.
5. **Tích hợp Frontend**: Dùng AWS SDK để gọi Bedrock Agent Runtime API, kết nối vào giao diện web (ví dụ: giao diện quản trị viết bằng ReactJS) để kỹ sư có thể chat trực tiếp với hệ thống.

---
title: "Blog 3"
weight: 3
pre: "<b>3.3. </b>"
---

## Đưa Trí Tuệ Nhân Tạo Lên Tầm Cao Mới: Claude Sonnet 5 Đã Có Mặt Trên AWS

![Blog 3](/images/blog/blog3.png)

Anthropic chính thức ra mắt Claude Sonnet 5 trên nền tảng Amazon Bedrock. Đây là mô hình AI lý tưởng mang lại sự cân bằng hoàn hảo giữa mức độ thông minh (tiệm cận bản Opus), tốc độ xử lý nhanh và tối ưu chi phí, thích hợp để vận hành ở quy mô lớn (scale).

**Các điểm chính cần nắm:**

- Cung cấp trí tuệ hàng đầu (top-tier intelligence) với khả năng lập trình, sinh code cực kỳ chính xác và hỗ trợ xây dựng tự động hóa hiệu quả.
- Là xương sống vững chắc cho các Autonomous Agents (Đặc vụ tự trị), có khả năng xử lý mượt mà các chuỗi phụ thuộc phức tạp và sử dụng công cụ đa bước (multi-step tool use).
- Vượt trội trong khả năng lập luận cấu trúc (Structured Reasoning), rất phù hợp cho các ngành yêu cầu làm báo cáo, phân tích dữ liệu hay tự động kiểm toán.
- Đảm bảo tính lưu trú dữ liệu (regional data residency) và tuân thủ các tiêu chuẩn bảo mật khắt khe của doanh nghiệp khi chạy trực tiếp trên hệ sinh thái AWS.

Sự ra mắt của Claude Sonnet 5 giúp các đội ngũ công nghệ dễ dàng triển khai các "siêu trợ lý" AI chuyên nghiệp, tự động hóa quy trình nội bộ mà không phải đắn đo về rào cản chi phí hay an toàn thông tin.

Link: https://aws.amazon.com/blogs/machine-learning/introducing-claude-sonnet-5-on-aws-anthropics-most-capable-sonnet-model/

**Hướng dẫn triển khai chi tiết:**

1. **Yêu cầu quyền truy cập**: Đăng nhập vào AWS Management Console, tìm dịch vụ Amazon Bedrock. Trình hướng dẫn bên trái, chọn Model access → Manage model access và tick chọn cấp quyền cho model Anthropic Claude Sonnet 5.
2. **Kiểm thử trên Playground**: Chuyển sang mục Playgrounds → Chat, chọn model Claude Sonnet 5. Bắt đầu thử nghiệm bằng cách đưa vào các yêu cầu thực tế để đo lường độ chính xác (ví dụ: yêu cầu mô hình sinh ra một file test case tự động bằng Cypress cho form đăng nhập, hoặc viết một cấu trúc Controller C# chuẩn RESTful).
3. **Tùy chỉnh tham số**: Tinh chỉnh các thông số như Temperature (độ sáng tạo) và Top P để output trả về đúng tính chất nghiệp vụ.
4. **Tích hợp vào code base**: Sử dụng AWS SDK, gọi API Converse hoặc InvokeModel của Bedrock. Truyền Model ARN của Claude Sonnet 5 và đoạn prompt vào payload để bắt đầu tự động hóa các tác vụ trực tiếp từ ứng dụng của bạn.

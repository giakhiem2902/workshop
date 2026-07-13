---
title: "Sự Kiện 3"
weight: 3
pre: "<b>4.3. </b>"
---

## AWS Meet Up – 11/07/2026

**Chủ đề:** Cloud Architecture, AWS Security, Monitoring & AWS Cloud Practitioner

### Mục Đích Của Sự Kiện

- Giúp sinh viên tiếp cận những kiến thức thực tế về thiết kế kiến trúc hệ thống trên nền tảng AWS.
- Chia sẻ các giải pháp ứng dụng AI trong bảo mật ứng dụng Web và quy trình DevSecOps.
- Trang bị kiến thức về Service Level Agreement (SLA), Monitoring và quản lý vận hành hệ thống Cloud.
- Hướng dẫn lộ trình học tập và chuẩn bị cho chứng chỉ AWS Certified Cloud Practitioner (CLF-C02).
- Tạo cơ hội giao lưu, học hỏi kinh nghiệm từ các chuyên gia và cộng đồng AWS Student Builder.

### Danh Sách Diễn Giả

- Thinh Nguyen – DevOps / DevSecOps / Cloud Engineer, Styl Solutions
- Nguyễn Huỳnh Sơn – Infrastructure Support Engineer, Endava
- Ngô Lê Tấn Huy – Speaker, AWS Certified Cloud Practitioner

### Nội Dung Nổi Bật

**1. Chung kết Cuộc thi Cloud Architect**

Mở đầu chương trình là vòng chung kết cuộc thi Cloud Architect, với sự tham gia của hai đội xuất sắc nhất là Team Ngũ Đại Hiệp và Team KLKAT.

Hai đội đã trình bày giải pháp kiến trúc hệ thống được xây dựng trên nền tảng AWS, phân tích cách lựa chọn các dịch vụ Cloud phù hợp với yêu cầu của bài toán, đồng thời trình bày phương án triển khai, khả năng mở rộng, tính sẵn sàng, bảo mật và tối ưu chi phí của hệ thống.

Bên cạnh phần trình bày, các đội còn trả lời nhiều câu hỏi từ ban giám khảo liên quan đến tư duy thiết kế kiến trúc, phương án xử lý các tình huống thực tế cũng như khả năng tối ưu hiệu năng và vận hành hệ thống trên AWS.

Sau quá trình đánh giá, Team KLKAT đã xuất sắc giành chức Quán quân của cuộc thi Cloud Architect.

Phần thi giúp em học hỏi thêm về quy trình thiết kế kiến trúc Cloud theo tiêu chuẩn AWS, cách lựa chọn dịch vụ phù hợp với từng bài toán và kỹ năng trình bày, bảo vệ giải pháp kỹ thuật trước hội đồng chuyên môn.

**2. Securing Your Web Apps With AWS Security Agent**

Diễn giả Thịnh Nguyễn đã giới thiệu AWS Security Agent, một giải pháp ứng dụng Generative AI nhằm hỗ trợ tự động hóa quy trình kiểm thử bảo mật cho các ứng dụng Web. Thay vì chỉ thực hiện các bài kiểm thử thủ công, AI Agent có khả năng tự động phân tích kiến trúc hệ thống, rà soát mã nguồn và thực hiện kiểm thử xâm nhập nhằm phát hiện các lỗ hổng bảo mật trong quá trình phát triển phần mềm.

Qua phần chia sẻ, em hiểu rõ hơn về:

- Những hạn chế của phương pháp kiểm thử bảo mật truyền thống như tốn nhiều thời gian, chi phí cao và phụ thuộc vào chuyên gia bảo mật.
- AWS Security Agent được xây dựng trên nền tảng Amazon Bedrock, có khả năng lập kế hoạch và tự động thực hiện các tác vụ bảo mật.
- Quy trình Design Review, Code Review và Automated Penetration Testing trong toàn bộ vòng đời phát triển phần mềm.
- Khả năng đánh giá kiến trúc theo các tiêu chuẩn PCI DSS, NIST CSF và AWS Well-Architected Framework.
- Tích hợp với GitHub và GitLab để tự động kiểm tra Pull Request, phát hiện lỗ hổng bảo mật và đề xuất bản vá phù hợp.
- Khả năng mô phỏng các chuỗi tấn công nhiều bước nhằm xác minh lỗ hổng thay vì chỉ đưa ra cảnh báo.
- Những hạn chế của AI Security Agent đối với các hệ thống sử dụng xác thực đa yếu tố (MFA), xác thực sinh trắc học hoặc các bài toán nghiệp vụ phức tạp.

Phần chia sẻ giúp em hiểu rõ hơn về xu hướng ứng dụng AI trong lĩnh vực DevSecOps, đồng thời nhận thấy vai trò quan trọng của tự động hóa trong việc nâng cao chất lượng và mức độ an toàn của các ứng dụng Web.

**3. SLA and Monitoring – From SLA to Monitoring: What Really Matters**

Diễn giả Nguyễn Huỳnh Sơn đã chia sẻ về vai trò của Service Level Agreement (SLA) và Monitoring trong việc đảm bảo chất lượng dịch vụ của các hệ thống Cloud hiện đại. Thông qua nhiều ví dụ thực tế, diễn giả nhấn mạnh rằng một hệ thống có hạ tầng hoạt động ổn định chưa đồng nghĩa với việc người dùng có trải nghiệm tốt. Điều quan trọng là cần theo dõi toàn bộ hành trình sử dụng dịch vụ thay vì chỉ giám sát CPU, Memory hoặc Network.

Qua phần trình bày, em hiểu rõ hơn về:

- Khái niệm Service Level Agreement (SLA) và vai trò của SLA trong việc đảm bảo chất lượng dịch vụ.
- Monitoring là một phần quan trọng trong quá trình quản lý rủi ro, giúp phát hiện sự cố trước khi ảnh hưởng đến người dùng.
- Mô hình Monitoring Pyramid, bao gồm Cloud Provider, Infrastructure, Application, Business Metrics và Customer Experience.
- Thông điệp "Healthy Infrastructure ≠ Healthy User Experience", nhấn mạnh rằng hạ tầng hoạt động bình thường nhưng người dùng vẫn có thể gặp lỗi khi sử dụng hệ thống.
- Cách sử dụng Amazon CloudWatch, CloudWatch Alarm và Amazon SNS để theo dõi hệ thống, thiết lập cảnh báo và hỗ trợ xử lý sự cố.
- Tầm quan trọng của việc theo dõi các chỉ số nghiệp vụ như Login Success Rate, tỷ lệ giao dịch thành công và trải nghiệm người dùng thay vì chỉ tập trung vào các chỉ số tài nguyên.

Thông qua phần chia sẻ này, em hiểu được tư duy xây dựng hệ thống Monitoring theo hướng lấy người dùng làm trung tâm, từ đó nâng cao khả năng vận hành và đảm bảo chất lượng dịch vụ.

**4. Inside the Exam – AWS Certified Cloud Practitioner**

Diễn giả Ngô Lê Tấn Huy đã giới thiệu tổng quan về chứng chỉ AWS Certified Cloud Practitioner (CLF-C02), đồng thời chia sẻ lộ trình học tập và kinh nghiệm ôn thi dành cho những người mới bắt đầu tìm hiểu về AWS Cloud.

Qua phiên chia sẻ, em học được:

- Cấu trúc bài thi gồm 65 câu hỏi trong 90 phút với bốn nhóm kiến thức chính: Cloud Concepts, Security and Compliance, Cloud Technology and Services, Billing, Pricing and Support.
- Sáu lợi ích nổi bật của AWS Cloud cùng các nguyên tắc thiết kế trong AWS Well-Architected Framework.
- Mô hình Shared Responsibility Model, giúp phân biệt trách nhiệm bảo mật giữa AWS và khách hàng.
- Kiến thức cơ bản về IAM, Security Groups, Network ACL, AWS WAF, AWS Shield và AWS Artifact.
- Vai trò của các dịch vụ cốt lõi như Amazon EC2, AWS Lambda, Amazon S3, Amazon RDS, Amazon DynamoDB, Amazon VPC và Amazon Route 53.
- Các mô hình tính phí của Amazon EC2, AWS Cost Explorer, AWS Budgets và các gói hỗ trợ của AWS.
- Kinh nghiệm học tập, luyện đề, thực hành trên AWS Free Tier và các mẹo làm bài thi nhằm đạt kết quả tốt.

Phiên chia sẻ giúp em có cái nhìn tổng quan về hệ sinh thái AWS, đồng thời định hướng rõ ràng hơn trong việc học tập và chuẩn bị cho chứng chỉ AWS Certified Cloud Practitioner.

### Những Gì Học Được

**Kiến Thức Về Cloud Architecture**
- Hiểu quy trình xây dựng kiến trúc hệ thống trên AWS.
- Biết cách lựa chọn các dịch vụ phù hợp với từng yêu cầu nghiệp vụ.
- Hiểu các tiêu chí đánh giá một kiến trúc Cloud như khả năng mở rộng, tính sẵn sàng, bảo mật và tối ưu chi phí.

**Kiến Thức Về Bảo Mật**
- Hiểu cách AI Agent hỗ trợ tự động hóa quy trình kiểm thử bảo mật.
- Nắm được quy trình Design Review, Code Review và Automated Pentesting.
- Biết cách ứng dụng Amazon Bedrock trong DevSecOps và Security Automation.

**Kiến Thức Về Monitoring**
- Hiểu vai trò của SLA trong quản lý hệ thống.
- Phân biệt Monitoring hạ tầng và Monitoring trải nghiệm người dùng.
- Biết cách sử dụng Amazon CloudWatch và Amazon SNS để giám sát và cảnh báo sự cố.

**Kiến Thức AWS**
- Hiểu cấu trúc chứng chỉ AWS Certified Cloud Practitioner.
- Nắm được các dịch vụ AWS cốt lõi và nguyên tắc thiết kế theo AWS Well-Architected Framework.
- Có thêm kinh nghiệm học tập và định hướng phát triển trong lĩnh vực Cloud Computing.

**Ứng Dụng Vào Công Việc**

Sau khi tham gia workshop, em định hướng áp dụng các kiến thức đã học vào quá trình học tập và phát triển dự án như:

- Áp dụng tư duy thiết kế kiến trúc Cloud để hoàn thiện các dự án triển khai trên AWS.
- Nghiên cứu tích hợp AI Security Agent nhằm hỗ trợ kiểm thử bảo mật cho các ứng dụng Web.
- Sử dụng Amazon CloudWatch và Amazon SNS để xây dựng hệ thống Monitoring và cảnh báo tự động.
- Áp dụng các nguyên tắc trong AWS Well-Architected Framework để tối ưu hiệu năng, bảo mật và chi phí của hệ thống.
- Tiếp tục học tập và thực hành nhằm chinh phục chứng chỉ AWS Certified Cloud Practitioner trong thời gian tới.

### Trải Nghiệm Trong Sự Kiện

Workshop mang đến cho em nhiều kiến thức thực tiễn về thiết kế kiến trúc hệ thống, bảo mật, Monitoring và các chứng chỉ AWS. Em đặc biệt ấn tượng với vòng chung kết cuộc thi Cloud Architect khi được quan sát cách các đội xây dựng và bảo vệ giải pháp kiến trúc trước hội đồng chuyên môn. Bên cạnh đó, phần chia sẻ về AWS Security Agent và Monitoring giúp em hiểu rõ hơn xu hướng ứng dụng AI trong DevSecOps cũng như cách xây dựng hệ thống giám sát dựa trên trải nghiệm người dùng.

Ngoài những kiến thức chuyên môn, sự kiện còn tạo cơ hội giao lưu với các chuyên gia và cộng đồng AWS Student Builder, giúp em mở rộng góc nhìn về định hướng nghề nghiệp trong lĩnh vực Cloud Computing và AI.

### Bài Học Rút Ra

- Thiết kế kiến trúc Cloud hiệu quả cần cân bằng giữa hiệu năng, bảo mật, khả năng mở rộng và chi phí vận hành.
- AI đang trở thành công cụ quan trọng trong việc tự động hóa kiểm thử bảo mật và hỗ trợ DevSecOps.
- Monitoring hiệu quả cần tập trung vào trải nghiệm người dùng thay vì chỉ theo dõi các chỉ số của hạ tầng.
- Việc nắm vững kiến thức nền tảng về AWS và chủ động thực hành là bước quan trọng để phát triển sự nghiệp trong lĩnh vực Cloud Computing.
- Tham gia các cuộc thi và workshop chuyên ngành không chỉ giúp nâng cao kiến thức chuyên môn mà còn rèn luyện tư duy giải quyết vấn đề, kỹ năng trình bày và khả năng làm việc trong môi trường thực tế.

### Hình Ảnh

![AWS Meet Up 11/07/2026 - ảnh 1](/images/event/event3/1.jpg)
![AWS Meet Up 11/07/2026 - ảnh 2](/images/event/event3/2.jpg)
![AWS Meet Up 11/07/2026 - ảnh 3](/images/event/event3/3.jpg)
![AWS Meet Up 11/07/2026 - ảnh 4](/images/event/event3/4.jpg)

---
title: "Blog 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---
# XÂY DỰNG TRỢ LÝ AI SERVERLESS TẠI PELAGO: TỪ Ý TƯỞNG ĐẾN CHĂM SÓC KHÁCH HÀNG TRONG VỎN VẸN 2 TUẦN
Trong ngành y tế kỹ thuật số, thách thức lớn nhất khi mở rộng quy mô là làm sao giữ được sự tương tác cá nhân hóa sâu sắc với bệnh nhân mà không gây quá tải cho đội ngũ chăm sóc y tế hay làm giảm chất lượng dịch vụ. Pelago – một phòng khám kỹ thuật số chuyên điều trị và hỗ trợ rối loạn sử dụng chất gây nghiện – đã giải quyết bài toán này bằng cách xây dựng một trợ lý AI hướng sự kiện (event-driven) trên nền tảng AWS chỉ trong vòng 2 tuần.

Tuy nhiên, trong lĩnh vực y tế, việc áp dụng Generative AI không chỉ đơn thuần là gọi một API của mô hình ngôn ngữ lớn (LLM). Đội ngũ kỹ thuật phải đối mặt với các thách thức khắt khe về bảo mật dữ liệu sức khỏe (PHI - Protected Health Information), yêu cầu giám sát con người (Human-in-the-loop) và độ trễ phản hồi khi xử lý lịch sử trò chuyện kéo dài nhiều tuần, thậm chí nhiều tháng.

Để vượt qua các rào cản này, Pelago đã tận dụng các dịch vụ Serverless và AI của AWS như Amazon Bedrock, AWS Lambda, Amazon DynamoDB, Amazon SNS/SQS để tạo nên một hệ thống trợ lý AI an toàn, tối ưu chi phí và triển khai với tốc độ kỷ lục.

## 1. NHỮNG ĐIỂM NỔI BẬT:
Kiến trúc hướng sự kiện (Event-Driven Architecture) & Xử lý bất đồng bộ: Thay vì để huấn luyện viên (coach) phải chờ đợi AI sinh phản hồi theo thời gian thực khi mở cuộc trò chuyện, hệ thống lắng nghe tin nhắn mới từ bệnh nhân và kích hoạt quy trình xử lý ngầm (asynchronous background processing). Ngay khi huấn luyện viên mở đoạn chat, các gợi ý phản hồi ngữ cảnh đã sẵn sàng.

Cơ chế con người kiểm soát (Human-In-The-Loop): Hệ thống không bao giờ gửi tin nhắn tự động trực tiếp cho bệnh nhân. AI chỉ đóng vai trò là "Trợ lý", tạo ra các gợi ý và phân tích ngữ cảnh (suggested considerations). Đội ngũ chăm sóc y tế sẽ đọc, đánh giá, điều chỉnh nội dung trước khi gửi đến người bệnh, đảm bảo độ an toàn lâm sàng tuyệt đối.

Bảo mật dữ liệu y tế nhạy cảm (PHI Compliance) trong VPC: Tất cả dữ liệu bệnh nhân và luồng xử lý AI đều vận hành hoàn toàn bên trong hạ tầng Amazon VPC của Pelago. Việc tích hợp với Amazon Bedrock được thực hiện an toàn, loại bỏ nguy cơ rò rỉ dữ liệu ra môi trường Internet công cộng và đáp ứng nghiêm ngặt các quy định bảo mật y tế.

Mở rộng linh hoạt & Tối ưu chi phí nhờ Serverless: Toàn bộ giải pháp sử dụng mô hình Serverless hoàn toàn (AWS Lambda, DynamoDB, SQS). Hệ thống tự động mở rộng quy mô khi lượng tin nhắn tăng đột biến và không phát sinh chi phí duy trì hạ tầng khi không có lượt truy cập (pay-per-use).

Rút ngắn thời gian đưa sản phẩm ra thị trường (Time-to-Market): Nhờ tận dụng các dịch vụ quản lý hoàn toàn (fully managed) của AWS, Pelago đã đưa hệ thống từ khâu khái niệm (concept) đến môi trường thực tế phục vụ bệnh nhân (care) chỉ trong vỏn vẹn 14 ngày.

## 2. TÌNH HUỐNG THỰC TẾ:
Một huấn luyện viên tại Pelago phải đồng thời quản lý và trò chuyện với hàng chục bệnh nhân đang trong quá trình điều trị. Mỗi tin nhắn gửi đi đòi hỏi huấn luyện viên phải nhớ lại toàn bộ lịch sử trao đổi, diễn biến tâm lý và tình trạng sức khỏe từ nhiều tuần trước đó. Việc tổng hợp thủ công này tốn rất nhiều thời gian.

Kiến trúc triển khai chuẩn Serverless & AI Assistant tại Pelago như sau:

*User Message Event → Amazon SNS / SQS → AWS Lambda (Context Orchestrator) → Amazon DynamoDB (Fetch History) → Amazon Bedrock (Generate Suggestions) → DynamoDB / Cache Store → Care Team Dashboard*
![Hình minh họa](/images/3-BlogsPosted/3.3-Blog3/blog3.png)

Trong kiến trúc này:
- **User Message Event & Queuing (SNS/SQS):** Khi bệnh nhân gửi tin nhắn, sự kiện lập tức được đẩy vào luồng hàng đợi để đảm bảo tính sẵn sàng cao và không làm thất lạc dữ liệu.

- **AWS Lambda:** Đóng vai trò là trung tâm điều phối (orchestrator). Lambda lấy lịch sử trò chuyện từ Amazon DynamoDB, xây dựng prompt chứa đầy đủ ngữ cảnh dài hạn và gửi yêu cầu tới Amazon Bedrock.

- **Amazon Bedrock:** Tiếp nhận prompt, sử dụng các mô hình nền tảng mạnh mẽ (như Anthropic Claude) để phân tích ý định, tình trạng bệnh nhân và đưa ra gợi ý câu trả lời tối ưu nhất.

- **Care Team Dashboard:** Khi huấn luyện viên mở ứng dụng, gợi ý từ AI đã được lưu trữ sẵn trong DynamoDB và hiển thị tức thì trên giao diện, giúp giảm thời gian soạn thảo tin nhắn từ vài phút xuống còn vài giây.
### 3. KẾT LUẬN:
Điều mình thấy ấn tượng ở giải pháp của Pelago là cách họ kết hợp khéo léo giữa Serverless và Generative AI để giải quyết một bài toán nghiệp vụ phức tạp trong thời gian cực ngắn. Thay vì tốn hàng tháng trời dựng server, quản lý cluster hay tự host các mô hình LLM phức tạp, họ tập trung hoàn toàn vào logic nghiệp vụ và trải nghiệm người dùng.

Việc thiết kế hệ thống theo hướng Event-driven kết hợp Human-in-the-loop không chỉ giải quyết triệt để bài toán độ trễ (latency) của LLM mà còn bảo đảm tính an toàn tuyệt đối – yếu tố sống còn trong ngành y tế.
Theo mình, đây là một bài học thực tế rất giá trị cho các Startup lẫn Doanh nghiệp lớn: Để triển khai AI thành công, không nhất thiết phải đầu tư hạ tầng quá cồng kềnh. Việc tận dụng tối đa các dịch vụ Serverless kết hợp với Amazon Bedrock có thể giúp doanh nghiệp hiện thực hóa các giải pháp AI đột phá chỉ trong vài tuần, vừa đảm bảo tính an toàn, vừa tối ưu chi phí vận hành.
## 4. Link tài liệu gốc:
https://aws.amazon.com/vi/blogs/architecture/building-a-serverless-ai-assistant-at-pelago-concept-to-care-in-two-weeks/


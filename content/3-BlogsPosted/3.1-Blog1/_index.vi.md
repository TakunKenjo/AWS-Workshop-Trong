---
title: "Blog 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# AMAZON BEDROCK CHẶN ĐỨNG CÁC CUỘC TẤN CÔNG PHISHING DO AI TẠO RA NHƯ THẾ NÀO?
## Giới thiệu

Social engineering thông qua tấn công lừa đảo (phishing) vẫn là một trong những kỹ thuật phổ biến nhất của tội phạm mạng. Tuy nhiên, sự xuất hiện của Generative AI đã nâng mối đe dọa này lên một tầm cao mới. Kẻ tấn công giờ đây kết hợp các mô hình ngôn ngữ lớn với dữ liệu khai thác công khai (OSINT) từ mạng xã hội để tạo ra hàng nghìn email lừa đảo độc bản, có tính cá nhân hóa sâu sắc và bắt chước hoàn hảo phong cách giao tiếp của đối tác. </br>

Trước đây, các bộ lọc an ninh truyền thống dựa trên mẫu từ khóa, kiểm tra lỗi chính tả hoặc phát hiện tên miền bất thường có thể dễ dàng chặn đứng email xấu. Nhưng khi AI có thể viết những bức thư chuẩn mực về ngữ pháp và bối cảnh, các dấu vết lừa đảo cũ hoàn toàn biến mất. Các tổ chức cần một giải pháp phòng thủ thông minh hơn, tập trung vào hành vi và ngữ cảnh thay vì chỉ quét bề mặt văn bản.
Trong bài viết này, hãy cùng khám phá cách xây dựng một hệ thống phát hiện phishing thế hệ mới được vận hành bởi Amazon Bedrock. Bài viết sẽ đi qua các bước trong pipeline phân tích đa tầng, các dịch vụ AWS hỗ trợ giải pháp và cách kiến trúc này bảo vệ hộp thư doanh nghiệp trước các kịch bản lừa đảo tinh vi nhất.


## Thách thức của AI Phishing
Các email lừa đảo do AI tạo ra hoạt động trong một môi trường đánh lừa tâm lý cực kỳ tinh vi. Chúng không còn chứa các câu chào chung chung hay các lỗi biên dịch ngớ ngẩn. Thay vào đó, chúng có thể trích dẫn chính xác một dự án đang triển khai của công ty, gọi đúng tên phòng ban, và đưa ra các yêu cầu nghe có vẻ hoàn toàn hợp lý trong bối cảnh công việc.</br>

Các công cụ lọc email truyền thống (lexical pattern-matching) dựa vào việc đối chiếu các dấu hiệu tĩnh như từ khóa nhạy cảm hoặc cấu trúc viết sai. Vì văn bản do AI tạo ra có độ mượt mà tự nhiên và không lặp lại cấu trúc của các mẫu phishing đã biết, chúng dễ dàng vượt qua các tường lửa bảo mật thông thường. Hệ thống phòng thủ hiện đại bắt buộc phải chuyển dịch sang phân tích các tín hiệu động: độ lệch chuẩn trong phong cách giao tiếp (communication style deviations) và tính hợp lý về ngữ cảnh của yêu cầu (contextual appropriateness).

## Tổng quan kiến trúc pipeline phân tích 5 bước trên Amazon Bedrock
Giải pháp phòng chống lừa đảo này sử dụng Amazon Bedrock để truy cập vào các foundation model tiên tiến, kết hợp với các công cụ kiểm soát an toàn tích hợp sẵn để phân tích email theo thời gian thực mà không làm lộ dữ liệu nhạy cảm. Quy trình xử lý bao gồm 5 bước cốt lõi:
- **Bước 1**: Bộ lọc đầu vào và tiền xử lý với Amazon Bedrock Guardrails Khi một email mới đến, trước khi đưa vào mô hình AI để phân tích sâu, nó phải đi qua Amazon Bedrock Guardrails. Lớp này đóng vai trò sàng lọc thô, phát hiện và ẩn đi các thông tin nhận dạng cá nhân nhạy cảm (PII) hoặc các nội dung độc hại rõ ràng, đảm bảo dữ liệu được chuẩn hóa một cách an toàn. </br>
- **Bước 2**: Xây dựng Prompt ngữ cảnh kết hợp Amazon Bedrock Knowledge Bases Hệ thống không đánh giá email một cách cô lập. Sử dụng Amazon Bedrock Knowledge Bases, pipeline sẽ trích xuất thông tin từ hồ sơ hành vi của người gửi (sender baseline tracker) và bối cảnh tổ chức để xây dựng một prompt phân tích toàn diện. Prompt này chứa cả nội dung email hiện tại, lịch sử tương tác trước đây của người gửi, và các ví dụ về phishing đã biết. </br>
- **Bước 3**: Phân tích bằng AI hiệu năng cao Mô hình nền tảng (ví dụ như Claude 3.5 Sonnet hoặc các phiên bản tương đương) trên Amazon Bedrock sẽ xử lý prompt đã được làm giàu ngữ cảnh. Trong quá trình này, các guardrails tiếp tục giám sát đầu ra của mô hình để ngăn chặn hiện tượng "ảo tưởng" (hallucination) và bảo vệ an toàn dữ liệu đầu ra theo đúng chính sách an toàn của doanh nghiệp. </br>
- **Bước 4**: Chấm điểm rủi ro đa yếu tố Sau khi phân tích, hệ thống sẽ tự động tính toán và đưa ra 3 loại điểm số thành phần bao gồm: điểm bất thường nội dung, điểm sai lệch hành vi người gửi, và điểm không phù hợp ngữ cảnh. Các điểm số này được tổng hợp thành một chỉ số rủi ro duy nhất trên thang điểm từ 0 đến 100. </br>
- **Bước 5**: Phân loại và định tuyến tự động Dựa trên điểm số rủi ro cuối cùng, hệ thống sẽ tự động đưa ra hành động:
  - Dưới 30 điểm (An toàn): Email được chuyển thẳng vào hộp thư đến của nhân viên.
  - Từ 30 đến dưới 70 điểm (Nghi ngờ): Email bị đưa vào khu vực cách ly (quarantine) để đội ngũ an ninh mạng kiểm tra thủ công.
  - Từ 70 điểm trở lên (Nguy hiểm): Email bị chặn đứng hoàn toàn (block) trước khi tiếp cận người dùng.
![Hình minh họa](/images/3-Blog/blog1.jpg)

## Đặc điểm triển khai và vận hành

Mô hình phòng thủ chủ động này mang lại khả năng vận hành linh hoạt và an toàn tuyệt đối cho doanh nghiệp:
- **Bảo mật dữ liệu nghiêm ngặt**: Nhờ có Amazon Bedrock Guardrails, các thông tin nhạy cảm được bảo vệ trong suốt quá trình suy luận (inference), đáp ứng các tiêu chuẩn khắt khe về responsible AI.
- **Khả năng mở rộng**: Pipeline xử lý hoạt động dựa trên cấu trúc API được quản lý hoàn toàn của Amazon Bedrock, cho phép hệ thống tự động mở rộng quy mô để quét hàng triệu email mỗi ngày mà không cần doanh nghiệp phải tự quản lý hay duy trì hạ tầng GPU phức tạp.

## Kết quả đo lường được
Việc ứng dụng giải pháp phân tích đa tầng bằng AI trên Amazon Bedrock mang lại những thay đổi mang tính bước ngoặt cho hệ thống an ninh doanh nghiệp:
- Rút ngắn thời gian phát hiện: Nhận diện chính xác các cuộc tấn công lừa đảo có chủ đích (spear-phishing) tinh vi ngay khi email vừa cập bến hệ thống.
- Giảm tỷ lệ báo động giả: Nhờ cơ chế đối chiếu với hồ sơ giao tiếp thực tế của người gửi, hệ thống hạn chế tối đa việc giữ lại các email công việc quan trọng của đối tác.
- Tối ưu hiệu suất đội ngũ SOC: Tự động hóa hoàn toàn các bước phân tích thô và phân loại, giúp các chuyên gia an ninh mạng tập trung xử lý các sự cố phức tạp thay vì phải đọc thủ công hàng nghìn email nghi ngờ mỗi ngày.

## Nhìn về phía trước
Cuộc chiến chống lừa đảo trên không gian mạng đang chuyển dịch thành cuộc đua công nghệ AI giữa kẻ tấn công và người phòng thủ. Bằng cách dịch chuyển trọng tâm từ kiểm tra từ ngữ bề mặt sang phân tích sâu về hành vi và ngữ cảnh giao tiếp, doanh nghiệp có thể chủ động đi trước các mối đe dọa một bước.
## Kết luận
Bài viết đã chỉ ra cách xây dựng hệ thống phát hiện email lừa đảo thế hệ mới sử dụng Amazon Bedrock phối hợp với Amazon Bedrock Guardrails và Knowledge Bases. Kiến trúc này mang lại khả năng phân tích ngữ cảnh mạnh mẽ, chấm điểm rủi ro chính xác và tự động hóa quy trình định tuyến email để bảo vệ tài sản số của doanh nghiệp.
Để tìm hiểu thêm về cách xây dựng ứng dụng an ninh mạng bằng AI, hãy truy cập AWS Architecture Center. Để bắt đầu với Amazon Bedrock, xem Getting started with Amazon Bedrock.

## Link bài viết
https://aws.amazon.com/vi/blogs/machine-learning/how-amazon-bedrock-catches-ai-generated-phishing/
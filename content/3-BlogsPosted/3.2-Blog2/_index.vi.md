---
title: "Blog 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---
# AMAZON BEDROCK BASELINE ARCHITECTURE IN AN AWS LANDING ZONE: KHUNG KIẾN TRÚC CHUẨN ĐỂ TRIỂN KHAI GENERATIVE AI AN TOÀN TRONG DOANH NGHIỆP
Khi các doanh nghiệp bắt đầu ứng dụng Generative AI (AI tạo sinh) vào quy trình vận hành, việc xây dựng các ứng dụng dựa trên các mô hình ngôn ngữ lớn (LLM) ngày càng trở nên phổ biến. Amazon Bedrock là dịch vụ hàng đầu được lựa chọn nhờ khả năng cung cấp các mô hình nền tảng mạnh mẽ thông qua một API duy nhất. </br>

Tuy nhiên, thách thức lớn nhất khi đưa Generative AI vào môi trường doanh nghiệp quy mô lớn chính là quản trị, chi phí và bảo mật.

Trong thực tế, các ứng dụng AI này thường có quyền truy cập vào các dữ liệu nội bộ nhạy cảm (như thông qua Knowledge Bases hoặc cơ chế RAG).

Nếu không có một kiến trúc mạng và phân quyền chặt xem xét từ đầu, doanh nghiệp sẽ phải đối mặt với nguy cơ rò rỉ dữ liệu, khó kiểm soát chi phí sử dụng mô hình AI của từng phòng ban và thiếu khả năng giám sát tập trung.

Để giải quyết bài toán này, AWS đề xuất mô hình Amazon Bedrock baseline architecture trong môi trường AWS Landing Zone. Giải pháp này giúp các tổ chức thiết lập các rào cản kiểm soát mạng, phân quyền truy cập tinh tế và quản lý tập trung các năng lực AI/ML một cách an toàn và tối ưu nhất.

Trong thực tế, kiến trúc này tận dụng sức mạnh của AWS Organizations, Amazon VPC Lattice, VPC Endpoints, AWS Identity and Access Management (IAM) và Amazon CloudWatch để tạo ra một hạ tầng kết nối an toàn đa tài khoản (multi-account) cho các ứng dụng Generative AI.
## NHỮNG ĐIỂM NỔI BẬT
- **Kiến trúc đa tài khoản an toàn (Multi-Account Setup):**
Phân chia hệ thống thành các tài khoản chuyên biệt (Service Network Account, Generative AI Account, Workload Accounts). Điều này giúp cô lập môi trường, giảm thiểu rủi ro lan rộng nếu một tài khoản bị tấn công và đơn giản hóa việc quản lý chi phí.
- **Kết nối bảo mật qua Amazon VPC Lattice:**
Sử dụng VPC Lattice để quản lý việc giao tiếp xuyên tài khoản giữa các ứng dụng và dịch vụ AI mà không cần phải thiết lập hạ tầng mạng phức tạp (như VPC Peering hay Transit Gateway quá chằng chịt). VPC Lattice cũng cho phép áp dụng các chính sách xác thực (auth policies) ở mức độ dịch vụ một cách nghiêm ngặt.
- **Ngăn chặn rò rỉ dữ liệu bằng VPC Endpoints:**
Đảm bảo toàn bộ lưu lượng truy cập từ ứng dụng đến Amazon Bedrock luôn đi qua mạng nội bộ của AWS bằng PrivateLink (VPC Interface Endpoints), loại bỏ hoàn toàn việc dữ liệu nhạy cảm phải đi ra ngoài Internet công cộng.
- **Phân quyền tinh tế (Fine-grained Access Control):**
Sử dụng kết hợp giữa IAM Policies và VPC Lattice Auth Policies để quy định chính xác đội ngũ nào hoặc ứng dụng nào được phép gọi các mô hình cụ thể (chẳng hạn giới hạn quyền truy cập các mô hình cao cấp, đắt tiền cho một vài nhóm kiểm thử nhất định).
- **Giám sát và kiểm toán tập trung:**
Tích hợp chặt chẽ với Amazon CloudWatch, AWS CloudTrail và VPC Lattice Access Logs nhằm ghi lại toàn bộ lịch sử tương tác với API của Bedrock, giúp theo dõi hiệu năng, phát hiện hành vi bất thường và phân bổ chi phí chuẩn xác.
## TÌNH HUỐNG THỰC TẾ
Giả sử một tập đoàn tài chính lớn muốn triển khai các trợ lý ảo AI (AI Agents) cho nhiều phòng ban (Dev, Test, Production) để phân tích các báo cáo nội bộ bảo mật, đồng thời cần kiểm soát chi phí sử dụng mô hình Amazon Bedrock tập trung.
Kiến trúc triển khai chuẩn hóa theo Landing Zone như sau:

- Workload Account (Môi trường Ứng dụng) → Service Network Account (VPC Lattice Service) → Generative AI Account (VPC Endpoints & Proxy Layer) → Amazon Bedrock

**Trong kiến trúc này:**

- **Workload Accounts:** Nơi chạy các ứng dụng client hoặc chatbot của từng phòng ban. Khi cần gọi AI, chúng gửi request đến mạng dịch vụ tập trung.
- **Service Network Account:** Đóng vai trò là trung tâm điều phối mạng của tổ chức. Tại đây, VPC Lattice kiểm tra các chính sách xác thực (Auth Policies) để xem request có hợp lệ hay không.
- **Generative AI Account:** Nơi quản lý tập trung các tài nguyên AI/ML. Tài khoản này tạo ra một lớp Proxy và kết nối trực tiếp tới Amazon Bedrock thông qua VPC Endpoints được bảo mật tuyệt đối.
- **Amazon Bedrock:** Tiếp nhận request từ endpoint nội bộ, xử lý bằng các mô hình nền tảng một cách an toàn và trả kết quả ngược lại.
- **CloudWatch & CloudTrail:** Theo dõi và ghi nhận log ở mọi công đoạn nhằm đảm bảo tính minh bạch và an toàn dữ liệu.
## KẾT LUẬN
Điều mình thấy ấn tượng ở kiến trúc Amazon Bedrock baseline này là cách AWS giải quyết bài toán đưa AI vào doanh nghiệp một cách có hệ thống. Thay vì để từng dự án tự ý kết nối tới Bedrock một cách manh mún, việc tập trung hóa năng lực Generative AI vào một tài khoản chuyên biệt mang lại sự nhất quán tối đa.

Trong kiến trúc này, việc đưa Amazon VPC Lattice vào làm "trọng tài" điều phối lưu lượng và xác thực là một bước đi rất thông minh, giúp giảm tải gánh nặng cấu hình mạng cho các kỹ sư Cloud và bảo mật.

Theo mình, đây là một mô hình kiến trúc bắt buộc phải tìm hiểu nếu bạn đang định hướng trở thành Cloud Architect hoặc Security Engineer làm việc với Generative AI trên AWS, vì nó giải quyết trực tiếp các vấn đề thực tế nhất của doanh nghiệp: Governance, Security, và Cost Optimization.

Thông qua bài blog này của AWS, chúng ta càng thấy rõ rằng: Phát triển một ứng dụng AI chạy được thì dễ, nhưng xây dựng một nền tảng AI an toàn, bền vững và tuân thủ các tiêu chuẩn doanh nghiệp lớn mới là thử thách thực sự.
## Link tài liệu
https://aws.amazon.com/vi/blogs/architecture/amazon-bedrock-baseline-architecture-in-an-aws-landing-zone/




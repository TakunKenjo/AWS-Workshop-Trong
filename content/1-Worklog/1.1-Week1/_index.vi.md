---
title: "Worklog Tuần 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---
### Mục tiêu tuần 1:

* Làm quen với môi trường thực tập và các thành viên FCJ.
* Tìm hiểu kiến thức nền tảng về AWS Cloud, các dịch vụ cốt lõi và công cụ quản lý AWS.
* Thực hành tạo tài khoản AWS, cấu hình MFA, quản lý chi phí với AWS Budget và triển khai các dịch vụ cơ bản.
* Tìm hiểu chuyên sâu về IAM, VPC, EC2 và thực hành xây dựng hạ tầng mạng an toàn trên AWS.
* Thảo luận nhóm, lựa chọn đề tài Smart Docs AI, nghiên cứu công nghệ ReactJS, Python và hệ sinh thái AWS để xây dựng dự án.
* Thiết kế, phát triển giao diện ban đầu của dự án, đẩy mã nguồn lên GitHub và làm quen với AWS Cloud9.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Làm quen với các thành viên FCJ <br> - Đọc và lưu ý các nội quy, quy định tại đơn vị thực tập <br> - Đọc quy định, yêu cầu về project <br> - Xem và xác định các nguồn tài liệu để học <br> - Xem video “First Cloud Journey Kick off 2024” <br> - Xem hướng dẫn vẽ kiến trúc AWS với Draw.io <br> - Xem hướng dẫn làm Workshop và thực hành: <br>&emsp; + Cài đặt Hugo <br>&emsp; + Hiểu cách triển khai kiến trúc file, tổ chức thư mục trong workshop <br>&emsp; + Biết cách sử dụng Markdown với VSCode <br> - Đọc hướng dẫn/yêu cầu về đồ án để biết cấu trúc báo cáo Workshop <br> - Tạo và khởi chạy được sườn báo cáo cho Workshop <br> - Điều chỉnh thông tin giới thiệu cá nhân | 22/06/2026 | 22/06/2026 | [FCAJ Kick off](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=1) <br><br> [Draw.io Guide](https://www.youtube.com/watch?v=l8isyDe-GwY&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=2) <br><br> [Workshop Guide](https://www.youtube.com/watch?v=mXRqgMr_97U&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=3) |
| 3 | - Tìm hiểu lý thuyết: <br>&emsp; + Khái niệm & lợi ích của điện toán đám mây <br>&emsp; + Triết lý AWS (điều tạo nên sự khác biệt của AWS) <br> - Tìm hiểu hạ tầng toàn cầu AWS (Data Center, Availability Zone - AZ, Region, Edge Locations) <br> - Tìm hiểu công cụ quản lý AWS Services (Root Login, IAM user login, Service search, Support Center, CLI, AWS SDK) <br> - Nắm tổng quan các nhóm dịch vụ AWS: Compute, Storage, Networking, Database,... <br> - **Thực hành:** Tạo mới tài khoản AWS Free Tier và thực hiện 5 nhiệm vụ nền tảng (Launch EC2 Instance, Amazon Bedrock Playground, Set up AWS Budgets, Create Lambda Web App, Create RDS Database) <br> - **Thực hành:** Cài đặt MFA bảo mật tài khoản <br> - **Thực hành:** Quản lý chi phí với AWS Budget (Tạo Budget theo template, Cost Budget, Usage Budget, tìm hiểu lý thuyết về RI & Saving Plans Budget) <br> - Tìm hiểu về AWS Support & Tiến hành dọn dẹp tài nguyên bài lab | 23/06/2026 | 23/06/2026 | [AWS Cloud Concepts](https://www.youtube.com/watch?v=HxYZAK1coOI&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=4) <br><br> [AWS Free Tier](https://000001.awsstudygroup.com/vi/) <br><br> [AWS Budgets](https://000007.awsstudygroup.com/vi/)<br><br> [AWS Support](https://000009.awsstudygroup.com/vi/)| 
| 4 | - Tìm hiểu lý thuyết: IAM Group, IAM User, IAM Policy, IAM Role <br> - **Thực hành AWS IAM:** Tạo IAM Group, IAM User, IAM Role, Operator User; thực hành chuyển đổi Role (Switch Role) và dọn dẹp tài nguyên IAM sau bài lab <br> - Tìm hiểu kiến trúc mạng: Amazon VPC, Subnet, Route Table, Internet Gateway, NAT Gateway, Security Group, Network ACLs, VPC Resource Map <br> - **Thực hành AWS VPC:** Xây dựng môi trường VPC, triển khai các thành phần mạng cơ bản và thiết lập cấu trúc mạng an toàn <br> - Tìm hiểu lý thuyết mở rộng: Triển khai Amazon EC2 Instances chuyên sâu và cấu hình Site to Site VPN | 24/06/2026 | 24/06/2026 | [AWS IAM](https://000002.awsstudygroup.com/vi/) <br><br> [Amazon VPC](https://000003.awsstudygroup.com/vi/)|
| 5 | - Thảo luận nhóm và quyết định chốt đề tài project <br> - Xem xét, đánh giá các dịch vụ công nghệ AWS sẽ áp dụng cho project <br> - Hệ thống và ôn tập lại kiến thức về ReactJS và Python <br> - Thiết kế bản mẫu giao diện (Mockup/Wireframe) ban đầu cho project “Smart Docs AI” | 25/06/2026 | 25/06/2026 |
| 6 | - Triển khai viết mã nguồn (Coding) giao diện cho dự án SmartDocsAI <br> - Quản lý mã nguồn và thực hiện push code lên kho lưu trữ GitHub | 26/06/2026 | 26/06/2026 | Kho lưu trữ GitHub dự án nhóm |
| 7 | - Tìm hiểu lý thuyết và thực hành cấu hình **AWS Cloud9** <br> - Khởi tạo Cloud9 instance, làm quen với môi trường Command Line và thao tác với file text trên cloud <br> - Thực hiện dọn dẹp, xóa tài nguyên Cloud9 instance sau khi hoàn thành để tối ưu chi phí | 27/06/2026 | 27/06/2026 | [AWS Cloud9](https://000049.awsstudygroup.com/vi/) |


### Kết quả đạt được tuần 1:

* Đã làm quen, kết nối hiệu quả và thiết lập quy trình làm việc chung với các thành viên trong nhóm First Cloud Journey (FCJ).
* Nắm vững kiến thức cơ bản về AWS Cloud, hiểu rõ các mô hình hạ tầng toàn cầu (Region, AZ) cũng như cách phân loại các nhóm dịch vụ cốt lõi.
* Hoàn thành việc đăng ký tài khoản AWS Free Tier, thiết lập bảo mật tối đa với MFA và cấu hình AWS Budget để kiểm soát rủi ro chi phí phát sinh.
* Hiểu sâu về cơ chế phân quyền của IAM (User, Group, Role, Policy) và thực hành xây dựng thành công một hạ tầng mạng VPC an toàn, khép kín.
* Hoàn thành việc lựa chọn đề tài dự án **Smart Docs AI**, thống nhất các mảng công nghệ cốt lõi (ReactJS, Python, AWS), hoàn thiện thiết kế giao diện sơ khởi và cấu trúc mã nguồn trên GitHub.
* Làm quen và sử dụng tốt môi trường lập trình đám mây AWS Cloud9 cũng như công cụ tạo tài liệu Hugo bằng Markdown.
* Biết cách quản lý chi phí AWS hiệu quả, tối ưu hóa các hạn mức của AWS Free Tier và định hình rõ ràng lộ trình học tập, nghiên cứu các dịch vụ nâng cao trong giai đoạn tiếp theo.
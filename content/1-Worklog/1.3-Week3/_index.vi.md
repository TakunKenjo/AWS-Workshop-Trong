---
title: "Worklog Tuần 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:

* Hoàn thiện và cải thiện giao diện người dùng (Frontend) của dự án Smart Docs AI, nâng cao trải nghiệm sử dụng thông qua việc bổ sung các chức năng cần thiết.
* Tìm hiểu quy trình CI/CD với AWS CodePipeline, Amazon S3 và GitHub để tự động hóa quá trình triển khai ứng dụng.
* Nghiên cứu các dịch vụ cốt lõi của AWS gồm Amazon CloudWatch, AWS Lambda và Amazon Cognito, từ đó hiểu được cách giám sát hệ thống, xử lý các tác vụ serverless và quản lý xác thực người dùng.
* Tìm hiểu cách tích hợp AWS Lambda với Amazon S3 và Amazon DynamoDB để xây dựng các ứng dụng serverless.
* Nâng cao kiến thức về kiến trúc triển khai AI trên AWS thông qua việc nghiên cứu và chia sẻ bài viết về Amazon Bedrock Baseline Architecture in an AWS Landing Zone.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Chỉnh sửa Code FE project Smart Docs AI: <br>&emsp; + Cho phép xóa tài liệu đã tải lên trước khi xử lý <br>&emsp; + Cập nhật trạng thái model hoạt động linh động (ban đầu là giá trị tĩnh - cố định) <br>&emsp; + Đóng/mở sidebar | 06/07/2026 | 06/07/2026 | |
| 3 | - Viết Blog thứ 2 và đăng lên nhóm AWS Study Group VN: *Amazon Bedrock baseline architecture in an AWS landing zone* | 07/07/2026 | 07/07/2026 | [Amazon Bedrock Baseline Architecture in an AWS Landing Zone](https://aws.amazon.com/vi/blogs/architecture/amazon-bedrock-baseline-architecture-in-an-aws-landing-zone/) |
| 4 & 5 | - Tìm hiểu AWS CodePipeline + AWS S3 Bucket + GitHub <br> - Code thêm giao diện project: <br>&emsp; + Login Form <br>&emsp; + Register Form <br>&emsp; + Xử lý Protected Route | 08/07/2026 | 09/07/2026 | [Deploy to Amazon S3 using AWS CodePipeline](https://docs.aws.amazon.com/codepipeline/latest/userguide/tutorials-s3deploy.html) |
| 6 | - Tìm hiểu về Amazon CloudWatch <br> - Tìm hiểu Lambda và CloudWatch | 10/07/2026 | 10/07/2026 | [Giới thiệu về Amazon EC2 Auto Scaling](https://000006.awsstudygroup.com/vi/) |
| 7 | - Tìm hiểu AWS Cognito <br> - Tìm hiểu Lambda tương tác với S3 và DynamoDB | 11/07/2026 | 11/07/2026 | [AWS Cognito](https://000081.awsstudygroup.com/vi/) <br> [Lambda tương tác với Amazon S3 và Amazon DynamoDB](https://000078.awsstudygroup.com/vi/) |

### Kết quả đạt được tuần 3:

* Hoàn thành các cải tiến giao diện cho dự án Smart Docs AI, bao gồm:
  * Thêm chức năng xóa tài liệu trước khi xử lý.
  * Cập nhật trạng thái hoạt động của AI model theo thời gian thực thay vì sử dụng dữ liệu tĩnh.
  * Bổ sung tính năng đóng/mở Sidebar giúp tối ưu không gian làm việc.
  * Xây dựng giao diện Login, Register và triển khai Protected Route để quản lý quyền truy cập.
* Nghiên cứu và nắm được quy trình triển khai website tĩnh lên Amazon S3 thông qua AWS CodePipeline kết hợp với GitHub, hiểu cách tự động hóa quá trình build và deploy.
* Viết và đăng thành công bài blog về Amazon Bedrock Baseline Architecture in an AWS Landing Zone lên nhóm AWS Study Group VN, góp phần củng cố kiến thức và chia sẻ với cộng đồng.
* Tìm hiểu cơ chế hoạt động của Amazon CloudWatch, biết cách thu thập log, theo dõi metric và giám sát tài nguyên AWS.
* Tìm hiểu mô hình AWS Lambda, hiểu cách xây dựng các hàm serverless và tích hợp với CloudWatch để theo dõi và ghi log.
* Nghiên cứu Amazon Cognito, nắm được quy trình xác thực, đăng ký, đăng nhập và quản lý người dùng trong ứng dụng.
* Tìm hiểu cách AWS Lambda tương tác với Amazon S3 và Amazon DynamoDB, hiểu quy trình xử lý dữ liệu và lưu trữ trong kiến trúc serverless.
* Củng cố kiến thức về các dịch vụ AWS phục vụ triển khai ứng dụng hiện đại, tạo nền tảng cho việc triển khai dự án Smart Docs AI trên môi trường AWS trong các tuần tiếp theo.
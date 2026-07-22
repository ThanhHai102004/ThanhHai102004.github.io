---
title: "Sharing and Feedback"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 7. </b> "
---

# CHIA SẺ VÀ GÓP Ý

## Kinh nghiệm học tập và triển khai
Trong suốt kỳ thực tập, tôi bắt đầu bằng việc học các kiến thức nền tảng và dịch vụ cốt lõi của AWS, sau đó dần chuyển sang các chủ đề nâng cao hơn như serverless, bảo mật, cơ sở dữ liệu, điện toán phi máy chủ, CI/CD, giám sát và kiểm soát chi phí. Việc viết worklog hàng tuần giúp tôi ôn lại những gì đã học, nhận diện khó khăn và hoàn thiện các phần còn thiếu trước khi chốt báo cáo.

Dự án chính của tôi là **Campus IT Support Ticket Portal**, một hệ thống dựa trên web dùng để gửi và quản lý các yêu cầu hỗ trợ IT trong môi trường trường học. Hệ thống bao gồm hai nhóm người dùng chính: người dùng có thể gửi ticket, theo dõi trạng thái và tải lên file đính kèm; quản trị viên có thể xem danh sách ticket, lọc yêu cầu, cập nhật trạng thái, thêm ghi chú xử lý và xóa ticket khi cần.

Điểm quan trọng nhất của dự án này là nó được xây dựng với kiến trúc serverless trên AWS. Frontend được triển khai bằng **AWS Amplify Hosting**, xác thực được xử lý bởi **Amazon Cognito**, API được quản lý bởi **Amazon API Gateway**, logic backend chạy trên **AWS Lambda**, dữ liệu được lưu trong **Amazon DynamoDB**, file đính kèm được lưu trong **Amazon S3**, thông báo sử dụng **Amazon SES**, log được giám sát thông qua **Amazon CloudWatch**, và toàn bộ quyền hạn được kiểm soát bởi **AWS IAM**.

Thông qua dự án này, tôi hiểu rằng một ứng dụng đám mây hoàn chỉnh không chỉ là tạo ra các dịch vụ riêng lẻ. Phần quan trọng hơn là thiết kế luồng kết nối giữa các dịch vụ, áp dụng các quyền hạn phù hợp, kiểm tra kỹ lưỡng từng hàm và ghi chép lại quá trình triển khai đủ rõ ràng để người khác có thể hiểu được.

## Kiến thức thu được

- Tôi hiểu cách một frontend được host và tự động deploy thông qua **AWS Amplify Hosting**.
- Tôi học được cách **Amazon Cognito** hỗ trợ đăng ký, đăng nhập, JWT token và phân quyền qua các nhóm `Users`/`Admins`.
- Tôi hiểu vai trò của **API Gateway** trong việc nhận request, xác thực JWT token và chuyển tiếp request đến **AWS Lambda**.
- Tôi đã thực hành triển khai các thao tác backend với **AWS Lambda**, bao gồm các hàm tạo, đọc, cập nhật và xóa.
- Tôi học cách lưu trữ dữ liệu NoSQL trong **Amazon DynamoDB** và quản lý file đính kèm bằng **Amazon S3**.
- Tôi đã quen thuộc với thông báo email sử dụng **Amazon SES** và luồng cập nhật thời gian thực bằng **Amazon DynamoDB Streams / WebSocket**.
- Tôi học cách sử dụng **Amazon CloudWatch** để kiểm tra lỗi và giám sát hoạt động backend.
- Tôi nhận thức rõ hơn về **nguyên tắc tối thiểu quyền (least privilege)** của AWS và giám sát chi phí thông qua **Billing Dashboard**.

## Khó khăn gặp phải

Trong quá trình triển khai, tôi gặp một số khó khăn khi kết nối các dịch vụ lại với nhau. Ví dụ, luồng Cognito và JWT Authorizer ban đầu rất dễ bị cấu hình sai vì frontend, API Gateway và Lambda đều cần xử lý token và quyền người dùng chính xác. Việc tách quyền người dùng thông thường khỏi quyền quản trị cũng đòi hỏi phải kiểm tra cẩn thận để ngăn người dùng truy cập vào các tính năng quản trị.

Một thách thức khác là gỡ lỗi backend. Khi request từ frontend không hoạt động như mong đợi, tôi phải kiểm tra nhiều lớp như cấu hình API Gateway, log Lambda, dữ liệu DynamoDB, quyền IAM và cài đặt CORS. Khi đã quen thuộc hơn với CloudWatch Logs, tôi xác định sự cố nhanh hơn và kiểm tra hệ thống từng bước một.

Việc viết tài liệu cũng tốn đáng kể thời gian vì các phần Working, Proposal, Blogs Posted, Workshop, Self-Assessment và Sharing and Feedback cần phải đồng bộ với nhau. Khi kiến trúc hoặc nội dung dự án thay đổi, các phần tài liệu liên quan cũng phải được cập nhật để tránh mâu thuẫn.

## Góp ý và Đề xuất

Từ trải nghiệm của tôi, hình thức học dựa trên workshop rất phù hợp cho học sinh/sinh viên vì nó kết hợp giữa lý thuyết và thực hành thực tế. Tuy nhiên, để học hiệu quả hơn, người học nên ghi chú lại trong lúc triển khai, chụp ảnh màn hình sau các bước quan trọng và cập nhật sơ đồ kiến trúc làm tài liệu tham khảo nếu dự án thay đổi.

Tôi cũng nhận ra việc dọn dẹp tài nguyên (cleanup) và giám sát qua Billing Dashboard cần được chuẩn bị kỹ lưỡng. Người học AWS mới có thể tập trung tạo tài nguyên và quên kiểm tra xem tài nguyên còn chạy hay không sau khi thực hành. Việc giám sát chi phí nên trở thành một thói quen ngay từ đầu.

Nếu tiếp tục phát triển dự án này, tôi muốn thực hiện các nội dung sau:

- Xây dựng dashboard thống kê ticket theo trạng thái, mức độ ưu tiên và danh mục.
- Cải thiện giao diện quản trị để lọc và thao tác hàng loạt ticket mượt mà hơn.
- Thêm log chi tiết cho các hành động quản trị.
- Hoàn-thiện cấu hình custom domain và quy trình xác thực domain nếu cho phép.
- Định nghĩa các chính sách IAM để quyền giữa các dịch vụ được kiểm soát chặt chẽ hơn.

## Kết luận

Nhìn chung, kỳ thực tập mang lại cho tôi cái nhìn thực tế hơn về cách xây dựng một ứng dụng serverless trên AWS. Tôi không chỉ học cách sử dụng các dịch vụ AWS riêng lẻ, mà còn hiểu về thiết kế luồng hệ thống, kiểm soát truy cập, giám sát lỗi, quản lý chi phí và tài liệu kỹ thuật. Trải nghiệm này mang lại cho tôi nền tảng vững chắc hơn để tiếp tục học điện toán đám mây và xây dựng các dự án AWS trong tương lai.
---
title: "Blog 3 Học Serverless, Authentication, Monitoring và Security trên AWS"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

Sau khi đã thực hành các dịch vụ AWS core, tôi bắt đầu chuyển sang phần serverless để phục vụ project Campus IT Support Ticket Portal. Đây là giai đoạn tôi học được nhiều nhất, vì các dịch vụ không còn đứng riêng lẻ nữa mà phải kết nối thành một luồng hoàn chỉnh: frontend gọi API, API xác thực token, backend xử lý logic, dữ liệu lưu vào database, file lưu vào storage và lỗi được theo dõi qua log.

Dịch vụ tôi làm quen trước là AWS Lambda. Ban đầu tôi hơi mất thời gian để thay đổi cách nghĩ. Với server truyền thống, ứng dụng backend thường chạy liên tục. Với Lambda, function chỉ chạy khi có request hoặc event. Điều này rất phù hợp với các chức năng như tạo ticket, cập nhật trạng thái ticket, lấy danh sách ticket hoặc xử lý thông tin file đính kèm.

Khi viết logic cho Lambda, tôi nhận ra function không nên ôm quá nhiều việc. Một function dễ kiểm soát hơn khi nó có luồng rõ ràng: nhận request, kiểm tra dữ liệu đầu vào, xử lý nghiệp vụ, gọi DynamoDB hoặc S3 nếu cần, rồi trả response. Nếu viết quá nhiều logic lẫn vào nhau, lúc debug sẽ rất mệt, đặc biệt khi lỗi chỉ hiện trong CloudWatch Logs.

API Gateway là phần tiếp theo tôi thực hành. Đây là nơi frontend giao tiếp với backend. Tôi tạo các route tương ứng với chức năng của hệ thống, ví dụ gửi ticket, lấy danh sách ticket, cập nhật trạng thái hoặc xóa ticket. Lúc cấu hình API, tôi phải chú ý HTTP method, CORS và cách route invoke Lambda. Có lúc frontend gọi API bị lỗi CORS, từ đó tôi hiểu rằng frontend chạy được chưa chắc API đã sẵn sàng cho browser gọi.

Phần authentication làm tôi mất nhiều thời gian hơn dự kiến. Tôi dùng Amazon Cognito để quản lý đăng ký, đăng nhập và phân quyền user/admin. Ban đầu JWT token khá khó hình dung vì nó đi qua nhiều bước: người dùng đăng nhập, Cognito trả token, frontend lưu và gửi token khi gọi API, API Gateway dùng JWT Authorizer để kiểm tra token trước khi cho request đi tiếp.

Sau khi hiểu được luồng đó, tôi thấy Cognito giúp project rõ ràng hơn. User thông thường chỉ cần gửi ticket và xem ticket của mình. Admin cần quyền rộng hơn để xem danh sách ticket, cập nhật trạng thái, ghi chú xử lý hoặc xóa ticket. Từ đây tôi phân biệt rõ hơn authentication và authorization. Authentication trả lời câu hỏi “người dùng là ai”, còn authorization trả lời “người này được phép làm gì”.

Với dữ liệu ticket, tôi sử dụng DynamoDB. Khác với RDS, DynamoDB khiến tôi phải nghĩ trước về cách ứng dụng sẽ truy vấn dữ liệu. Với Ticket Portal, các thao tác chính gồm tạo ticket, lấy ticket theo người dùng, admin xem danh sách, cập nhật trạng thái và xóa ticket. Khi xác định được các thao tác này, việc thiết kế item và key trong DynamoDB dễ có hướng hơn.

S3 được dùng cho phần file đính kèm. Tôi không muốn lưu file trực tiếp trong database vì như vậy dữ liệu ticket sẽ nặng và khó quản lý. Cách hợp lý hơn là file được lưu trong S3, còn DynamoDB chỉ lưu metadata như tên file hoặc object key. Nhờ vậy ticket vẫn gọn, nhưng hệ thống vẫn biết file nào thuộc về ticket nào.

Monitoring là phần tôi thấy rất thực tế khi làm project. Khi backend lỗi, nếu không xem log thì gần như chỉ đoán mò. CloudWatch Logs giúp tôi kiểm tra Lambda có được gọi không, request body có đúng không, lỗi đến từ validate input, IAM permission, DynamoDB hay S3. Có lần lỗi không nằm ở code chính mà nằm ở quyền của Lambda role, và tôi chỉ phát hiện được sau khi đọc log.

Security cũng là phần tôi phải rà lại nhiều lần. Tôi kiểm tra IAM role của Lambda, quyền truy cập DynamoDB, quyền với S3 bucket, CORS và các route cần token. Với project sinh viên, có thể chưa đạt mức production, nhưng tôi vẫn muốn hệ thống có cấu trúc quyền hợp lý: user không làm việc của admin, bucket không public bừa bãi và backend không dùng quyền quá rộng.

Một việc nhỏ nhưng quan trọng ở cuối quá trình học là cleanup và kiểm tra Billing. Sau mỗi lần tạo hoặc test tài nguyên, tôi kiểm tra lại những gì còn hoạt động. Việc này giúp tránh phát sinh chi phí không cần thiết và cũng giúp tôi hiểu tài nguyên nào thật sự thuộc về project.

Điều tôi rút ra sau giai đoạn này là serverless không có nghĩa là đơn giản hơn về tư duy. Nó giảm việc quản lý server, nhưng đòi hỏi hiểu rõ trách nhiệm của từng dịch vụ. API Gateway là cổng API, Lambda xử lý logic, Cognito quản lý identity, DynamoDB lưu dữ liệu, S3 lưu file, CloudWatch hỗ trợ quan sát lỗi và IAM kiểm soát quyền.

Sau khi nối được các phần này lại với nhau, tôi hiểu hơn cách một ứng dụng cloud hoạt động end-to-end. Đây cũng là phần giúp tôi viết workshop rõ hơn, vì mỗi bước triển khai đều có lý do cụ thể chứ không chỉ là làm theo hướng dẫn: deploy frontend, cấu hình đăng nhập, tạo API, viết backend, lưu dữ liệu, kiểm thử user/admin, xem log và cleanup tài nguyên.

Link bài blog đã đăng: [AWS Study Group VN](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2219706598794300/)

## Tài liệu tham khảo
- [AWS Lambda Deverloper Guide](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)
- [Amazon API Gateway REST API](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-rest-api.html)
- [Amazon Cognito Deverloper Guide](https://docs.aws.amazon.com/cognito/latest/developerguide/what-is-amazon-cognito.html)
- [What is Amazon DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html)
- [Sending Lambda logs to CloudWatch Logs](https://docs.aws.amazon.com/lambda/latest/dg/monitoring-cloudwatchlogs.html)
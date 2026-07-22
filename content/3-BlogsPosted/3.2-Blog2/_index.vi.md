---
title: "Blog 2 Thực hành các dịch vụ AWS core: EC2, S3, VPC và Database"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

Sau khi đã quen hơn với tài khoản AWS và giao diện console, tôi chuyển sang thực hành các dịch vụ core. Đây là giai đoạn tôi bắt đầu thấy AWS không còn là một danh sách dịch vụ rời rạc, mà là nhiều mảnh ghép có thể kết hợp với nhau để tạo thành một hệ thống. Những dịch vụ tôi tập trung nhiều nhất gồm EC2, S3, VPC, Security Group, IAM và database như RDS/Aurora.

Tôi bắt đầu với EC2 vì đây là dịch vụ giúp hình dung rõ nhất khái niệm compute trên cloud. Khi tạo một instance, tôi phải chọn AMI, instance type, key pair, network và security group. Ban đầu các lựa chọn này có vẻ chỉ là bước cấu hình, nhưng khi thực hành nhiều hơn tôi hiểu mỗi lựa chọn đều ảnh hưởng đến cách instance hoạt động. AMI quyết định hệ điều hành, instance type quyết định tài nguyên, còn security group quyết định instance được phép nhận traffic nào.

Một điều tôi rút ra từ EC2 là tạo tài nguyên rất nhanh, nhưng quản lý tài nguyên mới là phần cần cẩn thận. Sau khi test xong, tôi phải kiểm tra instance còn chạy hay không, có public IP hay không và security group có đang mở port quá rộng không. Những thao tác này nhỏ nhưng giúp tôi hình thành thói quen kiểm tra lại tài nguyên sau mỗi lần thực hành.

Tiếp theo, tôi học Amazon S3. Lúc đầu tôi chỉ nghĩ S3 là nơi upload file, nhưng khi làm kỹ hơn tôi thấy S3 liên quan nhiều đến cách tổ chức dữ liệu và phân quyền. Tôi thực hành tạo bucket, upload object, kiểm tra object key, bật/tắt public access và xem cách bucket policy hoặc IAM permission ảnh hưởng đến quyền truy cập.

Phần S3 giúp tôi hiểu rõ hơn một nguyên tắc quan trọng: không nên public dữ liệu nếu không thật sự cần. Trong project Ticket Portal, file đính kèm của ticket có thể là ảnh lỗi hoặc tài liệu người dùng gửi lên. Những file này không nên để ai cũng truy cập được. Cách hợp lý hơn là lưu file trong S3, còn ứng dụng kiểm soát quyền truy cập thông qua backend và IAM role.

VPC là phần tôi thấy khó hơn hẳn so với EC2 và S3. Các khái niệm như subnet, route table, internet gateway và security group lúc đầu khá dễ nhầm. Tôi phải đọc lại nhiều lần và thực hành từng bước để hiểu traffic đi như thế nào. Khi một resource không kết nối được, tôi không thể chỉ nhìn vào một chỗ, mà phải kiểm tra subnet, route table, security group và cả cách resource được đặt trong network.

Nhờ thực hành VPC, tôi hiểu rõ hơn vì sao network design ảnh hưởng đến security. Không phải tài nguyên nào cũng nên đưa ra internet. Nếu một database chỉ phục vụ backend, nó nên được bảo vệ trong phạm vi phù hợp thay vì mở public không cần thiết. Dù project cuối của tôi dùng nhiều dịch vụ serverless, kiến thức VPC vẫn giúp tôi hiểu cách AWS tổ chức môi trường mạng và cách suy nghĩ khi thiết kế hệ thống thực tế.

Tôi cũng thực hành với Amazon RDS và Aurora để hiểu database quan hệ trên AWS. So với việc tự cài database trên server, RDS giúp giảm nhiều công việc vận hành, nhưng không có nghĩa là người dùng không cần quan tâm cấu hình. Tôi vẫn phải chú ý database engine, instance size, backup, networking và security. Phần này giúp tôi hiểu rằng managed service không thay thế hoàn toàn tư duy thiết kế, mà giúp giảm bớt phần vận hành lặp lại.

Khi so sánh RDS với DynamoDB, tôi bắt đầu hiểu hơn việc chọn database phải dựa trên cách ứng dụng truy cập dữ liệu. RDS phù hợp với dữ liệu quan hệ, SQL query và các thao tác cần join. DynamoDB phù hợp hơn với các access pattern rõ ràng, tốc độ cao và mô hình serverless. Với hệ thống ticket, các thao tác như tạo ticket, xem danh sách, cập nhật trạng thái và xóa ticket khá rõ ràng, nên DynamoDB là lựa chọn hợp lý cho project cuối.

Trong giai đoạn này tôi cũng tiếp tục làm workshop trên AWS Study Group. Điều tôi thấy hữu ích nhất là được tự tay tạo resource, cấu hình, test rồi sửa lỗi. Có những lỗi rất đơn giản như nhầm region, security group thiếu rule hoặc IAM role thiếu quyền, nhưng chính các lỗi đó làm tôi hiểu dịch vụ thật hơn. Nếu chỉ đọc tài liệu, tôi nghĩ mình sẽ khó nhớ được lâu như vậy.

Sau khi thực hành các dịch vụ core, tôi có cái nhìn rõ hơn về từng lớp trong một hệ thống cloud. EC2 giúp hiểu compute, S3 giúp hiểu storage, VPC giúp hiểu networking, RDS/Aurora giúp hiểu database quan hệ, còn IAM và Billing nhắc tôi rằng security và chi phí luôn đi cùng quá trình triển khai.

Giai đoạn này tạo nền tốt để tôi chuyển sang serverless. Khi đã hiểu compute truyền thống, storage, network và database, tôi dễ hình dung hơn vì sao các dịch vụ như API Gateway, Lambda, Cognito, DynamoDB, S3 và CloudWatch có thể kết hợp thành một ứng dụng hoàn chỉnh.

Link bài blog đã đăng: [AWS Study Group VN](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2219703182127975/)

## Tài liệu tham khảo
- [Amazon EC2 Usrer Guide](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html)
- [What is Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html)
- [What is Amazon VCP](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html)
- [Amazon RDS User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html)
- [Amazon Aura User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/CHAP_AuroraOverview.html)
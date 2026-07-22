---
title: "Blog 1 Học AWS từ tạo tài khoản, IAM và kiểm soát chi phí"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

Khi mới bắt đầu học AWS, tôi từng nghĩ phần khó nhất sẽ là triển khai được một hệ thống chạy trên cloud. Nhưng sau vài buổi đầu thực hành, tôi nhận ra việc đầu tiên cần làm tốt lại là những thứ rất cơ bản: tạo tài khoản đúng cách, hiểu region mình đang dùng, biết chỗ kiểm tra chi phí và không cấp quyền quá rộng cho tài nguyên.

Việc đầu tiên tôi làm là đăng nhập vào AWS Management Console và làm quen với giao diện. Lúc đầu tôi khá rối vì console có rất nhiều dịch vụ, mỗi dịch vụ lại có dashboard và cách đặt tên riêng. Tôi phải thử tìm từng dịch vụ như EC2, S3, IAM, Billing và CloudWatch để quen dần vị trí của chúng. Một việc nhỏ nhưng giúp tôi tránh nhầm về sau là luôn nhìn lại region ở góc trên bên phải trước khi tạo tài nguyên. Có lúc tôi tìm một resource không thấy, sau đó mới biết mình đang xem sai region.

Sau phần làm quen console, tôi bắt đầu chú ý nhiều hơn đến Billing Dashboard. Đây là phần tôi nghĩ sinh viên học AWS rất nên kiểm tra thường xuyên. Khi làm local, nếu cấu hình sai thì thường chỉ mất thời gian sửa. Còn trên cloud, nếu tạo tài nguyên rồi quên xóa, chi phí có thể phát sinh thật. Vì vậy tôi tập thói quen sau mỗi buổi thực hành đều kiểm tra Billing, Free Tier và danh sách resource đã tạo.

Trong quá trình học, tôi để ý một số dịch vụ dễ phát sinh phí nếu không quản lý kỹ, ví dụ EC2 instance, NAT Gateway, Load Balancer, Route 53 domain hoặc dữ liệu lưu trữ lâu dài. Tôi chưa dùng tất cả các dịch vụ đó trong project cuối, nhưng việc biết trước giúp tôi cẩn thận hơn khi đọc workshop hoặc làm theo hướng dẫn. Với tôi, kiểm soát chi phí không còn là việc phụ, mà là một phần của cách học cloud có trách nhiệm.

Phần tiếp theo tôi học là IAM. Ban đầu IAM hơi khô vì nhiều khái niệm giống nhau: user, group, role, policy. Tôi mất một thời gian để phân biệt user là danh tính người dùng, group dùng để gom quyền cho nhiều user, role thường được service sử dụng, còn policy là phần mô tả quyền được phép làm gì. Khi hiểu được các khái niệm này, tôi mới thấy vì sao AWS luôn nhấn mạnh nguyên tắc least privilege.

Lúc thực hành, có những lúc tôi muốn cấp quyền rộng để làm cho nhanh. Nhưng khi liên hệ với project Ticket Portal, tôi thấy cách đó không ổn. Ví dụ Lambda chỉ cần đọc/ghi ticket trong DynamoDB thì không nên có toàn quyền Administrator. Nếu Lambda chỉ upload file đính kèm lên một S3 bucket cụ thể, quyền của role cũng nên giới hạn vào bucket đó. Việc học IAM từ sớm giúp tôi nhìn security như một phần của thiết kế, không phải bước làm cho có ở cuối project.

Tôi cũng thực hành tạo EC2 instance để hiểu compute truyền thống trên AWS. Khi tạo instance, tôi phải chọn AMI, instance type, key pair, security group và network. Những bước này giúp tôi hiểu một máy chủ ảo trên AWS được cấu hình như thế nào. Dù project cuối cùng của tôi dùng serverless nhiều hơn, EC2 vẫn là phần đáng học vì nó giúp tôi có nền tảng để so sánh với Lambda.

Một lỗi nhỏ tôi gặp khi học EC2 là cấu hình security group chưa đúng nên không truy cập được instance như mong muốn. Từ lỗi đó tôi hiểu rằng không phải cứ tạo tài nguyên xong là dùng được ngay. Network rule, port, inbound traffic và quyền truy cập đều ảnh hưởng trực tiếp đến kết quả thực hành. Những lỗi nhỏ như vậy làm tôi nhớ bài lâu hơn so với chỉ đọc tài liệu.

Ngoài các dịch vụ nền tảng, tôi cũng tìm hiểu sơ bộ Amazon Bedrock. Tôi không dùng Bedrock làm dịch vụ chính trong project, nhưng phần này giúp tôi thấy AWS không chỉ có hạ tầng như server, storage hay database. AWS còn có nhiều managed services ở tầng cao hơn, phục vụ các bài toán ứng dụng hiện đại và AI.

Sau giai đoạn đầu, điều tôi rút ra là học AWS không nên bắt đầu bằng việc làm thật nhiều dịch vụ cùng lúc. Trước hết cần biết cách dùng tài khoản an toàn, kiểm tra chi phí, hiểu IAM và thao tác được trên console. Những việc này nghe đơn giản nhưng nếu bỏ qua thì khi làm project lớn hơn rất dễ gặp lỗi khó kiểm soát.

Với tôi, giai đoạn này giống như bước chuẩn bị nền. Sau khi đã quen console, biết kiểm tra Billing và hiểu cơ bản về IAM, tôi tự tin hơn khi chuyển sang các dịch vụ core như EC2, S3, VPC, RDS và sau đó là các dịch vụ serverless cho project Campus IT Support Ticket Portal.


Link bài blog đã đăng: [AWS Study Group VN](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2219698898795070/)

## Tài liệu tham khảo
- [Getting started with AWS](https://docs.aws.amazon.com/whitepapers/latest/aws-overview/getting-started-with-aws.html)
- [AWS Management Console](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/what-is.html)
- [AWS Billing and Cost Management](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/billing-what-is.html)
- [Security best practice IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
- [Amazon EC2 Usrer Guide](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html)
---
title : "Tổng quan kiến trúc"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

## Tổng quan kiến trúc hệ thống

Campus IT Support Ticket Portal được triển khai bằng kiến trúc serverless trên Amazon Web Services.

Kiến trúc này không yêu cầu vận hành một máy chủ backend truyền thống. Các chức năng như xác thực người dùng, xử lý API, lưu trữ ticket, lưu trữ tệp đính kèm, thông báo email và cập nhật thời gian thực được triển khai bằng các dịch vụ AWS được quản lý.

Frontend được triển khai thông qua AWS Amplify Hosting. Người dùng đăng ký và đăng nhập thông qua Amazon Cognito Hosted UI. Sau khi xác thực thành công, Cognito cấp JWT token cho frontend.

Frontend đính kèm JWT token trong các request gửi tới Amazon API Gateway. API Gateway sử dụng JWT Authorizer để xác thực người dùng trước khi chuyển request đến hàm AWS Lambda phù hợp.

Lambda xử lý logic ứng dụng, tương tác với Amazon DynamoDB để lưu trữ dữ liệu ticket, và sử dụng Amazon S3 để lưu trữ tệp đính kèm.

Hệ thống cũng sử dụng DynamoDB Streams, hàm Lambda thông báo, Amazon SES và API Gateway WebSocket API để gửi thông báo email và cập nhật theo thời gian thực.

#### 2. Sơ đồ kiến trúc tổng thể

![](/images/5-Workshop/5.2-ArchitectureOverview/Architecture.jpg)

### 3. Các thành phần chính

#### 3.1 Người dùng và quản trị viên

Hệ thống hỗ trợ hai nhóm người dùng chính:

Người dùng: sinh viên hoặc nhân viên gửi yêu cầu hỗ trợ IT và theo dõi trạng thái của họ.

Quản trị viên: thành viên của đội ngũ hỗ trợ IT nhận, phân loại, cập nhật và xóa ticket.

Cả hai nhóm người dùng đều truy cập hệ thống qua trình duyệt web trên HTTPS.

#### 3.2 AWS Amplify Hosting

AWS Amplify Hosting được sử dụng để triển khai và phân phối giao diện hệ thống.

Amplify được kết nối với GitHub và tự động thực hiện quy trình build và triển khai mỗi khi mã nguồn được đẩy lên kho lưu trữ.

Frontend được phát triển bằng Hugo, HTML, CSS và JavaScript.

#### 3.3 Amazon Cognito

Amazon Cognito cung cấp:

- Đăng ký tài khoản.
- Xác thực người dùng.
- Đăng xuất.
- Quản lý phiên làm việc.
- Phân quyền thông qua Cognito Groups.
- Cấp JWT token.

Hệ thống sử dụng hai nhóm chính:

- Users
- Admins

JWT token chứa thông tin người dùng và nhóm, và được frontend gửi tới API Gateway cho các request đã xác thực.

#### 3.4 Amazon API Gateway

Amazon API Gateway cung cấp hai loại API:

- HTTP API: hỗ trợ các thao tác tạo, đọc, cập nhật và xóa ticket.
- WebSocket API: duy trì kết nối thời gian thực giữa trình duyệt và backend.

HTTP API sử dụng JWT Authorizer để xác thực token được phát hành bởi Amazon Cognito.

Sau khi xác thực thành công, API Gateway chuyển request tới hàm Lambda phù hợp.

#### 3.5 AWS Lambda

Hệ thống sử dụng nhiều hàm Lambda để tách biệt trách nhiệm.

CampusSupportTicketService

Hàm Lambda này xử lý:

- Tạo ticket.
- Liệt kê ticket.
- Tra cứu từng ticket riêng lẻ.
- Cập nhật trạng thái.
- Cập nhật ghi chú xử lý.
- Xóa ticket.
- Kiểm tra quyền của người dùng và quản trị viên.
- Tạo presigned URL cho tải lên và tải xuống tệp.

CampusSupportNotificationService

Hàm Lambda này được kích hoạt bởi DynamoDB Streams để:

- Gửi email xác nhận khi ticket được tạo.
- Gửi cảnh báo cho ticket ưu tiên Cao và Khẩn cấp.
- Gửi email khi trạng thái ticket hoặc ghi chú xử lý thay đổi.
- Xuất bản sự kiện thời gian thực qua WebSocket API.

CampusSupportWebSocketService

Hàm Lambda này xử lý:

- Sự kiện $connect.
- Sự kiện $disconnect.
- Xác thực token Cognito trong quá trình thiết lập kết nối.
- Lưu trữ và xóa các giá trị connectionId.

#### 3.6 Amazon DynamoDB

Hệ thống sử dụng hai bảng DynamoDB chính.

CampusSupportTickets

Bảng này lưu trữ:

- ID ticket.
- Tên người gửi.
- Địa chỉ email.
- Danh mục sự cố.
- Mức độ ưu tiên.
- Mô tả sự cố.
- Trạng thái.
- Ghi chú xử lý.
- Thông tin đính kèm.
- Thời gian tạo và cập nhật.

CampusSupportConnections

Bảng này lưu các kết nối WebSocket đang hoạt động, bao gồm:

- connectionId
- User ID hoặc email.
- Nhóm phân quyền.
- Thời gian kết nối.

#### 3.7 Amazon S3

Amazon S3 lưu trữ các tệp đính kèm của ticket, bao gồm:

- Tệp PNG.
- Tệp JPG.
- Tệp WebP.
- Tài liệu PDF.

Bucket được đặt ở chế độ riêng tư.

Người dùng không truy cập trực tiếp bucket. Lambda tạo các S3 Presigned URL cho phép tải lên hoặc tải xuống tệp trong thời gian giới hạn.

#### 3.8 Amazon SES

Amazon SES được sử dụng để gửi:

- Email xác nhận sau khi tạo ticket.
- Email cảnh báo cho đội ngũ hỗ trợ IT.
- Thông báo khi trạng thái ticket thay đổi.
- Thông báo khi quản trị viên thêm ghi chú xử lý.

SES hiện đang hoạt động trong môi trường Sandbox, vì vậy địa chỉ người gửi và người nhận phải được xác minh.

#### 3.9 Amazon CloudWatch

Amazon CloudWatch lưu trữ log và hỗ trợ giám sát cho:

- AWS Lambda.
- API Gateway.
- DynamoDB Streams.
- WebSocket API.

CloudWatch giúp kiểm tra lỗi, thời gian thực thi, yêu cầu thất bại và các sự kiện hệ thống.

#### 3.10 AWS IAM

AWS IAM cung cấp quyền cho các hàm Lambda.

Mỗi hàm Lambda chỉ nhận các quyền cần thiết, chẳng hạn như:

- Đọc và ghi dữ liệu DynamoDB.
- Tải lên và tải xuống tệp từ S3.
- Gửi email qua SES.
- Gửi tin nhắn qua WebSocket Management API.
- Ghi log vào CloudWatch.

Mô hình quyền này tuân theo nguyên tắc least privilege.

### 4. Luồng xác thực người dùng

Quá trình xác thực diễn ra như sau:

- Người dùng truy cập frontend được lưu trữ trên AWS Amplify.
- Người dùng chọn chức năng đăng nhập hoặc đăng ký.
- Trình duyệt được chuyển hướng tới Amazon Cognito Hosted UI.
- Cognito xác thực tài khoản.
- Sau khi xác thực thành công, Cognito chuyển người dùng trở lại frontend.
- Frontend nhận JWT tokens.
- Token được lưu cho phiên đã xác thực.
- Frontend đính kèm token trong các request gửi tới API Gateway.
- JWT Authorizer xác thực token.
- Các request hợp lệ được chuyển tiếp tới Lambda.
- Nếu token không hợp lệ hoặc đã hết hạn, API Gateway từ chối request trước khi hàm Lambda được gọi.

### 5. Luồng tạo ticket

Quá trình tạo ticket diễn ra như sau:

- Người dùng nhập thông tin sự cố thông qua frontend.
- Khi chọn tệp đính kèm, frontend yêu cầu một URL tải lên từ backend.
- API Gateway xác thực JWT token.
- CampusSupportTicketService tạo một S3 presigned URL.
- Frontend tải tệp trực tiếp lên S3 bằng presigned URL.
- Frontend gửi thông tin ticket và metadata đính kèm tới HTTP API.
- API Gateway chuyển request tới CampusSupportTicketService.
- Lambda xác thực dữ liệu và quyền người dùng.
- Ticket được lưu vào bảng CampusSupportTickets.
- API trả về ID ticket cho frontend.
- DynamoDB Streams phát hành sự kiện INSERT.
- CampusSupportNotificationService gửi email xác nhận.
- Hàm thông báo xuất bản sự kiện qua WebSocket API.
- Giao diện người dùng và quản trị viên cập nhật mà không cần tải lại trang.

### 6. Luồng cập nhật ticket

Quá trình cập nhật ticket diễn ra như sau:

- Quản trị viên đăng nhập bằng tài khoản thuộc nhóm Admins.
- Quản trị viên chọn một ticket.
- Quản trị viên cập nhật trạng thái hoặc ghi chú xử lý của ticket.
- Frontend gửi request PATCH tới API Gateway.
- JWT Authorizer xác thực token.
- Lambda thực hiện kiểm tra thêm về Cognito Group.
- Nếu tài khoản đã xác thực thuộc nhóm Admins, Lambda cập nhật ticket trong DynamoDB.
- DynamoDB Streams phát hành sự kiện MODIFY.
- CampusSupportNotificationService so sánh dữ liệu ticket cũ và mới.
- Một email thông báo được gửi tới người gửi ticket.
- Một sự kiện WebSocket được gửi tới các trình duyệt đã kết nối.
- Giao diện cập nhật theo thời gian thực.

### 7. Luồng thông báo thời gian thực

Trình duyệt thiết lập kết nối tới WebSocket API tại stage production.

Quá trình kết nối như sau:

- Frontend gửi một Cognito token trong quá trình $connect.
- CampusSupportWebSocketService xác thực token.
- Khi token hợp lệ, connectionId được lưu trong CampusSupportConnections.
- Khi ticket được tạo hoặc cập nhật, hàm thông báo đọc các bản ghi kết nối đang hoạt động.
- Lambda gửi một sự kiện qua WebSocket Management API.
- Frontend nhận sự kiện và cập nhật giao diện.
- Khi người dùng đóng trang hoặc mất kết nối, sự kiện $disconnect được kích hoạt.
- Các bản ghi kết nối không hợp lệ bị xóa khỏi DynamoDB.

### 8. Kiến trúc bảo mật

Hệ thống áp dụng nhiều lớp bảo mật:

- HTTPS bảo vệ dữ liệu truyền giữa trình duyệt và các dịch vụ AWS.
- Amazon Cognito xác thực người dùng.
- JWT Authorizer bảo vệ các route của HTTP API.
- Cognito Groups phân biệt quyền của người dùng và quản trị viên.
- Lambda xác thực phân quyền trước khi thực hiện các thao tác quản trị.
- Bucket S3 vẫn ở chế độ riêng tư.
- Presigned URL chỉ có hiệu lực trong một khoảng thời gian giới hạn.
- IAM roles tuân theo nguyên tắc least privilege.
- CloudWatch logs hỗ trợ khắc phục sự cố và điều tra sự cố.

### 9. Đặc điểm của kiến trúc serverless

Kiến trúc serverless mang lại một số lợi ích:

- Không cần cấu hình hoặc bảo trì máy chủ backend.
- Các dịch vụ AWS có thể tự động mở rộng theo lưu lượng truy cập.
- Chi phí chủ yếu dựa trên mức sử dụng thực tế.
- Các dịch vụ xác thực, lưu trữ, email và WebSocket có thể tích hợp dễ dàng.
- Khối lượng công việc vận hành được giảm xuống.
- Kiến trúc phù hợp cho hệ thống hỗ trợ IT của trường học.
- Hệ thống có thể được mở rộng trong tương lai.

Phần tiếp theo trình bày các điều kiện tiên quyết cần thiết trước khi triển khai hệ thống.
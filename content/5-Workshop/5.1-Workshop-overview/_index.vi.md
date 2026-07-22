---
title : "Tổng quan dự án"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

### Campus IT Support Ticket Portal
+ **Campus IT Support Ticket Portal** là một hệ thống helpdesk không máy chủ được thiết kế cho môi trường giáo dục. Nó cho phép sinh viên và nhân viên gửi yêu cầu hỗ trợ IT, theo dõi trạng thái xử lý và nhận thông báo khi một ticket được tạo hoặc cập nhật.

Hệ thống cũng cung cấp giao diện quản trị cho đội ngũ hỗ trợ IT. Quản trị viên có thể tiếp nhận, tìm kiếm, phân loại, cập nhật, thêm ghi chú xử lý và xóa ticket. Dữ liệu hiển thị trên giao diện có thể được đồng bộ theo thời gian thực mà không cần người dùng tải lại trang.

Frontend của dự án được triển khai bằng **AWS Amplify Hosting** tại:

[Truy cập Campus IT Support Ticket Portal](https://main.d37atxjbyyp60m.amplifyapp.com/)

### 1. Mục tiêu của dự án

Dự án được phát triển để đạt được các mục tiêu sau:

- Cung cấp một kênh tập trung để sinh viên và nhân viên gửi yêu cầu hỗ trợ IT.
- Hỗ trợ các danh mục sự cố phổ biến như WiFi, tài khoản, phần mềm và thiết bị.
- Cho phép người dùng theo dõi lịch sử ticket và trạng thái xử lý.
- Cho phép người dùng đính kèm hình ảnh, tài liệu PDF và các tệp liên quan khác.
- Gửi email xác nhận khi ticket được tạo.
- Gửi thông báo khi trạng thái ticket hoặc ghi chú xử lý thay đổi.
- Đồng bộ dữ liệu ticket theo thời gian thực thông qua kết nối WebSocket.
- Cung cấp bảng điều khiển quản trị để giám sát và xử lý ticket.
- Áp dụng kiến trúc serverless để giảm yêu cầu quản lý máy chủ.
- Tự động xây dựng và triển khai frontend từ GitHub bằng AWS Amplify Hosting.

### 2. Người dùng mục tiêu

Hệ thống hỗ trợ hai nhóm người dùng chính.

#### Người dùng

Người dùng có thể là sinh viên hoặc nhân viên của cơ sở giáo dục. Các chức năng chính của họ bao gồm:

- Đăng ký tài khoản.
- Đăng nhập và đăng xuất.
- Gửi yêu cầu hỗ trợ IT.
- Chọn danh mục sự cố và mức độ ưu tiên.
- Đính kèm tệp vào ticket.
- Nhận mã ticket sau khi gửi.
- Tra cứu một ticket theo mã.
- Xem các yêu cầu đã gửi trước đó.
- Nhận thông báo email và cập nhật trạng thái theo thời gian thực.

#### Quản trị viên

Quản trị viên là thành viên của đội ngũ hỗ trợ IT. Các chức năng chính của họ bao gồm:

- Xem bảng điều khiển tổng quan hệ thống.
- Xem tất cả ticket đã gửi.
- Tìm kiếm và lọc ticket.
- Xem chi tiết ticket và tệp đính kèm.
- Cập nhật trạng thái ticket.
- Thêm ghi chú xử lý.
- Xóa ticket.
- Nhận cảnh báo cho ticket ưu tiên Cao và Khẩn cấp.

### 3. Công nghệ chính và các dịch vụ AWS

Dự án sử dụng các công nghệ và dịch vụ sau:

- **Hugo, HTML, CSS và JavaScript**: dùng để xây dựng giao diện frontend.
- **GitHub**: dùng để quản lý mã nguồn và kiểm soát phiên bản.
- **AWS Amplify Hosting**: dùng cho lưu trữ frontend và triển khai CI/CD.
- **Amazon Cognito**: dùng cho đăng ký, xác thực, đăng xuất và phân quyền.
- **Amazon API Gateway**: dùng để cung cấp API HTTP và API WebSocket.
- **AWS Lambda**: dùng để xử lý logic ticket, thông báo và kết nối WebSocket.
- **Amazon DynamoDB**: dùng để lưu trữ ticket và thông tin kết nối WebSocket.
- **Amazon S3**: dùng để lưu trữ các tệp đính kèm trong bucket riêng tư.
- **Amazon SES**: dùng để gửi email xác nhận và thông báo.
- **Amazon CloudWatch**: dùng cho ghi log và giám sát hệ thống.
- **AWS IAM**: dùng để quản lý vai trò dịch vụ và quyền truy cập.

### 4. Logo của dự án

Dự án sử dụng tên Campus Support – Helpdesk Portal, thể hiện một cổng hỗ trợ kỹ thuật tập trung cho môi trường giáo dục.

![project logo](/images/5-Workshop/5.1-Project%20Overview/project-logo.jpg)

### 5. Giao diện khách

Trước khi xác thực, người dùng có thể xem phần giới thiệu hệ thống và truy cập các chức năng đăng nhập và đăng ký.

Giao diện hiển thị biểu mẫu gửi yêu cầu hỗ trợ, các trường thông tin sự cố và hướng dẫn để giúp người dùng cung cấp đủ thông tin cho đội ngũ hỗ trợ IT.

![homepage](/images/5-Workshop/5.1-Project%20Overview/guest-homepage.jpg)

### 6. Giao diện người dùng đã xác thực

Sau khi đăng nhập thành công thông qua Amazon Cognito, thông tin tài khoản đã xác thực sẽ được hiển thị trong thanh điều hướng.

Một số trường biểu mẫu có thể được tự động điền bằng thông tin của người dùng đã xác thực. Người dùng có thể gửi ticket, xem các yêu cầu đã gửi trước đó và nhận cập nhật trạng thái mà không cần tải lại trang.

![](/images/5-Workshop/5.1-Project%20Overview/user-homepage.jpg)

### 7. Giao diện quản trị viên

Trang quản trị viên cung cấp bảng điều khiển chứa tổng quan về hệ thống, bao gồm:

- Tổng số ticket.
- Số lượng ticket đang được xử lý.
- Số lượng ticket ưu tiên cao.
- Số lượng ticket đã giải quyết.

Quản trị viên có thể tìm kiếm và lọc ticket theo trạng thái, mức độ ưu tiên hoặc danh mục sự cố. Họ cũng có thể xem chi tiết ticket, truy cập tệp đính kèm, cập nhật trạng thái ticket và xóa ticket.

Dữ liệu ticket được lấy từ Amazon DynamoDB thông qua Amazon API Gateway và AWS Lambda.

![](/images/5-Workshop/5.1-Project%20Overview/admin-dashboard.jpg)

### 8. Kết quả hiện tại của dự án

Dự án đã tạo ra một hệ thống helpdesk serverless có chức năng với các thành phần chính sau:

Một frontend được triển khai công khai.

Đăng ký, xác thực và đăng xuất người dùng.

Phân quyền người dùng và quản trị viên.

Một API HTTP để tạo, đọc, cập nhật và xóa ticket.

Một cơ sở dữ liệu Amazon DynamoDB.

Lưu trữ tệp đính kèm riêng tư bằng Amazon S3.

Thông báo email bất đồng bộ bằng Amazon SES.

Cập nhật thời gian thực thông qua kết nối WebSocket.

Ghi log và giám sát thông qua Amazon CloudWatch.

Một quy trình CI/CD từ GitHub đến AWS Amplify Hosting.

Phần tiếp theo trình bày kiến trúc hệ thống tổng thể và luồng dữ liệu giữa các thành phần của dự án.


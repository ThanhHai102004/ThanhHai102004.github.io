---
title : "Triển khai frontend với AWS Amplify"
date : 2024-01-01 
weight : 4 
chapter : false
pre : " <b> 5.4. </b> "
---

Frontend của hệ thống được triển khai bằng AWS Amplify Hosting. Amplify được kết nối với GitHub để có thể tự động build và triển khai khi mã nguồn thay đổi.

#### Các bước thực hiện

1. Mở AWS Amplify Console và tạo một ứng dụng mới.
2. Kết nối Amplify với kho lưu trữ GitHub của dự án.
3. Chọn nhánh chính để triển khai.
4. Kiểm tra các cài đặt build và bắt đầu quá trình triển khai.
5. Sau khi triển khai thành công, mở tên miền mặc định của Amplify để kiểm tra trang web.

![](/images/5-Workshop/5.4-DeployFrontendwithAWSAmplify/amplify-hosting.jpg)

![](/images/5-Workshop/5.4-DeployFrontendwithAWSAmplify/deployment-success.jpg)

### Kết quả

Trang web đã có thể truy cập công khai tại: https://main.d37atxjbyyp60m.amplifyapp.com/


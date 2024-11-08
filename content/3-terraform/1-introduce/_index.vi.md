+++
title = "Giới thiệu về hạ tầng"
date = 2024
weight = 1
chapter = false
pre = "<b>3.1. </b>"
+++

#### Hạ tầng Terraform

Như đã giới thiệu từ trước, Terraform cho phép cấu hình hạ tầng đám mây trên AWS một cách tự động và có tổ chức. Và template được mình chuẩn bị dưới đây, đã viết sẵn code để triển khai hạ tầng và cáu trúc của template như sau:

- Có 4 file chính được thực hiện xuyên suốt trong cấu hình và thiết lập dịch vụ là:
  - **terraform.tf**: Định cấu hình provider, đây là file cơ bản và thường ít thay đổi.
  - **variable.tf**: Lưu trữ các biến, giúp dễ dàng điều chỉnh giá trị cho từng lần triển khai.
  - **main.tf**: Đây là file chính để chạy các chương trình và dịch vụ cho hạ tầng đã được cấu hình.
  - **output.tf**: Xuất kết quả của các tài nguyên sau khi triển khai, giúp tận dụng lại các giá trị này cho mục đích khác.

- Thư mục **modules** sẽ chứa các cấu hình của từng dịch vụ.
- Các file **.tf** nằm ngoài thư mục **modules** sẽ tổng hợp các dịch vụ lại, cho phép triển khai đồng bộ và tối ưu hóa quá trình.
- Link template: https://github.com/LyHoangViet/Terraform-DoAn.git

{{% notice tip %}}
Để hiểu rõ hơn về các phần ở trong template mình đã viết sẵn, mình khuyên các bạn nên xem qua khóa học Terraform ở trên [KodeKloud](https://learn.kodekloud.com/courses/terraform-basics-training-course) và tự viết cho mình một hạ tầng mới có thể tham khảo thêm về hạ tầng của template này.
{{% /notice %}}

![image](/images/3-terraform/3.1.1.png)

- Bạn có thể đọc file README để biến thêm thông tin về hạ tầng này.
- Cài đặt các công cụ cần thiết như đã hướng dẫn.

![image](/images/3-terraform/3.1.2.png)

- Các biến cần sửa trong file ở local.

![image](/images/3-terraform/3.1.3.png)

- Cách deploy bàng các lệnh terraform.

![image](/images/3-terraform/3.1.4.png)

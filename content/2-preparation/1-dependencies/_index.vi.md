+++
title = "Chuẩn bị các phụ thuộc"
date = 2024
weight = 1
chapter = false
pre = "<b>2.1. </b>"
+++

#### Kiến thức cốt lõi

Để chuẩn bị tốt hơn cho Workshop này, bạn nên tham khảo ba bài tập trong **AWS Study Group**:

- [Deploy Application on Docker Container](https://000015.awsstudygroup.com/).
- [Deploy applications on Amazon Elastic Container Service](https://000016.awsstudygroup.com/).
- [Deploying CI/CD with ECS Container](https://000017.awsstudygroup.com/)

Khi các bạn hoàn thành tốt những bài trên, sẽ giúp các bạn có thể nắm rõ:

- Cách triển khai hạ tầng trên AWS.
- Sử dụng RDS để quản lý database.
- Tạo ECS để chạy container cho ứng dụng.
- Sử dụng Application Load Balancer để phân phối tải đồng đều.
- Thiết lập CI/CD để tự động hóa việc cập nhật và triển khai ứng dụng.
- Theo dõi và giám sát hiệu suất của các quy trình.

Sau khi đã hiểu rõ các thành phần trên, các bạn sẽ đến với cách để triển khai hạ tầng một cách nhanh chóng chỉ bằng vài dòng lệnh khi sử dụng Terraform. Bây giờ, hãy cùng bắt đầu Workshop và khám phá từng bước nhé!

#### Cài đặt các phụ thuộc

Để bắt đầu chạy mã trong Terraform, bạn cần:

- **Cài đặt Terraform CLI**: Công cụ dòng lệnh này giúp bạn quản lý và triển khai hạ tầng dưới dạng mã.
- **Cài đặt AWS CLI**: Công cụ này cho phép Terraform tương tác trực tiếp với các dịch vụ AWS, giúp dễ dàng quản lý tài nguyên trên đám mây.

{{% notice note %}}
Hãy chọn phiên bản phù hợp với hệ điều hành của bạn. Bạn có thể tham khảo hướng dẫn chi tiết cách cài đặt trong video dưới đây.
{{% /notice %}}

{{< youtube QbeNsbdZH5k >}}
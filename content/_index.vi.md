+++
title = "Triển khai hạ tầng Terraform tích hợp với GitHub Action"
date = 2024
weight = 1
chapter = false
+++

# Hạ tầng Terraform tích hợp với GitHub Action

#### Kiến trúc

{{< iframe src="/images/Terraform-WS.drawio.html" >}}

#### Quy trình

Để thực hiện bài Workshop này, chung ta có một quy trình đơn giản như sau: 

- Viết một hạ tầng Terraform cho hệ thống sẵn.
- Dùng lệnh để chạy hạ tầng lên AWS console.
- Triển khai ECS Service trên hạ tầng đã được tạo sẵn
- Triển khai CI/CD để tự động hóa quá trình.
- Tạo Monitoring để giám sát quá trình.

Quy trình này đảm bảo việc triển khai hạ tầng, dịch vụ và CI/CD được tự động hóa, mang lại hiệu quả cao và khả năng kiểm soát toàn diện cho hệ thống trên AWS.

#### Nội dung chính

1. [Giới thiệu](1-introduce/)
2. [Chuẩn bị](2-preparation/)
3. [Hạ tầng Terraform](3-terraform/)
4. [Thêm cơ sở dư liệu vào RDS](4-database/)
5. [Tạo ECS Service](5-ecs-service/)
6. [Kiểm tra kết quả](6-result/)
7. [Triển khai CI/CD với GitHub Action](7-cicd-github/)
8. [Giám sát](8-monitoring/)
9. [Dọn dẹp tài nguyên](9-clean-up/)
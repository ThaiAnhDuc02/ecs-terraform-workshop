+++
title = "Chạy lệnh Terraform"
date = 2024
weight = 4
chapter = false
pre = "<b>3.4. </b>"
+++

#### Run Command

Bây giờ, mình sẽ chạy lệnh để triển khai các hạ tầng đã được cấu hình này lên trên hạ tầng AWS.

- Chạy lệnh để khởi tạo hạ tầng.

```
terraform init
```

![image](/images/3-terraform/3.4.1.png)

- Dùng lệnh tiếp theo để theo dõi trước những thay đổi trong hạ tầng sẽ được áp dụng.

```
terraform plan
```

![image](/images/3-terraform/3.4.2.png)

- Lệnh cuối cùng dùng để áp dụng các hạ tầng đã cấu hình lên AWS.

```
terraform apply
```

- Nhập `yes`.

![image](/images/3-terraform/3.4.3.png)

- Đợi khoảng 15 đến 20 phút để hạ tầng được tạo hoàn tất.

![image](/images/3-terraform/3.4.4.png)

#### Kiểm tra kết quả

Sau khi chạy hoàn tất, chúng ta sẽ vào AWS console để kiểm tra trên giao diện xem các hạ tầng đã được tạo hoàn tất chưa.

- Vào kiểm tra bên trong **VPC**.

![image](/images/3-terraform/3.5.1.png)

- Kiểm tra ở **EC2 instance**.

![image](/images/3-terraform/3.5.2.png)

- Truy cập vào **RDS**.

![image](/images/3-terraform/3.5.3.png)

- Kiểm tra **ECS cluster**.

![image](/images/3-terraform/3.5.4.png)

- Kiểm tra **Task definition**.

![image](/images/3-terraform/3.5.5.png)

- Kiểm tra các dịch vụ ở **Cloud Map**.

![image](/images/3-terraform/3.5.6.png)

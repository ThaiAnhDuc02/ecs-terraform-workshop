+++
title = "Triển khai Rolling với Frontend"
date = 2024
weight = 2
chapter = false
pre = "<b>5.2. </b>"
+++

#### Tạo ECS Service Frontend

Tương tự như Sevice ở bên Backend, bây giờ chúng ta sẽ tạo ở bên Frontend.

- Chọn **Launch type** là **FARGATE**.
- Version chọn **LATEST**.

![image](/images/5-ecs-service/5.2.1.png)

- Chọn type là **Service**.
- **Family** chọn **Task definition** đã tạo cho frontend và chọn **version** mới nhất.
- Nhập tên: `frontend`

![image](/images/5-ecs-service/5.2.2.png)

- Chọn type là **Replica** và chọn 1 task để khởi chạy.
- Khác với backend phần sau của frontend để chạy mặc định là **Rolling**.

![image](/images/5-ecs-service/5.2.3.png)

#### Networking

Giờ thì mình sẽ gán Service này và các container vào trong vùng mạng, subnet mà mình đã tạo sẵn bằng hạ tầng Terraform.

- VPC: Chọn **VPC** mà chúng ta đã tạo trước đó
- Subnet: Chọn private subnet (**DoAn-network-subnet-private3**) mà chúng ta đã tạo trong phần chuẩn bị
- Security group: Chọn **DoAn-network-sg-private**.
- Public ip: Phần này sẽ tắt để tăng tính bảo mật hơn vì traffic đã được truyền thông qua **Load Balancer** rồi.

![image](/images/5-ecs-service/5.2.4.png)

#### Load balancing

Cấu hình một số thông tin của Load Balancer như sau:

- Load balancing type: chọn **Application Load Balancer**.
- Container: **frontend 80:80** (port ở đây sẽ là port của host và container).
- Chọn **Use an existing load balancer**.
- Chọn **Doan-alb** load balance.
- Health check grace period: **30**.

![image](/images/5-ecs-service/5.2.5.png)

Trong phần listener, chúng ta sẽ tạo ra listener đã tạo trước đó ở **Terraform**.

- Chọn **Use an existing listener**, chọn **80:HTTP**

Target group, chọn target group mà mình đã tạo ở tại **Terraform**.

- Chọn **Use an existing target group**, chọn **my-tg**

![image](/images/5-ecs-service/5.2.6.png)

Kiểm tra lại cấu hình và chọn **Create**.

![image](/images/5-ecs-service/5.2.7.png)

- Đợi khoảng 5 phút để service được tạo hoàn tất.

![image](/images/5-ecs-service/5.2.8.png)

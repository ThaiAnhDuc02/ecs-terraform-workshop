+++
title = "Triển khai Blue/Green và Service Scaling với Backend"
date = 2024
weight = 1
chapter = false
pre = "<b>5.1. </b>"
+++

#### Tạo ECS Service Backend

Bây giờ, chúng ta cần phải tạo ECS service để chạy các container ở trong đó.

- Tìm kiếm từ khóa `ECS` trong **AWS Console**.
- Chọn **Cluster** mình đã tạo.
- Kéo xuống phần **Service** và chọn **Create**.

![image](/images/5-ecs-service/5.1.1.png)

Chúng ta sẽ cấu hình FARGATE để dễ dàng sử dụng hơn.

- Chọn **Launch type** là **FARGATE**.
- **Version** chọn **LATEST**.

![image](/images/5-ecs-service/5.1.2.png)

- Chọn type là **Service**.
- **Family** chọn **Task definition** đã tạo cho backend và chọn **version** mới nhất.
- Nhập tên: `backend`

![image](/images/5-ecs-service/5.1.3.png)

- Chọn type là **Replica** và chọn 1 task để khởi chạy.
- Chọn deploy bằng **Blue/Green**.
- Chọn cấu hình deploy là **CodeDeployDefault.ECSCanary10Percent5Minutes**
- Phần Role chọn role đã tạo ở phần chuẩn bị `CodeDeployServiceRole`. 

![image](/images/5-ecs-service/5.1.4.png)

#### Service discovery

Phần này quan trọng, để cho Frontend Service và Backend Service thì chúng ta phải cấu hình **Service discovery** cho Backend Service với namespace và serivce đã tạo trong phần **Cloud Map** (Đã được cấu hình bằng **Terraform**).

- Chọn **Use service discovery**.
- Chọn **Select an existing namespace**, chọn namespace **fcjresbar.internal** mà chúng ta đã được tạo trước đó.
- Chọn **Select an existing service discovery service**, chọn service **backend**.
- Các cấu hình còn lại để mặc định.

![image](/images/5-ecs-service/5.1.5.png)

#### Networking

Giờ thì mình sẽ gán Service này và các container vào trong vùng mạng, subnet mà mình đã tạo sẵn bằng hạ tầng **Terraform**.

- VPC: Chọn **VPC** mà chúng ta đã tạo trước đó
- Subnet: Chọn private subnet (**DoAn-network-subnet-private4**) mà chúng ta đã tạo trong phần chuẩn bị
- Security group: Chọn **DoAn-network-sg-private**.
- Public ip: Phần này sẽ tắt để tăng tính bảo mật hơn vì traffic đã được truyền thông qua **Load Balancer** rồi. 

![image](/images/5-ecs-service/5.1.6.png)

#### Load Balancing

Cấu hình một số thông tin của Load Balancer như sau:

- Load balancing type: Chọn **Application Load Balancer**
- Container: **backend 5000:5000** (port ở đây sẽ là port của host và container)
- Chọn **Use an existing load balancer**
- Chọn **Doan-alb** load balancer
- Health Check: Giữ mặc định.

![image](/images/5-ecs-service/5.1.7.png)

Phần Listener ta sẽ tạo mới 2 Listener.

- Production listener: port **5000**, protocol **HTTP**
- Test listener: port **8080**, protocol **HTTP**

![image](/images/5-ecs-service/5.1.8.png)

Phần của **target group** sẽ được giữ mặc định hoặc cấu hình theo ý muốn.

![image](/images/5-ecs-service/5.1.9.png)

![image](/images/5-ecs-service/5.1.10.png)

#### Service auto scaling

Giờ thì mình sẽ cấu hình scaling cho container

- Minimun: 1
- Maximun: 2
- Scaling policy type: **Target tracking**

![image](/images/5-ecs-service/5.1.11.png)

Cấu hình chính sách cho scaling

- Name: `ScaleAtThreshold75Percent`
- ECS service metric: **ECSServiceAverageCPUUtilization**
- Target value: **75**
- Scale-out cooldown period: **120**
- Scale-in cooldown period: **120**
- Và ấn **Create** để tạo

![image](/images/5-ecs-service/5.1.12.png)

Chúng ta cần phải đợi khoảng 5 phút để cho Service được tạo hoàn tất.

![image](/images/5-ecs-service/5.1.13.png)

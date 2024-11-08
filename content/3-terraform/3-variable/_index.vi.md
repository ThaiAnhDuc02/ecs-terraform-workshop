+++
title = "Chỉnh sửa các biến"
date = 2024
weight = 3
chapter = false
pre = "<b>3.3. </b>"
+++

#### Giải thích về các biến

Để hiểu rõ hơn về các biến trong hạ tầng Terraform này, bạn có thể xem xét đoạn mã dưới đây cùng với phần ghi chú chi tiết.

```
# Setup local variables
locals {
  region = "ca-central-1"                               # Region mà bạn hiện đang sử dụng
  author = "DoAn"                                       # Tên của người sử dụng hoặc là dự án
  network_root_name = "DoAn-network"                    # Tên của VPC
  vpc_cidr = "10.0.0.0/16"                              # Địa chỉ chính của VPC hạ tầng mạng ảo của bạn
  compute_root_name = "DoAn-compute"                    # Tên của EC2 instance
  key_name = "test-terraform"                           # Tên của Key pair mình đã tạo ở phần chuẩn bị
  
  # RDS database
  db_username = "admin"                                 # Tên của user name trong RDS
  db_password = "DoAn123456"                            # Password của database
  db_name = "Doandb"                                    # Tên của RDS instance
  
  # Cloud Map
  service_discovery_namespace_name = "fcjresbar.internal"   # Tên namespace của cloud map
  service_discovery_service_name = "backend"                # Tên dịch vụ bên trong namespace
  
  # Load Balancer
  target_group_name = "my-tg"                           # Tên của target group
  alb_name = "Doan-alb"                                 # Tên của ALB
  
  # Task definition of backend
  backend_family = "fcjresbar-task-be"                  # Tên của task definition backend
  backend_image = "lyhoangviet/backend:v1.0.2"          # Link image ở trên docker hub của backend
  mysql_database = "fcjresbar"                          # Tên của database đã tạo
  db_dialect = "mysql"                                  # dùng để xác định loại cơ sở dữ liệu
  be_port = "5000"                                      # Port của backend
  jwt_secret = "0bac010eca699c25c8f62ba86e319c2305beb94641b859c32518cb854addb5f4" # Secret key dùng để mã hóa xác thực 

  # Task definition of frontend
  frontend_family = "fcjresbar-task-fe"                 # Tên của task definition frontend
  frontend_image = "lyhoangviet/frontend:v1.0.2"        # Link image ở trên docker hub của frontend
  be_host = "backend.fcjresbar.internal"                # Tên được ánh xạ từ Cloud map
  

  ec2_instances = [
    {
      name               = "server_test"                # Tên đằng sau của EC2 instance
      ami                = "ami-0eb9fdcf0d07bd5ef"      # Ubuntu Server 24.04 LTS
      instance_type      = "t3.medium"                  # Loại instance muốn sử dụng
      subnet_id          = module.infrastructure_vpc.subnet_public1_id    # Subnet được tạo ở VPC
      security_group_ids = [module.security.public_sg_id]                 # Security group được tạo ở SG
    },
  ]
}
```

{{% notice note %}}
Lưu ý: Các biến trên để có thể hoạt động tốt, bạn cần phải thay đổi đúng theo các thông số cấu hình của bạn.
{{% /notice %}}

- Đường dẫn tới code

```
vi .\Terraform-DoAn\deploy-infrastructure-ecs\variable.tf
```

![image](/images/3-terraform/3.3.1.png)

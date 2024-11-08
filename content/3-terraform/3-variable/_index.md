+++
title = "Edit Variables"
date = 2024
weight = 3
chapter = false
pre = "<b>3.3. </b>"
+++

#### Explanation of Variables

To better understand the variables in this Terraform infrastructure, you can review the code snippet below along with detailed annotations.

```
# Setup local variables
locals {
  region = "ca-central-1"                               # The region you are currently using
  author = "DoAn"                                       # Name of the user or the project
  network_root_name = "DoAn-network"                    # Name of the VPC
  vpc_cidr = "10.0.0.0/16"                              # Primary CIDR block for your VPC virtual network infrastructure
  compute_root_name = "DoAn-compute"                    # Name of the EC2 instance
  key_name = "test-terraform"                           # Name of the Key pair created in the setup stage
  
  # RDS database
  db_username = "admin"                                 # Username for RDS
  db_password = "DoAn123456"                            # Database password
  db_name = "Doandb"                                    # Name of the RDS instance
  
  # Cloud Map
  service_discovery_namespace_name = "fcjresbar.internal"   # Cloud Map namespace name
  service_discovery_service_name = "backend"                # Service name within the namespace
  
  # Load Balancer
  target_group_name = "my-tg"                           # Name of the target group
  alb_name = "Doan-alb"                                 # Name of the ALB
  
  # Task definition of backend
  backend_family = "fcjresbar-task-be"                  # Name of the backend task definition
  backend_image = "lyhoangviet/backend:v1.0.2"          # Link to the backend image on Docker Hub
  mysql_database = "fcjresbar"                          # Name of the created database
  db_dialect = "mysql"                                  # Specifies the type of database
  be_port = "5000"                                      # Backend port
  jwt_secret = "0bac010eca699c25c8f62ba86e319c2305beb94641b859c32518cb854addb5f4" # Secret key used for authentication encryption

  # Task definition of frontend
  frontend_family = "fcjresbar-task-fe"                 # Name of the frontend task definition
  frontend_image = "lyhoangviet/frontend:v1.0.2"        # Link to the frontend image on Docker Hub
  be_host = "backend.fcjresbar.internal"                # Mapped name from Cloud Map
  

  ec2_instances = [
    {
      name               = "server_test"                # Name of the EC2 instance
      ami                = "ami-0eb9fdcf0d07bd5ef"      # Ubuntu Server 24.04 LTS
      instance_type      = "t3.medium"                  # Type of instance to use
      subnet_id          = module.infrastructure_vpc.subnet_public1_id    # Subnet created in VPC
      security_group_ids = [module.security.public_sg_id]                 # Security group created in SG
    },
  ]
}
```

{{% notice note %}}
Note: To function correctly, the above variables should be modified according to your specific configuration parameters.
{{% /notice %}}

- Path to code

```
vi .\Terraform-DoAn\deploy-infrastructure-ecs\variable.tf
```

![image](/images/3-terraform/3.3.1.png)

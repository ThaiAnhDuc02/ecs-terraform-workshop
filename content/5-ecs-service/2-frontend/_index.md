+++
title = "Rolling Deployment with Frontend"
date = 2024
weight = 2
chapter = false
pre = "<b>5.2. </b>"
+++

#### Create ECS Frontend Service

Similar to the Backend Service, we now need to create the Frontend Service.

- Choose **Launch type** as **FARGATE**.
- Set **Version** to **LATEST**.

![image](/images/5-ecs-service/5.2.1.png)

- Select type as **Service**.
- For **Family**, choose the **Task definition** created for the frontend and select the latest **version**.
- Enter name: `frontend`

![image](/images/5-ecs-service/5.2.2.png)

- Set type as **Replica** and select 1 task to launch.
- Unlike the backend, the frontend will run by default in **Rolling** mode.

![image](/images/5-ecs-service/5.2.3.png)

#### Networking

Now, we will assign this Service and its containers to the network area and subnet we previously created using Terraform.

- **VPC**: Select the **VPC** created earlier.
- **Subnet**: Select the private subnet (**DoAn-network-subnet-private3**) created in the preparation phase.
- **Security group**: Select **DoAn-network-sg-private**.
- **Public IP**: Disable this setting to enhance security since traffic is already routed through the **Load Balancer**.

![image](/images/5-ecs-service/5.2.4.png)

#### Load Balancing

Configure some information for the Load Balancer as follows:

- **Load balancing type**: Choose **Application Load Balancer**.
- **Container**: Select **frontend 80:80** (port here refers to the host and container port).
- Choose **Use an existing load balancer**.
- Select **Doan-alb** load balancer.
- **Health check grace period**: Set to **30**.

![image](/images/5-ecs-service/5.2.5.png)

In the listener section, we’ll select the listener created earlier in **Terraform**.

- Choose **Use an existing listener** and select **80:HTTP**.

For the target group, select the target group previously created in **Terraform**.

- Choose **Use an existing target group** and select **my-tg**.

![image](/images/5-ecs-service/5.2.6.png)

Review the configuration and select **Create**.

![image](/images/5-ecs-service/5.2.7.png)

- Wait approximately 5 minutes for the service to be fully created.

![image](/images/5-ecs-service/5.2.8.png)

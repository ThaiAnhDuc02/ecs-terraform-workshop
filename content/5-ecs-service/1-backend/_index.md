+++
title = "Deploying Blue/Green and Service Scaling with Backend"
date = 2024
weight = 1
chapter = false
pre = "<b>5.1. </b>"
+++

#### Creating ECS Service

Now, we need to create an ECS service to run our containers.

- Search for the keyword `ECS` in the **AWS Console**.
- Select the **Cluster** that you've created.
- Scroll down to the **Service** section and choose **Create**.

![image](/images/5-ecs-service/5.1.1.png)

We’ll configure FARGATE for easier usage.

- Choose **Launch type** as **FARGATE**.
- **Version** select **LATEST**.

![image](/images/5-ecs-service/5.1.2.png)

- Choose type as **Service**.
- **Family** select the **Task definition** created for the backend and choose the latest **version**.
- Enter name: `backend`

![image](/images/5-ecs-service/5.1.3.png)

- Choose type as **Replica** and select 1 task to launch.
- Select deployment type as **Blue/Green**.
- Select deployment configuration as **CodeDeployDefault.ECSCanary10Percent5Minutes**.
- In the Role section, choose the role created in the preparation step: `CodeDeployServiceRole`.

![image](/images/5-ecs-service/5.1.4.png)

#### Service Discovery

This part is important. For the Frontend Service and Backend Service to communicate, we need to configure **Service discovery** for the Backend Service with the namespace and service created in **Cloud Map** (configured with **Terraform**).

- Select **Use service discovery**.
- Choose **Select an existing namespace** and select the namespace **fcjresbar.internal** that was created previously.
- Choose **Select an existing service discovery service** and select the **backend** service.
- Leave other configurations as default.

![image](/images/5-ecs-service/5.1.5.png)

#### Networking

Now, we’ll assign this Service and its containers to the network and subnet that we previously created using **Terraform**.

- VPC: Choose the **VPC** that we created earlier.
- Subnet: Choose the private subnet (**DoAn-network-subnet-private4**) created in the preparation step.
- Security group: Select **DoAn-network-sg-private**.
- Public IP: This option will be disabled to enhance security as traffic is already routed through the **Load Balancer**.

![image](/images/5-ecs-service/5.1.6.png)

#### Load Balancing

Configure some information for the Load Balancer as follows:

- Load balancing type: Choose **Application Load Balancer**.
- Container: **backend 5000:5000** (this port is for both the host and the container).
- Choose **Use an existing load balancer**.
- Select **Doan-alb** load balancer.
- Health Check: Keep it as default.

![image](/images/5-ecs-service/5.1.7.png)

In the Listener section, we’ll create 2 new Listeners.

- Production listener: port **5000**, protocol **HTTP**.
- Test listener: port **8080**, protocol **HTTP**.

![image](/images/5-ecs-service/5.1.8.png)

The **target group** section can be kept as default or configured as desired.

![image](/images/5-ecs-service/5.1.9.png)

![image](/images/5-ecs-service/5.1.10.png)

#### Service Auto Scaling

Now, we’ll configure scaling for the container.

- Minimum: 1
- Maximum: 2
- Scaling policy type: **Target tracking**

![image](/images/5-ecs-service/5.1.11.png)

Configure the scaling policy:

- Name: `ScaleAtThreshold75Percent`
- ECS service metric: **ECSServiceAverageCPUUtilization**
- Target value: **75**
- Scale-out cooldown period: **120**
- Scale-in cooldown period: **120**
- Then click **Create** to finish.

![image](/images/5-ecs-service/5.1.12.png)

We need to wait about 5 minutes for the Service to be fully created.

![image](/images/5-ecs-service/5.1.13.png)

+++
title = "Run Terraform Command"
date = 2024
weight = 4
chapter = false
pre = "<b>3.4. </b>"
+++

#### Run Command

Now, I will run the command to deploy the configured infrastructure on AWS.

- Run the command to initialize the infrastructure.

```
terraform init
```
![image](/images/3-terraform/3.4.1.png)

- Use the next command to preview the changes that will be applied to the infrastructure.

```
terraform plan
```

![image](/images/3-terraform/3.4.2.png)

- The final command is used to apply the configured infrastructure to AWS.

```
terraform apply
```

- Type `yes`.

![image](/images/3-terraform/3.4.3.png)

- Wait about 15 to 20 minutes for the infrastructure to be fully created.

![image](/images/3-terraform/3.4.4.png)

#### Check the Results

After the process is complete, we will go to the AWS console to check the interface to see if the infrastructure has been fully created.

- Check inside **VPC**.

![image](/images/3-terraform/3.5.1.png)

- Check in **EC2 instance**.

![image](/images/3-terraform/3.5.2.png)

- Access **RDS**.

![image](/images/3-terraform/3.5.3.png)

- Check **ECS cluster**.

![image](/images/3-terraform/3.5.4.png)

- Check **Task definition**.

![image](/images/3-terraform/3.5.5.png)

- Check the services in **Cloud Map**.

![image](/images/3-terraform/3.5.6.png)

+++
title = "Git clone template"
date = 2024
weight = 2
chapter = false
pre = "<b>3.2. </b>"
+++

#### Clone template

As noted in the [Preparation](/2-preparation) section, you need to have the required dependencies installed on your machine, and you can use [Visual Studio Code](https://code.visualstudio.com/download) for easier folder management.

- Use the command below to check if Git is installed.

```
git -v
```

![image](/images/3-terraform/3.2.1.png)

- Next, clone the repository to run the code.

```
git clone https://github.com/ThaiAnhDuc02/ecs-terraform.git
cd .\Terraform-DoAn\deploy-infrastructure-ecs\
```

![image](/images/3-terraform/3.2.2.png)

- Log in to AWS CLI

```
aws --version
aws configure
```

![image](/images/3-terraform/3.2.3.png)

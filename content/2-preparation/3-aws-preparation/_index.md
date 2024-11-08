+++
title = "Creating Access Key, Role, and Key Pair"
date = 2024
weight = 3
chapter = false
pre = "<b>2.3. </b>"
+++

#### Creating an Access Key

First, we need to create an Access Key to access the AWS console via the Command Line Interface (CLI). This Access Key will enable us to manage and interact with AWS services easily from the command line.

- Go to the **AWS Console** and search for `IAM`.
- Select the **User** you are currently using.
- Go to **Security credentials**, scroll down, and choose **Create access key**.

![image](/images/2-preparation/2.1.png)

- Select **Command Line Interface (CLI)**.

![image](/images/2-preparation/2.2.png)

- Check the **Confirmation** box and click **Next**.

![image](/images/2-preparation/2.3.png)

- Click **Create access key**.

![image](/images/2-preparation/2.4.png)

- Complete the creation of the access key and download the **file** containing the access key.
- Select **Done** to finish.

![image](/images/2-preparation/2.5.png)

#### Creating a Role

Next, we will create a Role to grant permissions for the ECS service that we will use later.

- Select **Roles** and click **Create role**.

![image](/images/2-preparation/2.6.png)

- Choose **AWS service** as the type.
- Select **CodeDeploy** as the service.
- Select **CodeDeploy - ECS** as the use case.

![image](/images/2-preparation/2.7.png)

- You will see a pre-created policy.
- Click **Next**.

![image](/images/2-preparation/2.8.png)

- Enter the name: `CodeDeployServiceRole`.
- Enter the description: `Allows CodeDeploy to read S3 objects, invoke Lambda functions, publish to SNS topics, and update ECS services on your behalf.`

![image](/images/2-preparation/2.9.png)

- Review and click **Create role**.

![image](/images/2-preparation/2.10.png)

#### Creating a Key Pair

Create a key pair to use with your EC2 instance.

- In the search bar, enter `Key pair`.
- Select **Key pairs**.

![image](/images/2-preparation/2.11.png)

- Select **Key Pairs**.
- Click **Create key pair**.

![image](/images/2-preparation/2.12.png)

- Enter the name: `terraform-cicd`.
- Select type **RSA**.
- Choose file type **.pem**.
- Click **Create key pair**.

![image](/images/2-preparation/2.13.png)

- The **Key pair** creation is successful.

![image](/images/2-preparation/2.14.png)

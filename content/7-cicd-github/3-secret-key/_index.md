+++
title = "Add Secret Keys"
date = 2024
weight = 3
chapter = false
pre = "<b>7.3. </b>"
+++

#### Create Secret Keys in GitHub

Create secret keys in GitHub to assign these values to variables in the CI/CD pipeline, ensuring it runs correctly.

- Go to the **Settings** of the repository you created in the previous section.
- Select **Secrets and variables** and **Actions** as shown.
- Click **New repository secret** to create a new secret.

![image](/images/7-cicd/7.3.1.png)

- Add the following values as shown below:

  - `AWS_ACCESS_KEY_ID`: Add the access key value you created in AWS.
  - `AWS_SECRET_ACCESS_KEY`: Add the secret key value you created in AWS.
  - `AWS_REGION`: Set this to the region you are using.
  - `AWS_ACCOUNT_NUMBER`: Set this to the account number you are using.
  - `DOCKER_PASSWORD`: Add the password or token from your Docker account.
  - `DOCKER_USERNAME`: Add the username from your Docker account.
  - `CLUSTER_NAME`: Set this to the name of your ECS Cluster.
  - `TASK_NAME_BE`: Set this to the name of the backend task definition.
  - `TASK_NAME_FE`: Set this to the name of the frontend task definition.
  - `SERVICE_NAME_BE`: Set this to the name of the backend service.
  - `SERVICE_NAME_FE`: Set this to the name of the frontend service.
  - `AWS_APPLICATION_NAME`: Set this to the name of the Application in CodeDeploy for the backend.
  - `AWS_DEPLOYMENT_GROUP_NAME`: Set this to the name of the Deployment Group in the backend Application.

![image](/images/7-cicd/7.3.2.png)

{{% notice note %}}
Since this repository is using **Docker Hub** to store images, if you wish to use a different registry like **ECR**, you will need to adjust the variables in the configuration files to match **ECR**.
{{% /notice %}}

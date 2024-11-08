+++
title = "Clone GitHub Template"
date = 2024
weight = 1
chapter = false
pre = "<b>7.1. </b>"
+++

{{% notice tip %}}
In this section, we provide a sample **template** to run CI/CD using **GitHub Actions**. You can refer to and clone this to simplify your setup, making the CI/CD deployment process faster and more efficient. Alternatively, you can configure your own CI/CD section to manage your code more easily.
{{% /notice %}}

#### Clone Source Code from GitHub

You will reuse the EC2 virtual machine from the previous section to clone this code and edit it there. Once you have the code, you can modify it as needed to suit your requirements.

- Use the following command to check and clone the code.
- Then navigate into the folder to edit the code as needed.

```bash
git -v
git clone https://github.com/LyHoangViet/cicd-github-action-ws17.git
ls
cd ./cicd-github-action-ws17/
```

![image](/images/7-cicd/7.1.1.png)

Edit the source code in the next step to create an example of how a CI/CD run in GitHub Actions will be changed.

- Path: **frontend/src/components/Menu.jsx**
- On line 68 in the file, you can edit as shown below (or customize as needed).

![image](/images/7-cicd/7.1.2.png)

#### Code Explanation

First, the main.yml file contains all tasks for the frontend and backend.

- How to access the file:

```
vi .github/workflows/main.yml
```

```
name: CI/CD Pipeline

on:
  push:
    tags:
      - '*'

jobs:
  frontend:
    uses: ./.github/workflows/frontend.yml
    secrets: inherit

  backend:
    uses: ./.github/workflows/backend.yml
    secrets: inherit
```

- Explanation:

  - name: CI/CD Pipeline specifies the workflow structure.
  - on: (...) defines the event that triggers the workflow.
  - jobs: (...) lists the jobs that will run when CI/CD is executed.

Next, the backend.yml and frontend.yml files configure specific jobs for these sections. Since the configurations are similar, we'll focus on the backend.yml file.

- How to access the file:

```
vi .github/workflows/backend.yml
```

```
name: Backend CI/CD

on:
  workflow_call:

# Use Docker Hub
env:
  IMAGE_NAME_BE: ${{ secrets.DOCKER_USERNAME }}/backend:${{ github.ref_name }}

jobs:
  # this comment need when you implement in prod env (1)
  # check_changes_backend:
  #   runs-on: ubuntu-latest
  #   outputs:
  #     backend: ${{ steps.filter.outputs.backend }}
  #   steps:
  #     - uses: actions/checkout@v2
  #     - uses: dorny/paths-filter@v2
  #       id: filter
  #       with:
  #         filters: |
  #           backend:
  #             - 'backend/**'

  build-and-push:
    # this comment need when you implement in prod env (1)
    # needs: check_changes_backend
    # if: ${{ needs.check_changes_backend.outputs.backend == 'true' }} 
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v1
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ${{ secrets.AWS_REGION }}

      # Use Docker Hub
      - name: Login to Docker Hub
        uses: docker/login-action@v2
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}

      - name: Build, tag, and push image to Amazon ECR
        working-directory: ./backend
        run: |
          docker build -f Dockerfile -t ${{ env.IMAGE_NAME_BE }} .
          docker push ${{ env.IMAGE_NAME_BE }}

  deploy:
    needs: build-and-push
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v1
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ${{ secrets.AWS_REGION }}

      - name: Deploy Backend
        env:
          TASK_NAME_BE: ${{ secrets.TASK_NAME_BE }}
          IMAGE_NAME_BE: ${{ env.IMAGE_NAME_BE }}
          AWS_APPLICATION_NAME: ${{ secrets.AWS_APPLICATION_NAME }}
          AWS_DEPLOYMENT_GROUP_NAME: ${{ secrets.AWS_DEPLOYMENT_GROUP_NAME }}
          REGION: ${{ secrets.AWS_REGION }}
        run: bash backend/deploy-backend.sh
```

- Explanation:
  - name: Backend CI/CD is the workflow name.
  - on: (...) triggers the workflow, allowing it to call other workflows.
  - env: (...) defines environment variables for the image (currently using Docker Hub, but can be switched to ECR).
  - build-and-push: (...) is a job within the main jobs section, used to build an image and push it to Docker Hub.
  - deploy: (...) is the second job, used to deploy the image to ECS.
  - run: bash backend/deploy-backend.sh points to the deployment file.

Finally, access the deploy-backend.sh file (or deploy-frontend.sh for the frontend) to configure code for ECS deployment.

- How to access the file:

```
vi backend/deploy-backend.sh
```

```
#!/bin/bash
# Retrieve the task definition from ECS
TASK_DEFINITION=$(aws ecs describe-task-definition --task-definition "$TASK_NAME_BE" --region "$REGION")

# Register a new task definition with an updated image
NEW_TASK_DEFINITION=$(echo $TASK_DEFINITION | jq --arg IMAGE "$IMAGE_NAME_BE" '.taskDefinition | .containerDefinitions[0].image = $IMAGE | del(.taskDefinitionArn) | del(.revision) | del(.status) | del(.requiresAttributes) | del(.compatibilities) | del(.registeredAt) | del(.registeredBy)')
NEW_REVISION=$(aws ecs register-task-definition --region "$REGION" --cli-input-json "$NEW_TASK_DEFINITION")
echo $NEW_REVISION | jq '.taskDefinition.revision'


# Extract the task definition ARN, container name, and container port using jq
AWS_TASK_DEFINITION_ARN=$(echo $TASK_DEFINITION | jq -r '.taskDefinition.taskDefinitionArn')
CONTAINER_NAME=$(echo $TASK_DEFINITION | jq -r '.taskDefinition.containerDefinitions[0].name')
CONTAINER_PORT=$(echo $TASK_DEFINITION | jq -r '.taskDefinition.containerDefinitions[0].portMappings[0].containerPort')

# Create the application specification (AppSpec) in JSON format
APP_SPEC=$(jq -n --arg taskDef "$AWS_TASK_DEFINITION_ARN" --arg containerName "$CONTAINER_NAME" --argjson containerPort "$CONTAINER_PORT" '{
  version: "0.0",
  Resources: [
    {
      TargetService: {
        Type: "AWS::ECS::Service",
        Properties: {
          TaskDefinition: $taskDef,
          LoadBalancerInfo: {
            ContainerName: $containerName,
            ContainerPort: $containerPort
          }
        }
      }
    }
  ]
}')

# Create the revision configuration for the deployment
REVISION=$(jq -n --arg appSpec "$APP_SPEC" '{
  revisionType: "AppSpecContent",
  appSpecContent: {
    content: $appSpec
  }
}')

# Trigger the deployment using the specified application name, deployment group, and revision
aws deploy create-deployment --region "$REGION" \
  --application-name "$AWS_APPLICATION_NAME" \
  --deployment-group-name "$AWS_DEPLOYMENT_GROUP_NAME" \
  --revision "$REVISION"
```

- Results:
  - The ECS task definition is updated with the new image.
  - CodeDeploy triggers a deployment with the updated configuration, synchronizing the application with the new backend image in the existing ECS service.
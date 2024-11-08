+++
title = "Clone GitHub template"
date = 2024
weight = 1
chapter = false
pre = "<b>7.1. </b>"
+++

{{% notice tip %}}
Trong phần này, chúng tôi cung cấp sẵn một **template** mẫu để chạy CI/CD bằng **GitHub Actions**. Bạn có thể tham khảo và clone về để dễ dàng hơn trong việc thiết lập và sử dụng, giúp quá trình triển khai CI/CD trở nên nhanh chóng và hiệu quả hơn. Ngoài ra bạn có thể tự cấu hình phần CI/CD của mình để quản lý code của mình dễ dàng hơn.
{{% /notice %}}

#### Git clone mã nguồn trên GitHub

Bạn sẽ sử dụng lại máy ảo EC2 ở phần trước để clone code này về và chỉnh sửa trong nó. Sau khi đã có code, bạn có thể chỉnh sửa theo yêu cầu của bạn cho phù hợp.

- Sử dụng lệnh sau để kiểm tra và clone code.
- Sau đó truy cập vào trong folder để sửa code theo yêu cầu.

```
git -v
git clone https://github.com/LyHoangViet/cicd-github-action-ws17.git
ls
cd ./cicd-github-action-ws17/
```

![image](/images/7-cicd/7.1.1.png)

Chỉnh sửa lại source code ở phần sau để có thể làm ví dụ khi run một CI/CD trong Github action sẽ được thay đổi.

- Đường dẫn: **frontend/src/components/Menu.jsx**
- Dòng 68 ở trong file, mình có thể sửa như ở dưới (hoặc sửa theo ý muốn tùy vào yêu cầu).

![image](/images/7-cicd/7.1.2.png)

#### Giải thích code

Đầu tiên sẽ là file main.yml sẽ chứa tất cả những công việc của frontend và backend.

- Cách truy cập vào file:

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

- Trong đó:

  - name: CI/CD Pipeline là cấu trúc của workflow
  - on: (…) là sự kiện kích hoạt workflow
  - jobs: (…) là những jobs sẽ được hoạt động khi run CI/CD

Tiếp theo sẽ là file backend.yml và file frontend.yml là nơi sẽ cấu hình jobs cụ thể 2 phần này. Bởi vì cấu hình cũng khá giống nhau nên mình xin phép hướng dẫn một file là file backend.yml

- Cách truy cập vào file:

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

- Trong đó:
  - name: Backend CI/CD là tên cấu trúc của workflow.
  - on: (…) là sự kiện kích hoạt workflow cho phép gọi tới workflow khác.
  - env: (…) dùng để định nghĩa các biến môi trường cho image (hiện đang dùng cho Docker hub có thể đổi qua ECR).
  - build-and-push: (…) là một workflow trong jobs chính, sử dụng để build một image và push lên Docker hub.
  - deploy: (…) là một jobs thứ 2 dùng để deploy image vừa được build lên ECS.
  - run: bash backend/deploy-backend.sh phần cuối này sẽ dẫn đên file dùng để deploy.

Cuối cùng mình sẽ cần phải truy cập vào file deploy-backend.sh hoặc ở bên frontend là file deploy-frontend.sh để cấu hình code khi deploy ECS.

- Cách truy cập vào file:

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

- Kết quả:
  - Task definition ECS được cập nhật với image mới.
  - CodeDeploy kích hoạt deployment với cấu hình mới, đồng bộ hóa ứng dụng với image backend mới trong service ECS hiện có.
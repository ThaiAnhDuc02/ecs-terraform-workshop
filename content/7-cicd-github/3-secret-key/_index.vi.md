+++
title = "Thêm Secret key"
date = 2024
weight = 3
chapter = false
pre = "<b>7.3. </b>"
+++

#### Tạo secret key trong Github

Tạo secret key cho github để có thể dùng các giá trị này gán vào các biến ở trong CI/CD để nó được hoạt động đúng cách.

- Vào phần **Settings** của repository bạn đã tạo từ phần trước.
- Chọn **Secrets and variables** và **Actions** như hướng dẫn.
- Chọn **New repository secret** để tạo secret.

![image](/images/7-cicd/7.3.1.png)

- Thêm các giá trị như hình sau đây vào:

  - `AWS_ACCESS_KEY_ID` gán giá trị access key vừa tạo trong aws vào.
  - `AWS_SECRET_ACCESS_KEY` gán giá trị secret key vừa tạo trong aws vào.
  - `AWS_REGION` gán giá trị bằng region bạn đang sử dụng.
  - `AWS_ACCOUNT_NUMBER` gán số account của bạn đang sử dụng.
  - `DOCKER_PASSWORD` gán mật khẩu hoặc token ở tài khoản Docker của bạn.
  - `DOCKER_USERNAME` gán username ở tài khoản Docker của bạn.
  - `CLUSTER_NAME` gán giá trị bằng tên Cluster ECS.
  - `TASK_NAME_BE` gán giá trị bằng tên task definition của backend.
  - `TASK_NAME_FE` gán giá trị bằng tên task definition của frontend.
  - `SERVICE_NAME_BE` gán giá trị bằng tên Sevice name của backend.
  - `SERVICE_NAME_FE` gán giá trị bằng tên Sevice name của frontend.
  - `AWS_APPLICATION_NAME` gán giá trị bằng tên Application ở trong CodeDeploy của backend.
  - `AWS_DEPLOYMENT_GROUP_NAME` gán giá trị bằng tên Deployment group ở trong Application của backend.

![image](/images/7-cicd/7.3.2.png)

{{% notice note %}}
Vì repository đang sử dụng **Docker Hub** để chứa images, nếu bạn muốn sử dụng một nơi lưu trữ khác như **ECR**, cần phải chỉnh sửa lại các biến trong file cấu hình để phù hợp với **ECR**.
{{% /notice %}}

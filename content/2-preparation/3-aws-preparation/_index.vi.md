+++
title = "Tạo Access key, Role và Key pair"
date = 2024
weight = 3
chapter = false
pre = "<b>2.3. </b>"
+++

#### Tạo Access key

Trước tiên, chúng ta cần tạo Access Key để có thể truy cập vào AWS console thông qua giao diện dòng lệnh (CLI). Access Key này sẽ cho phép chúng ta quản lý và tương tác với các dịch vụ AWS một cách dễ dàng từ dòng lệnh.

- Truy cập vào **AWS Console** và tìm kiếm từ khóa `IAM`
- Chọn vào **User** hiện đang sử dụng.
- Chọn **Security credentials** và kéo xuống và chọn **Create access key**.

![image](/images/2-preparation/2.1.png)

- Chọn **Command Line Interface (CLI)**.

![image](/images/2-preparation/2.2.png)

- Tích vào ô **Confirmation** và chọn **Next**.

![image](/images/2-preparation/2.3.png)

- Chọn **Create access key**.

![image](/images/2-preparation/2.4.png)

- Hoàn thành tạo access key, tải **file** chứa access key về.
- Chọn **Done** để hoàn tất.

![image](/images/2-preparation/2.5.png)

#### Tạo Role

Tiếp theo sẽ là tạo Role để cấp quyền cho ECS service chúng ta sẽ làm ở phần sau.

- Chọn **Roles** và chọn **Create role**.

![image](/images/2-preparation/2.6.png)

- Chọn type **AWS service**.
- Chọn service là **CodeDeploy**
- Chọn Use case **CodeDeploy - ECS**.

![image](/images/2-preparation/2.7.png)

- Chúng ta sẽ thấy có một policy đã được tạo sẵn.
- Chọn **Next**.

![image](/images/2-preparation/2.8.png)

- Nhập tên: `CodeDeployServiceRole`
- Nhập mô tả: `Allows CodeDeploy to read S3 objects, invoke Lambda functions, publish to SNS topics, and update ECS services on your behalf.`

![image](/images/2-preparation/2.9.png)

- Kiểm tra lại và chọn **Create role**.

![image](/images/2-preparation/2.10.png)

#### Tạo Key pair

Tạo key pair để sử dụng cho máy ảo EC2 instance của bạn.

- Trên thanh tìm kiếm bạn nhập từ khóa `Key pair`
- Chọn **Key pairs**.

![image](/images/2-preparation/2.11.png)

- Chọn **Key Pairs**.
- Chọn **Create key pair**.

![image](/images/2-preparation/2.12.png)

- Nhập tên: `terraform-cicd`
- Chọn type **RSA**.
- Chọn file **.pem**
- Chọn **Create key pair**.

![image](/images/2-preparation/2.13.png)

- Tạo thành công **Key pair**.

![image](/images/2-preparation/2.14.png)

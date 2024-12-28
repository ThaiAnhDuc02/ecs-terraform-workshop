+++
title = "Git clone template"
date = 2024
weight = 2
chapter = false
pre = "<b>3.2. </b>"
+++

#### Clone template

Như đã ghi chú ở phần [Chuẩn bị](/2-preparation) bạn cần phải cài đặt sẵn các dependencies ở trên máy mình, và bạn có thể dùng [Visual Studio Code](https://code.visualstudio.com/download) để dễ dàng hơn trong việc quản lý các thư mục.

- Dùng lệnh để kiểm tra git đã được cài đặt chưa.
```
git -v
```

![image](/images/3-terraform/3.2.1.png)

- Tiếp theo sẽ là clone code về để chạy.
```
git clone https://github.com/LyHoangViet/Terraform-DoAn.git
cd .\Terraform-DoAn\deploy-infrastructure-ecs\
``` 

![image](/images/3-terraform/3.2.2.png)

- Đăng nhập vào AWS CLI
```
aws --version
aws configure
```

![image](/images/3-terraform/3.2.3.png)

+++
title = "Tạo project mới và push code"
date = 2024
weight = 2
chapter = false
pre = "<b>7.2. </b>"
+++

#### Tạo mới repository

Repository này sẽ là nơi để bạn chạy Github Action.

- Đầu tiên là vào tài khoản Github của bạn.
- Chọn **Repositories**.
- Chọn **New**.

![image](/images/7-cicd/7.2.1.png)

- Nhập tên repository: `terraform-cicd`
- Nhập mô tả: `Use to CI/CD`
- Chọn **Public**.
- Chọn **Create repository**.

![image](/images/7-cicd/7.2.2.png)

- Hoàn thành tạo **Repository**.

![image](/images/7-cicd/7.2.3.png)

#### Push code

Truy cập vào máy ảo đã clone và sửa code.

- Dùng lệnh để **remote repo** của bạn.
- Kiểm tra xem đã **remote** thành công chưa.

```
git remote set-url origin "Link repo github"
git remote -v
```

![image](/images/7-cicd/7.2.4.png)

- Dùng lệnh để đẩy code lên repo mới tạo của bạn.

```
git add .
git commit -m "Fist commit"
git branch -M main
git push -u origin main
```

![image](/images/7-cicd/7.2.5.png)

- Kiểm tra lại trong repo trên Github xem code đã được đẩy lên chưa.

![image](/images/7-cicd/7.2.6.png)

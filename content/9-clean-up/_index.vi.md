+++
title = "Dọn dẹp tài nguyên"
date = 2024
weight = 9
chapter = false
pre = "<b>9. </b>"
+++

#### Dọn dẹp trên AWS console

Đầu tiên các bạn cần phải truy cập vào AWS console để xóa các dịch vụ mà các bạn đã tạo thủ công trước.

- Trong trang **console**, tìm kiếm từ khóa **CloudFormation**.
- Chọn **Stacks**.
- Chọn 2 **Service** mình đã tạo và chọn **Delete**.

![image](/images/9-clear/9.1.png)

- Chọn **Delete**.

![image](/images/9-clear/9.2.png)

- Đợi khoảng 5 đến 10 phút để quá trình xóa hoàn thành.

![image](/images/9-clear/9.3.png)

- Vào lại ECS cluster xem service đã được xóa chưa.

![image](/images/9-clear/9.4.png)

#### Dọn dẹp bằng lệnh Terraform

{{% notice note %}}
Bởi vì các tài nguyên trong hạ tầng đã được tạo bởi **Terraform**, vì thế **Terraform** có một cái rất là tiện lợi đó là chỉ cần dùng một dòng lệnh duy nhất để có thể xóa hết tài nguyên mà không cần phải xóa thủ công từng cái một.
{{% /notice %}}

Bây giờ mình sẽ vào lại nơi mình đã chạy hạ tầng bằng Terraform.

- Dùng lệnh để xóa tài nguyên.

```
terraform destroy
```

![image](/images/9-clear/9.5.png)

- Nhập `yes` để xác nhận.

![image](/images/9-clear/9.6.png)

- Đợi khoảng 15 đến 20 phút để có thể xóa hết tài nguyên.

![image](/images/9-clear/9.7.png)

- Sau khi xóa thành công, các bạn nên vào lại AWS console kiểm tra lại các tài nguyên xem đã được xóa hết chưa.

![image](/images/9-clear/9.8.png)

+++
title = "Thêm cơ sở dư liệu vào RDS"
date = 2024
weight = 4
chapter = false
pre = "<b>4. </b>"
+++

#### Kết nối vào EC2 Instance

Đầu tiên mình cần truy cập vào instance đã được tạo bởi Terraform và truy cập vào nó để add dữ liệu cho RDS.

- Tìm kiếm `ECS Instance` trong AWS console.
- Chọn tên instance mình đã tạo và chọn **Connect**.

![image](/images/4-rds/4.1.png)

- Chọn **SSH client**.
- Copy đường dẫn như hình.

![image](/images/4-rds/4.2.png)

- Dán vào bên trong VS Code của mình và cấu hình lại đường dẫn của **Key pair** mình đã lưu.
- Kết nối thành công.

![image](/images/4-rds/4.3.png)

#### Add Database

{{% notice note %}}
Bởi vì trong cấu hình Terraform của mình đã setup sẵn các dependencies và có cả cơ sở dữ liệu mẫu trong đó, vì thế nên việc add data vào RDS sẽ trở nên dễ dàng hơn.
{{% /notice %}}

Bây giờ, chúng ta sẽ đi vào thư mục đã được setup sẵn và thêm đường dẫn tuyệt đối cho phần cơ sở dữ liệu trong này.

- Chúng ta sẽ dùng lệnh sau.

```
cd ./aws-fcj-container-app/database/
echo $PWD/init.sql
```

![image](/images/4-rds/4.4.png)

Tiếp theo ta cần đăng nhập vào RDS để add data ở trong đường dẫn đó vào.

- Copy Endpoint của RDS.
- Dùng endpoint đó để dán vào lệnh sau.

```
mysql -h "rds-endpoint" -u "name-user" -p
```

![image](/images/4-rds/4.5.png)

- Dán lệnh trên vào trong máy ảo và nhập password để kết nối tới RDS.
- Dán đường dẫn có data vào trong RDS đang được kết nối.

```
source /home/ubuntu/aws-fcj-container-app/database/init.sql
```

![image](/images/4-rds/4.6.png)

- Add dữ liệu thành công.

![image](/images/4-rds/4.7.png)

- Dùng một số lệnh để kiểm tra database.

```
SHOW DATABASES;
USE fcjresbar;
SELECT * FROM Clients;
```

![image](/images/4-rds/4.8.png)

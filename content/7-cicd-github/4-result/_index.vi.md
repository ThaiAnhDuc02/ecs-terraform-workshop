+++
title = "Kiểm tra kết quả"
date = 2021
weight = 4
chapter = false
pre = "<b>7.4. </b>"
+++

#### Tạo tag

Để CI/CD được chạy, chúng ta cần phải tạo tag mới cho code.

- Vào lại **repository** của bạn.
- Chọn vào **Tags**.

![image](/images/7-cicd/7.4.1.png)

- Chọn **Releases**.
- Chọn **Draft a new release**.

![image](/images/7-cicd/7.4.2.png)

- Nhập tên tag mới: `v1.0.4`
- Chọn **Create new tag**.

![image](/images/7-cicd/7.4.3.png)

- Chọn **Publish release** để tạo thành công.

![image](/images/7-cicd/7.4.4.png)

#### Kiểm tra kết quả

Để theo dõi tiến trình CI/CD, các bạn sẽ làm theo các bước sau:

- Vào phần **Actions**.
- Chọn vào tên tiến trình mình đã đặt.

![image](/images/7-cicd/7.4.5.png)

- Xem quá trình **CI/CD** của **backend** và **frontend** tại đây.
- Nếu lỗi thì xem **logs** ở bên dưới.

![image](/images/7-cicd/7.4.6.png)

Sau khi CI/CD chạy thành công, bạn sẽ lên giao diện AWS console để kiểm tra xem các thành phần như Task definition và Service đã được update hay chưa.

- Vào **Task definitions** kiểm tra xem có task mới nào được tạo chưa.
- Đầu tiên vào vào task của **Backend**.

![image](/images/7-cicd/7.4.7.png)

- Tiếp theo là vào task của **frontend**.

![image](/images/7-cicd/7.4.8.png)

- Kiểm tra **Service** đang được update.

![image](/images/7-cicd/7.4.9.png)

Sau khi đã hoàn thành tất cả, bạn sẽ vào lại DNS của Load balancer để kiểm tra phần thay đổi của bạn đã được update hay chưa.

- Load lại trang hiện tại.

![image](/images/7-cicd/7.4.10.png)

+++
title = "Giám sát"
date = 2024
weight = 8
chapter = false
pre = "<b>8. </b>"
+++

#### Cấu hình Container Insights (CloudWatch)

Trong phần này thì chúng ta sẽ phải cấu hình một số thứ trước khi có thể dùng được Container Insights. Container Insights là một dịch vụ mà cho phép chúng ta có thể quan sát được các thông số như mức sử dụng CPU, Network, … từ đó có thể suy ra được lượng người dùng trong một khoảng thời gian nào đó.

Kết hợp với CloudWatch thì chúng ta có thể xem được các logs được gửi từ trong Container dưới dạng các groups, thông thường thì tên group sẽ bắt đầu với tiền tố là /ecs/*. Khi đó thì chúng ta sẽ có cái nhìn tổng quát hơn về các ứng dụng trong hệ thống, như là đang chạy như thế nào, có cảnh báo gì không, hay là khi có một ứng dụng nào đó bị lỗi thì chúng ta có thể đọc các logs đó để tìm ra nguyên nhân, hoặc cũng có thể điều tra được các traffic bất thường khi hệ thống bị xâm nhập.

- Trong trang console của **ECS**, ở menu bên phải, chọn **Account settings**.
- Chọn **Update**.

![image](/images/8-monitoring/8.1.png)

- Chọn **Container Insights**.
- Chọn **Save changes**.

![image](/images/8-monitoring/8.2.png)

- Hoàn thành tạo cấu hình Container insight.

![image](/images/8-monitoring/8.3.png)

#### Quan sát các thông số với Performance Monitoring

- Vào lại **Clusters**.
- Chọn **Metrics**.
- Chọn vào **View Container Insights** để quan sát.

![image](/images/8-monitoring/8.4.png)

- Quan sát các thông số với **ECS**.

![image](/images/8-monitoring/8.5.png)

Nếu như chúng ta muốn đổi sang quan sát **Task definitions** thì làm theo các bước sau:

- Ở phần đang được khoanh trong hình, bạn đổi thành **ECS Tasks** để theo dõi được các sự kiện ở đây.

![image](/images/8-monitoring/8.6.png)

Tương tự nếu như muốn đổi qua xem các sự kiện ở bên ECS Service thì làm như sau:

- Ở phần đang được khoanh trong hình, bạn đổi thành **ECS Service** để theo dõi được các sự kiện ở đây.

![image](/images/8-monitoring/8.7.png)

#### Quan sát các thông số với Container Map

Ở trong phần này thì chúng ta có thể xem được trong **Cluster** mà chúng ta đã triển khai thì có những **Containers** nào, **Tasks** nào, **Services** nào, … một cách cụ thể hơn.

- Thay đổi **Performance Monitoring** thành **Container Map**.

![image](/images/8-monitoring/8.8.png)

Sau đó chúng ta sẽ thấy được giao diện mới, trong này, bạn có thể thấy được là một **Cluster** nó sẽ quản lý các tài nguyên có liên quan như **Services**, **Tasks**. Nhưng các thông số trong một Task sẽ khác với các thông số trong một **Service**, vì **Service** sẽ quản lý trực tiếp các **Task**, nên các thông số thuộc **Task** cũng sẽ thuộc **Service**.

![image](/images/8-monitoring/8.9.png)

Ở đây các bạn cũng có thể xem chi tiếng từng dịch vụ.

- Chọn vào **Service backend**.
- Chọn vào **Metrics**.

![image](/images/8-monitoring/8.10.png)

Tương tự thì bạn cũng có thể xem các Task definition.

- Chọn vào **Task fe**.
- Chọn **Metrics**.

![image](/images/8-monitoring/8.11.png)

#### Quan sát các thông số với Resources

- Đổi Container map thành Resources.

![image](/images/8-monitoring/8.12.png)

Ở đây, các bạn sẽ thấy được một list danh sách các sự kiện mình đã tạo, có thể chọn và từng dịch vụ để giám sát.

![image](/images/8-monitoring/8.13.png)

{{% notice tip %}}
Nhưng vậy thì chúng ta đã cấu hình và thực hành xong phần quan sát với Container Insights, nhưng AWS không chỉ giới hạn dịch vụ quan sát, theo dõi hệ thống trong Container Insights mà chúng ta cũng có thể dùng các dịch vụ khác hoặc các dịch vụ bên thứ 3 để làm việc đó.
{{% /notice %}}

**Chúc mừng bạn đã hoàn thành được bài Workshop này!**
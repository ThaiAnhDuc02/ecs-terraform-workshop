+++
title = "Giới thiệu"
date = 2024
weight = 1
chapter = false
pre = "<b>1. </b>"
+++

#### Bối cảnh

Tại sao lại có bài Workshop này?

Trong thực tế, triển khai hạ tầng **AWS** với **Container** thường phức tạp và tốn nhiều thời gian. Quy trình thủ công dễ dẫn đến lỗi cấu hình, khó kiểm soát, và lãng phí tài nguyên không cần thiết khi gặp sự cố. **Terraform** giải quyết những thách thức này bằng cách tự động hóa việc tạo và quản lý hạ tầng, giúp quy trình nhanh chóng và dễ dàng hơn. Khi kết hợp với **CI/CD**, việc triển khai trở nên tối ưu và dễ dàng theo dõi, giúp doanh nghiệp giảm rủi ro và cải thiện hiệu quả quản lý hệ thống.

Quy trình này mang lại nhiều lợi ích rõ rệt:

- **Tiết kiệm thời gian và chi phí**: Tự động hóa giảm thiểu công việc thủ công và tăng hiệu suất làm việc.
- **Độ tin cậy cao**: Các dịch vụ được triển khai đồng bộ, giảm thiểu lỗi do cấu hình.
- **Khả năng mở rộng linh hoạt**: Hạ tầng dễ dàng mở rộng hoặc thu hẹp theo nhu cầu, tối ưu hóa chi phí vận hành.
- **Phản hồi nhanh chóng với thay đổi**: CI/CD giúp cải tiến sản phẩm và cập nhật hệ thống nhanh hơn, đáp ứng tốt hơn nhu cầu thị trường.

Nhờ quy trình này, công ty không chỉ đáp ứng tốt nhu cầu mở rộng mà còn tối ưu hóa chất lượng dịch vụ, gia tăng tính cạnh tranh và tăng cường sự hài lòng của khách hàng.

#### Terraform là gì?

![Terraform](/images/1-account-setup/terraform.jpg)

**Terraform** là một công cụ mã nguồn mở do **HashiCorp** phát triển, dùng để quản lý hạ tầng (**Infrastructure as Code - IaC**). Nó cho phép người dùng định nghĩa và triển khai hạ tầng thông qua mã (code), giúp tự động hóa việc tạo, cập nhật, và quản lý các tài nguyên như máy chủ, cơ sở dữ liệu, mạng, và các dịch vụ khác trên các nền tảng điện toán đám mây như AWS, Azure, Google Cloud, và cả các hệ thống tại chỗ (on-premises).

Những điểm nổi bật của Terraform:
- **Quản lý Hạ Tầng như Code (IaC)**: Hạ tầng được mô tả bằng mã, cho phép kiểm soát phiên bản, chia sẻ, và sao lưu cấu hình dễ dàng, tương tự như việc quản lý mã nguồn của ứng dụng.
- **Triển khai và Cấu hình Tự động**: Với Terraform, người dùng có thể triển khai hoặc thay đổi hàng loạt tài nguyên chỉ bằng một dòng lệnh, giúp tiết kiệm thời gian và giảm thiểu sai sót thủ công.
- **Tính Độc lập với Nền Tảng**: Terraform hỗ trợ nhiều nhà cung cấp đám mây khác nhau, giúp doanh nghiệp triển khai hạ tầng đa đám mây hoặc chuyển đổi dễ dàng giữa các nền tảng mà không cần thay đổi công cụ.
- **Khả năng Quản lý Vòng đời Tài nguyên**: Terraform không chỉ tạo mà còn quản lý toàn bộ vòng đời tài nguyên, bao gồm cập nhật, sửa đổi và xóa bỏ tài nguyên khi cần thiết.
- **Tính Phân tách và Mở rộng**: Terraform cho phép chia nhỏ hạ tầng thành các module, giúp việc quản lý trở nên linh hoạt, dễ bảo trì và dễ mở rộng khi hệ thống phát triển.

Nhờ những ưu điểm trên, Terraform giúp đơn giản hóa quy trình quản lý hạ tầng, làm cho các thay đổi trở nên an toàn, kiểm soát được và dễ dàng triển khai trên quy mô lớn.

#### Github Action CI/CD

**GitHub Actions** là dịch vụ tự động hóa tích hợp trên GitHub, giúp tự động hóa quy trình phát triển phần mềm từ kiểm tra mã nguồn đến triển khai ứng dụng, dễ dàng thiết lập CI/CD (Continuous Integration/Continuous Deployment).

1. **Continuous Integration (CI)**
- Xây dựng và Kiểm tra Tự động: Tự động xây dựng và kiểm tra mã mỗi khi có thay đổi, giúp phát hiện lỗi sớm.
- Workflows: Định nghĩa các workflow để tự động thực hiện kiểm tra, xây dựng và phát hành mã khi có sự kiện như pull request hoặc commit mới.
2. **Continuous Deployment (CD)**
- Triển khai Tự động: Hỗ trợ triển khai ứng dụng tự động lên các môi trường như staging hoặc production khi mã được chấp nhận.
- Tích hợp Dịch vụ: Dễ dàng tích hợp với các dịch vụ như AWS, Azure và Google Cloud.
3. **Tính Năng Nổi Bật**
- Khả Năng Tùy Biến: Tạo các action tùy chỉnh hoặc sử dụng action từ GitHub Marketplace.
- Giao Diện Thân Thiện: Dễ dàng thiết lập và quản lý workflows mà không cần kiến thức sâu về scripting.
- Quản lý Tài Nguyên: Theo dõi trạng thái workflow và cung cấp thông tin chi tiết về quá trình kiểm tra và triển khai.
4. **Lợi Ích**
- Tiết Kiệm Thời Gian: Giảm thiểu công việc lặp đi lặp lại cho nhà phát triển.
- Nâng Cao Chất Lượng Mã: Cải thiện chất lượng phần mềm nhờ kiểm tra và triển khai thường xuyên.
- Khả Năng Linh Hoạt: Dễ dàng điều chỉnh quy trình CI/CD để phù hợp với nhu cầu dự án.

#### Monitoring với CloudWatch Container Insights

**CloudWatch Container Insights** là một tính năng trong **AWS CloudWatch**, cung cấp khả năng giám sát và phân tích các container đang chạy trên Amazon ECS (Elastic Container Service) và EKS (Elastic Kubernetes Service). Dưới đây là một số điểm nổi bật của Container Insights:

- **Giám sát Hiệu Suất**: Container Insights cho phép bạn theo dõi các chỉ số hiệu suất quan trọng như CPU, bộ nhớ, và mạng cho từng container, giúp phát hiện sớm các vấn đề và tối ưu hóa hiệu suất ứng dụng.
- **Thống Kê Tình Trạng Container**: Bạn có thể xem thông tin chi tiết về tình trạng hoạt động của các container, bao gồm trạng thái của chúng (chạy, dừng, lỗi) và các thông số khác như thời gian chạy và số lượng bản sao.
- **Tích Hợp Với AWS**: Container Insights có thể dễ dàng tích hợp với các dịch vụ khác của AWS, cho phép bạn xây dựng các giải pháp giám sát toàn diện và tạo báo cáo tùy chỉnh dựa trên các chỉ số container.
- **Dashboard Trực Quan**: AWS cung cấp các dashboard trực quan cho phép bạn theo dõi tình trạng và hiệu suất của container một cách dễ dàng, cùng với khả năng thiết lập cảnh báo khi có sự cố xảy ra.

{{% notice tip %}}
Trước khi bắt đầu làm Workshop, mình khuyến khích các bạn nên dành chút thời gian tìm hiểu sơ lược về các nội dung sẽ thực hiện. Giờ thì chúng ta cùng bắt đầu và khám phá từng bước trong Workshop nhé. Chúc các bạn hoàn thành Workshop thật suôn sẻ và đạt kết quả tốt nhất!
{{% /notice %}}
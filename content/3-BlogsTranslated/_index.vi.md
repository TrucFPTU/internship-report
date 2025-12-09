---
title: "Các bài blogs đã dịch"
date: "2025-12-09"
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

Tại đây sẽ là phần liệt kê, giới thiệu các blogs mà các bạn đã dịch. Ví dụ:

### [Blog 1 - AWS Site-to-Site VPN hỗ trợ IPv6 trên địa chỉ IP bên ngoài](3.1-Blog1/)

Bài viết này giới thiệu tính năng mới của AWS Site-to-Site VPN cho phép sử dụng địa chỉ IPv6 làm IP bên ngoài của VPN tunnel. Đây là cải tiến quan trọng giúp các tổ chức dễ dàng triển khai kiến trúc mạng thuần IPv6 mà không cần chuyển đổi qua IPv4. Bạn sẽ tìm hiểu lý do IPv6 ngày càng trở nên cần thiết, lợi ích của việc giảm tiêu thụ IPv4, giảm chi phí, và đáp ứng các yêu cầu tuân thủ trong những môi trường bắt buộc IPv6-only.

Bài viết cũng hướng dẫn cách triển khai một mô phỏng hạ tầng on-premises và AWS bằng CloudFormation, thiết lập VPN IPv6 qua Transit Gateway, phân tích các route được quảng bá, và cách kiểm tra hoạt động của đường hầm VPN trong môi trường thực tế.

### [Blog 2 - Tối ưu hóa Amazon EMR runtime cho Apache Spark với EMR S3A](3.2-Blog2/)

Bài viết này giới thiệu cách Amazon EMR 7.10 nâng cấp hiệu năng đọc/ghi của Apache Spark thông qua trình kết nối EMR S3A — phiên bản cải tiến của S3A mã nguồn mở và được đặt làm connector mặc định cho EMR trên EC2, Serverless, EKS và Outposts. Bạn sẽ tìm hiểu cách EMR S3A mang lại hiệu năng đọc tương đương EMRFS, đồng thời cải thiện hiệu năng ghi 7% với static partition overwrite và đến 215% với dynamic partition overwrite.

Bài viết mô tả kiến trúc hạ tầng benchmark (Spark 3.5.5, Hadoop 3.4.1, cluster r5d.4xlarge), phương pháp kiểm thử gồm ba giai đoạn (baseline với EMR S3A, kiểm thử EMRFS, và so sánh với OSS S3A), cùng quy trình benchmark 104 truy vấn SparkSQL. Ngoài ra bài viết còn phân tích chi phí EC2, EBS, EMR để đánh giá đầy đủ hiệu quả vận hành khi sử dụng EMR S3A so với EMRFS và S3A mã nguồn mở.

### [Blog 3 - ...](3.3-Blog3/)

### [Blog 3 - Thiết lập khôi phục thảm họa cross-account bằng AWS Elastic Disaster Recovery trong môi trường bảo mật (Phần 1)](3.3-Blog3/)

Bài viết này là phần đầu tiên trong loạt hai phần, hướng dẫn cách triển khai quy trình khôi phục thảm họa (DR) giữa các tài khoản AWS trong môi trường bảo mật cao bằng Elastic Disaster Recovery (DRS). Nội dung tập trung vào kiến trúc mạng và các thiết lập cần thiết để duy trì network isolation, bảo toàn sơ đồ địa chỉ IP, và đảm bảo ứng dụng tiếp tục hoạt động ổn định trong các tình huống failover/failback.

Bài viết giải thích cách sử dụng AWS PrivateLink, VPC Peering và Route 53 private hosted zones để kết nối các dịch vụ AWS mà không cần internet gateway, đáp ứng yêu cầu bảo mật nghiêm ngặt. Kiến trúc mẫu bao gồm production account và recovery account ở hai Region (Ireland và London), mỗi bên có VPC production, staging và recovery. Bên cạnh đó bài viết mô tả cách cấu hình VPC endpoints cho Elastic Disaster Recovery, Amazon S3, AWS STS và Amazon EC2 nhằm hỗ trợ replication, failover và reverse replication. Đây là nền tảng cần thiết để đạt DR bền vững, an toàn và phù hợp cho các workload nhạy cảm.

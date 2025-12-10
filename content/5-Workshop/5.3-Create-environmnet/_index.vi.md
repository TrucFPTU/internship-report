---
title: Tạo môi trường
date: "2025-12-09"
weight: 3
chapter: false
pre: " <b> 5.3 </b> "
---

## Tạo Elastic Beanstalk Application (Default VPC)

Đăng nhập AWS Console và truy cập dịch vụ Elastic Beanstalk.  
Tiến hành tạo mới một Application với các thông số:

- **Application name:** đặt theo tên dự án
- **Platform:** Java (Corretto) – phiên bản tương ứng với JDK ứng dụng đang sử dụng
- **Environment type:** Web Server
- **VPC:** sử dụng Default VPC (Elastic Beanstalk tự nhận diện và chọn mặc định)
- **Environment tier:** Single Instance (không sử dụng Load Balancer)

Việc sử dụng Default VPC giúp đơn giản hóa toàn bộ quá trình triển khai,  
không cần cấu hình subnet, route table hay security group thủ công.

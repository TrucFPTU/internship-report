---
title: "Giới thiệu"
date: "2025-12-09"
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

## Giới thiệu

Elastic Beanstalk (EB) là dịch vụ quản lý ứng dụng (Platform as a Service – PaaS) do AWS cung cấp, cho phép triển khai và vận hành các ứng dụng web mà không cần quản lý trực tiếp hạ tầng máy chủ.

Trong workshop này, ứng dụng **Spring Boot REST API** sẽ được triển khai trên môi trường Elastic Beanstalk với cấu hình **Single Instance**, sử dụng **Default VPC** nhằm đảm bảo sự đơn giản, dễ triển khai và phù hợp cho mục đích học tập, thử nghiệm cũng như trình diễn kỹ thuật.

Quy trình triển khai tập trung vào các bước cốt lõi:

- Đóng gói ứng dụng Spring Boot thành file thực thi `.jar`.
- Tạo Application và Environment trên Elastic Beanstalk.
- Tải lên và triển khai phiên bản ứng dụng.
- Kiểm thử hoạt động dịch vụ bằng công cụ Postman.
- Theo dõi log hệ thống để đánh giá hoạt động và xử lý lỗi nếu có.

Thông qua workshop này, người thực hiện có thể nắm được quy trình triển khai một dịch vụ backend Java lên nền tảng AWS một cách chuẩn hóa, đồng thời hiểu cách Elastic Beanstalk quản lý vòng đời ứng dụng trong mô hình Single Instance.

Đây cũng là bước nền tảng để mở rộng sang các mô hình phức tạp hơn như **Load Balanced Environment**, tích hợp **RDS**, hoặc triển khai **CI/CD** trong các workshop tiếp theo.

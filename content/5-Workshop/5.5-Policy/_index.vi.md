---
title: "Truy cập ứng dụng và kiểm thử"
date: "2025-12-09"
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

## Truy cập ứng dụng và kiểm thử API bằng Postman

Sau khi triển khai thành công, Elastic Beanstalk cung cấp URL dạng:

```bash
http://<environment-id>.<region>.elasticbeanstalk.com
```

![Ví dụ](/images/2-Proposal/domain.jpg)

Sử dụng URL này để gửi yêu cầu từ Postman đến API Spring Boot.
Ví dụ:

```bash
GET http://<env>.elasticbeanstalk.com/api/hello
```

![ví dụ](/images/2-Proposal/postman.jpg)

Nếu API phản hồi đúng dữ liệu, việc triển khai coi như hoàn tất.

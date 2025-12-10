---
title: "Các bước chuẩn bị"
date: "2025-12-09"
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

#### Chuẩn bị và tạo file build (.jar)

Trước khi triển khai lên AWS, ứng dụng Spring Boot cần được đóng gói dưới dạng file chạy `.jar`.

Tại thư mục gốc dự án, thực hiện lệnh:

```bash
mvn clean package -DskipTests
```

Sau khi hoàn tất, file build xuất hiện trong thư mục:

```bash
/target/<ten-ung-dung>.jar
```

![](/images/2-Proposal/target.jpg)

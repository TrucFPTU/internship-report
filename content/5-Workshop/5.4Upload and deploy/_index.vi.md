---
title: "Upload và Deploy"
date: "2025-12-09"
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

## Upload file .jar và triển khai ứng dụng

Tại màn hình Environment vừa tạo → chọn **Upload and Deploy**.  
Thực hiện:

- Chọn file `.jar` đã build.
- Đặt **Version label** (ví dụ: `v1-initial`).
- Xác nhận triển khai.

![](/images/2-Proposal/Upload.jpg)

Elastic Beanstalk sẽ tự động thực hiện:

- Copy file lên S3
- Khởi tạo một EC2 instance đơn lẻ
- Khởi chạy ứng dụng Spring Boot trong môi trường Java đã chọn

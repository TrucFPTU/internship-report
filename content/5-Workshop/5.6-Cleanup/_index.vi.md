---
title: "Quan sát và Dọn dẹp tài nguyên"
date: "2025-12-09"
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

## Quan sát log triển khai và log ứng dụng

Elastic Beanstalk cung cấp hai hình thức xem log:

### 1. Request Logs trong Elastic Beanstalk

Có thể truy cập tại **Logs → Request logs → Last 100 lines**.  
Log này hiển thị:

- Quá trình khởi chạy Spring Boot
- Nhật ký lỗi nếu ứng dụng gặp lỗi
- Request/response được xử lý qua môi trường runtime

### 2. CloudWatch Logs

Elastic Beanstalk tự động đẩy một số log vào CloudWatch,  
đặc biệt là log hệ thống của EC2 instance.

## Clean up tài nguyên sau khi triển khai

Để tránh phát sinh chi phí không mong muốn, cần tiến hành xoá các tài nguyên đã tạo sau khi hoàn tất workshop.

### 1. Xoá Environment

Truy cập Elastic Beanstalk → chọn environment → Actions → **Terminate environment**.  
Việc này sẽ xoá EC2 instance, security group tự tạo và các tài nguyên liên quan.

### 2. Xoá Application (nếu không còn sử dụng)

Elastic Beanstalk → Application → Actions → **Delete Application**.

### 3. Xoá file trong S3

Elastic Beanstalk lưu các version `.jar` trong bucket S3.  
Vào S3 → tìm bucket do EB tạo → xoá các version không cần thiết.

### 4. Kiểm tra lại CloudWatch Logs

Có thể xoá log group để dọn dẹp nếu muốn.


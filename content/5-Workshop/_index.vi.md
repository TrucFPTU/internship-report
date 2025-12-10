---
title: "Workshop"
date: "2025-12-09"
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Triển khai một ứng dụng **Spring Boot REST API** lên **Elastic Beanstalk**

#### Tổng quan

## Giới thiệu Workshop

Workshop này trình bày quy trình triển khai một ứng dụng **Spring Boot REST API** lên **Elastic Beanstalk** ở chế độ **Single Instance**.  
Mô hình này **không sử dụng Load Balancer**, **không cấu hình Auto Scaling**, và hoạt động hoàn toàn trong **VPC mặc định** của tài khoản AWS.

### Mục tiêu của workshop gồm:

- Tạo bản build `.jar` của dự án Spring Boot.
- Tạo Elastic Beanstalk Application và Environment đơn giản.
- Upload và triển khai file `.jar` lên môi trường.
- Kiểm tra hoạt động của API qua Postman.
- Quan sát và phân tích log bằng _request logs_.

#### Nội dung

1. [Tổng quan về workshop](5.1-Workshop-overview/)
2. [Chuẩn bị](5.2-Prerequiste/)
3. [Tạo môi trường](5.3-S3-vpc/)
4. [Upload và Deploy](5.4-S3-onprem/)
5. [Truy cập ứng dụng và kiểm thử](5.5-Policy/)
6. [Quan sát và Dọn dẹp tài nguyên](5.6-Cleanup/)

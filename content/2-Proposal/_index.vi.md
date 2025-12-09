---
title: "Bản đề xuất"
date: "2025-12-09"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

Tại phần này, bạn cần tóm tắt các nội dung trong workshop mà bạn **dự tính** sẽ làm.

# SportShop E-Commerce Platform

## Kiến trúc AWS ba tầng tối ưu chi phí cho hệ thống bán lẻ thể thao trực tuyến

---

### 1. Tóm tắt điều hành (Executive Summary)

SportShop E-Commerce Platform được xây dựng nhằm hiện đại hóa hoạt động bán hàng trực tuyến, phù hợp cho quy mô sinh viên hoặc dự án nhỏ. Hệ thống sử dụng ReactJS cho frontend, Spring Boot cho backend và Amazon RDS MySQL để lưu trữ dữ liệu.

Để giảm chi phí và đơn giản hoá, hệ thống loại bỏ Amazon Cognito, ALB, NAT Gateway và thanh toán ngân hàng. Backend chạy trên **Elastic Beanstalk single-instance**, trong khi frontend được phân phối qua **S3 + CloudFront**.

Dù tối giản, kiến trúc vẫn đảm bảo các best practice AWS thông qua ACM, Parameter Store, CloudWatch và CI/CD (CodePipeline + CodeBuild).

---

### 2. Tuyên bố vấn đề (Problem Statement)

#### Vấn đề hiện tại

- Quy trình deploy thủ công, chậm và dễ lỗi
- Secrets dễ bị lộ hoặc quản lý sai
- Giám sát hệ thống hạn chế
- Dễ downtime khi cập nhật hệ thống

#### Giải pháp đề xuất

Nền tảng sử dụng AWS Managed Services nhằm tự động hóa triển khai, tăng cường bảo mật, và tách bạch kiến trúc thành 3 lớp:

- **Edge:** Route 53, CloudFront (ACM)
- **Application:** Elastic Beanstalk (single-instance)
- **Data:** RDS MySQL, S3, CloudWatch

Secrets (database, JWT key) lưu tại **Parameter Store**.  
CI/CD triển khai theo chuỗi GitLab → CodePipeline → CodeBuild.

#### Lợi ích

- Giảm chi phí & đơn giản hoá vận hành
- Đẩy nhanh triển khai qua CI/CD
- Phân phối nội dung HTTPS toàn cầu qua CloudFront
- Phân lớp rõ ràng giúp dễ mở rộng sau này

---

### 3. Kiến trúc giải pháp (Solution Architecture)

#### Dịch vụ AWS sử dụng

- **Route 53** — DNS
- **CloudFront** — CDN & SSL
- **Elastic Beanstalk** — Backend Spring Boot
- **RDS MySQL** — CSDL quan hệ
- **S3** — Lưu trữ static & media
- **Parameter Store** — Lưu secrets
- **CloudWatch** — Logs & metrics
- **CodePipeline + CodeBuild** — CI/CD

#### Thiết kế theo từng tầng

**Edge Layer**

- Route 53 → CloudFront
- CloudFront phục vụ frontend ReactJS qua HTTPS

**Application Layer**

- Backend Spring Boot chạy Elastic Beanstalk single-instance
- JWT authentication xử lý nội bộ
- Secrets lấy từ Parameter Store

**Data Layer**

- RDS MySQL lưu dữ liệu
- S3 lưu media + build frontend
- CloudWatch giám sát hệ thống

---

![Kiến Trúc](/images/2-Proposal/anh1.jpg)

### 4. Triển khai kỹ thuật (Technical Implementation)

- Thiết lập VPC, subnet, security group
- Hosting frontend qua S3 + CloudFront
- Deploy backend lên Elastic Beanstalk
- Tạo & cấu hình RDS MySQL
- Quản lý secrets với Parameter Store
- CI/CD: GitLab → CodePipeline → CodeBuild
- Giám sát qua CloudWatch

**Tech Stack:**

- **Frontend:** ReactJS (S3 + CloudFront)
- **Backend:** Spring Boot (Java 17)
- **Database:** RDS MySQL
- **CI/CD:** CodePipeline, CodeBuild
- **Security:** IAM, ACM, Parameter Store

---

### 5. Lộ trình thực hiện (Timeline & Milestones)

#### Tháng 1

- Setup AWS (VPC, RDS, S3, CloudFront, Route 53)
- Deploy frontend & backend
- Cấu hình CI/CD

#### Tháng 2

- Tích hợp JWT Authentication
- Xây các module: sản phẩm, đơn hàng, người dùng
- Thiết lập monitoring

#### Tháng 3

- Kiểm thử hệ thống
- Tối ưu & hoàn thiện triển khai
- Viết tài liệu & training

---

### 6. Ước tính chi phí (Budget Estimation)

Có thể xem chi phí trên [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=621f38b12a1ef026842ba2ddfe46ff936ed4ab01)  
Hoặc tải [tệp ước tính ngân sách](../attachments/budget_estimation.pdf).

| Dịch vụ                          | Chi phí/tháng |
| -------------------------------- | ------------- |
| RDS MySQL                        | $21.84        |
| Elastic Beanstalk (EC2 t3.micro) | $11.68        |
| S3                               | $0.26         |
| Data Transfer                    | $0.60         |
| CloudFront                       | $0.88         |
| Route 53                         | $0.90         |
| ACM Public Certificate           | $0            |
| CloudWatch (metrics)             | $3.02         |
| CodePipeline                     | $0            |
| CodeBuild                        | $0.50         |
| Parameter Store                  | $0            |
| CloudWatch Logs                  | $1.41         |

**Tổng chi phí:** khoảng **$35–40/tháng**  
**Hàng năm:** ~$420–480

---

### 7. Đánh giá rủi ro (Risk Assessment)

#### Rủi ro

- Backend chỉ có single-instance → không chịu lỗi
- Không có NAT → không gọi API ngoài
- JWT cần quản lý key an toàn

#### Giảm thiểu

- Bật Elastic Beanstalk health check & auto-recovery
- Thực hiện coding practice an toàn
- RDS snapshot + automated backups

---

### 8. Phát triển mở rộng trong tương lai (Future Enhancements)

1. **Amazon Cognito** – MFA, OAuth, Social Login
2. **Application Load Balancer** – High Availability
3. **NAT Gateway** – Backend truy cập API ngoài
4. **Tích hợp thanh toán** – VNPay, Stripe, PayPal
5. **RDS Multi-AZ** – Tăng HA
6. **S3 Lifecycle + Glacier** – Tối ưu lưu trữ dài hạn
7. **X-Ray + OpenSearch** – Tracing & log analytics
8. **Microservices với ECS/EKS** – Tách backend thành dịch vụ nhỏ

---

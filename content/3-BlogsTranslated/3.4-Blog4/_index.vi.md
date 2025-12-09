---
title: "Blog 4"
date: "2025-12-09"
weight: 1
chapter: false
pre: " <b> 3.4. </b> "
---

---

title: "Thiết lập khôi phục thảm họa giữa các tài khoản bằng AWS Elastic Disaster Recovery trong mạng được bảo mật (Phần 1: Kiến trúc và thiết lập mạng)"
date: "2025-09-25"
weight: 1

---

# Thiết lập khôi phục thảm họa giữa các tài khoản bằng AWS Elastic Disaster Recovery trong mạng được bảo mật (Phần 1: Kiến trúc và thiết lập mạng)

Bởi **Aamir Dar** và **Faisal Oria**, đăng ngày **25 tháng 9 năm 2025**, thuộc các danh mục:  
**Advanced (300), AWS Elastic Disaster Recovery (DRS), Learning Levels, Storage, Technical How-to**, Liên kết cố định.

Bài viết này là phần đầu tiên trong loạt hai phần nhằm cung cấp cho bạn hướng dẫn từng bước về **cross-account failover và failback** sử dụng AWS Elastic Disaster Recovery (DRS).  
Trong phần đầu tiên này, chúng tôi tập trung vào:

- kiến trúc
- network setup
- đảm bảo private IP
- duy trì isolation
- đảm bảo hoạt động liên tục

trong các DR scenarios.

---

## Giới thiệu

Bảo mật cloud infrastructure là mối quan tâm quan trọng của các tổ chức trong ngành được quản lý hoặc có workload nhạy cảm.

Nhiều tổ chức yêu cầu **không có truy cập Internet trực tiếp**, dẫn đến thách thức khi triển khai DR như Elastic Disaster Recovery.

Security control phải được duy trì trong DR, đồng thời **không thay đổi network configurations**, vì có thể gây lỗi ứng dụng.

Để giải quyết vấn đề, cần chiến lược:

- duy trì isolation
- bảo toàn IP
- đảm bảo dependent services vẫn hoạt động

AWS PrivateLink cho phép kết nối giữa VPC và AWS Services **mà không lộ traffic ra Internet**, loại bỏ nhu cầu Internet Gateway.

Kiến trúc kết hợp:

- **PrivateLink**
- **VPC Peering**
- **VPC Endpoints**
- **Route 53 Private Hosted Zones**

để xây dựng DR bảo mật cao.

---

## Tổng quan giải pháp

Giải pháp mô tả bảo vệ một EC2 instance trong:

- **Production Account — Region Ireland (eu-west-1)**
- **Recovery Account — Region London (eu-west-2)**

Cả hai môi trường **không có internet access**.

Giải pháp sử dụng:

- AWS PrivateLink
- Elastic Disaster Recovery
- VPC Peering
- Route 53

### Kiến trúc gồm 4 VPC:

- Production VPC (Production Account)
- Staging VPC (Production Account)
- Recovery VPC (Recovery Account)
- Staging VPC (Recovery Account)

Cross-Region VPC Peering:

- Production VPC ↔ Recovery Staging VPC
- Recovery VPC ↔ Production Staging VPC

Đảm bảo:

- cách ly giữa 2 environments
- vẫn giao tiếp replication cần thiết

### VPC Endpoints được tạo:

#### Trong Recovery Account — Staging VPC:

- Elastic Disaster Recovery
- Amazon S3
- AWS STS
- Amazon EC2

#### Trong Recovery Account — Recovery VPC:

- Elastic Disaster Recovery endpoint riêng

#### Trong Production Account — Staging VPC:

- Elastic Disaster Recovery
- Amazon S3
- AWS STS
- Amazon EC2

#### Trong Production VPC:

- Elastic Disaster Recovery endpoint riêng cho recovery instances

### Route 53 Private Hosted Zone:

- Hai hosted zones (one per region)
- Cần alias records để resolve AWS STS qua private IP address

---

## Điều kiện tiên quyết

### Hai AWS Accounts:

- **Production Account**
- **Recovery Account**

### Elastic Disaster Recovery phải được khởi tạo tại:

- Source Region → Production Account
- Target Region → Recovery Account

### Bắt buộc bật tùy chọn:

**Use private IP for data replication (VPN, DirectConnect, VPC Peering)**

### Cross-Account Trust Relationship:

- Production trust Recovery
- Recovery trust Production
- Chọn role:  
  **Failback and in-AWS right-sizing roles** cho cả hai chiều

### EC2 Instances cần IAM Role:

- `AWSElasticDisasterRecoveryEc2InstancePolicy`

### Mỗi account phải có:

- Production VPC
- Recovery VPC
- Staging VPC (ở cả Production & Recovery Accounts)

---

## Hướng dẫn — Các bước chính

1. Tạo VPC endpoints trong Staging VPC của Recovery Account
2. Tạo Route 53 Private Hosted Zone + alias STS record
3. Kết nối Production VPC ↔ Staging VPC (Recovery)
4. Xác thực kết nối VPC endpoints
5. Tạo VPC endpoints trong Staging & Production VPCs của Production Account
6. Tạo Route 53 Private Hosted Zone (Production)
7. Kết nối Recovery VPC ↔ Staging VPC (Production)
8. Xác thực kết nối mạng lần cuối

---

## Bước 1: Tạo VPC Endpoint trong Staging VPC của Recovery Account

Các source servers cần kết nối đến:

- Elastic Disaster Recovery endpoint
- AWS STS endpoint
- Amazon S3 (để tải agent)
- Amazon EC2 (để tạo snapshot)

Security Group:

- Allow HTTPS từ CIDR của Production VPC và Staging VPC

Các endpoint bao gồm:

### Amazon S3:

- **Interface Endpoint** (cho installer)
- **Gateway Endpoint** (cho replication & conversion servers)

### Elastic Disaster Recovery:

- Interface endpoint cho Staging VPC
- Interface endpoint riêng cho Recovery VPC

### Amazon EC2:

- Interface endpoint

### AWS STS:

- Interface endpoint

Tạo trong console:

- VPC Console → Endpoints → Create endpoint
- Chọn AWS Services
- Tìm:
  - "drs"
  - "s3"
  - "sts"
  - "ec2"

### Hình minh hoạ (Hình 2 – Hình 6)

(_Markdown không hiển thị ảnh do bạn không gửi file—nhưng tao giữ nguyên mô tả hình như nội dung gốc_)

---

## Bước 2: Tạo Route 53 Private Hosted Zone cho AWS STS (Recovery Account)

Domain name:

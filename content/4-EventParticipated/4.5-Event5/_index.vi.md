---
title: "Event5"
date: 2025-11-29T08:30:00+07:00
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

# Báo cáo tổng hợp: “AWS Well-Architected – Security Pillar Workshop”

### Mục tiêu của sự kiện

- Hiểu mô hình **5 trụ cột bảo mật** trong AWS Well-Architected  
- Nắm các best practice về IAM, detection, data protection và incident response  
- Tìm hiểu chiến lược phòng tránh các mối đe dọa cloud phổ biến tại Việt Nam  
- Trải nghiệm demo thực tế như kiểm tra IAM Policy và hệ thống cảnh báo  

### Thời gian & địa điểm

- **Ngày:** 29/11/2025 (Buổi sáng)  
- **Giờ:** 08:30 – 12:00  
- **Địa điểm:** AWS Vietnam Office  


## Nền tảng bảo mật

- Vai trò của **Security Pillar** trong mô hình Well-Architected  
- Nguyên tắc cốt lõi: **Least Privilege – Zero Trust – Defense in Depth**  
- Giải thích sâu về **Mô hình Trách nhiệm Chia sẻ (Shared Responsibility)**  
- Các mối đe dọa cloud phổ biến tại Việt Nam (S3 lộ dữ liệu, IAM yếu, cấu hình sai)

---

## Pillar 1 — Identity & Access Management (IAM)

### Kiến trúc IAM hiện đại (08:50 – 09:30)

- Loại bỏ credential sống lâu → dùng **IAM Roles**, OIDC federation, temporary tokens  
- Dùng **IAM Identity Center** cho SSO và quản lý permission tập trung  
- Tăng cường bảo mật multi-account bằng **SCP** và permission boundaries  
- Bảo mật nâng cao: **MFA**, credential rotation, Access Analyzer  
- *Mini Demo:* Kiểm tra IAM policy và mô phỏng truy cập  

**Bài học chính:**  
→ IAM là lớp phòng thủ đầu tiên; cấu hình sai IAM là nguyên nhân hàng đầu của vi phạm bảo mật cloud.

---

##  Pillar 2 — Giám sát & Phát hiện

### Continuous Monitoring (09:30 – 09:55)

- Bộ công cụ phát hiện của AWS: **CloudTrail**, **GuardDuty**, **Security Hub**  
- Bật log trên mọi tầng: VPC Flow Logs, ALB Logs, S3 Access Logs  
- Xây pipeline cảnh báo qua **EventBridge**  
- “Detection-as-Code”: đưa luật cảnh báo vào IaC và version control  

**Bài học chính:**  
→ Bảo mật chỉ hiệu quả khi có **giám sát liên tục, đầy đủ và nhất quán**.

---

##  Pillar 3 — Infrastructure Protection

### Network & Workload Security (10:10 – 10:40)

- Thiết kế VPC: tách biệt public/private subnet  
- Security Groups vs NACLs: sự khác biệt và cách dùng chuẩn  
- Bảo vệ mở rộng: **AWS WAF**, **Shield Advanced**, **Network Firewall**  
- Bảo vệ workload: baseline security cho EC2, ECS, EKS  

**Bài học chính:**  
→ Phải áp dụng mô hình **bảo vệ đa lớp**, không thể chỉ dựa vào SG hoặc NACL.

---

## Pillar 4 — Data Protection

### Mã hóa, Key & Secrets (10:40 – 11:10)

- **KMS**: key policies, grants, rotation  
- Mã hóa at-rest & in-transit: S3, EBS, RDS, DynamoDB  
- Sử dụng **Secrets Manager** & Parameter Store thay vì hardcode secrets  
- Phân loại dữ liệu & guardrails hạn chế truy cập  

**Bài học chính:**  
→ Mã hóa là yêu cầu bắt buộc; quản lý key đúng cách quan trọng không kém.

---

##  Pillar 5 — Incident Response

### Playbook & Tự động hóa (11:10 – 11:40)

- Chu trình IR chuẩn AWS  
- Playbook thực tế:
  - Lộ IAM Access Key  
  - S3 bị public  
  - EC2 nhiễm malware  
- Quy trình cô lập: snapshot, quarantine, thu thập chứng cứ  
- Tự động hóa bằng **Lambda**, **Step Functions**

**Bài học chính:**  
→ IR phải được **chuẩn bị sẵn**, không thể viết khi sự cố đã xảy ra.

---

# Những điều học được

### Tư duy bảo mật

- Phòng ngừa quan trọng hơn xử lý  
- Hạn chế tối đa tài nguyên public-facing  
- Mọi thứ cần được quản lý bằng **Infrastructure as Code**  
- Zero Trust là nguyên tắc bắt buộc, không phải tùy chọn

### Kiến thức kỹ thuật

- Hiểu rõ 3 nguồn dữ liệu phát hiện:  
  **CloudTrail**, **VPC Flow Logs**, **DNS Logs**  
- Biết xây dựng quy trình IR từng bước  
- Áp dụng Network Firewall & DNS Firewall để chặn mối đe dọa chủ động  
- GuardDuty + Security Hub = hệ thống threat intelligence tự động

### Kỹ năng thực hành

- Xác thực quyền truy cập bằng Access Analyzer  
- Cấu hình CloudTrail cấp tổ chức kèm EventBridge  
- Sử dụng S3 Block Public Access  
- Mã hóa dữ liệu và xoay vòng secrets  

---

# Ứng dụng vào công việc

- Loại bỏ credential dài hạn, enforce MFA toàn bộ account  
- Triển khai GuardDuty, Security Hub và logging tập trung  
- Giảm thiểu tài nguyên public như database, cache, EC2  
- Bật mã hóa mặc định cho S3, RDS, EBS, DynamoDB  
- Viết playbook IR cho các kịch bản phổ biến  
- Tự động hóa quá trình phát hiện → cô lập → khắc phục bằng Lambda  

---

# Trải nghiệm sự kiện

Tham dự **AWS Security Pillar Workshop** giúp tôi hiểu rõ hơn về bảo mật cloud theo hướng hiện đại, chuyên sâu và thực tiễn.

### Ấn tượng từ diễn giả

- Các diễn giả chia sẻ nhiều trường hợp thực tế xảy ra tại doanh nghiệp Việt Nam  
- Nhấn mạnh rằng 80% sự cố cloud đến từ **cấu hình sai**, không phải do AWS  

### Hoạt động thực hành

- Dùng IAM Access Analyzer để mô phỏng và kiểm tra quyền  
- Tình huống “S3 public exposure” rất thực tế và gây ấn tượng mạnh  
- Học cách sử dụng Network Firewall và DNS Firewall để lọc traffic độc hại  

### Công cụ & tự động hóa

- GuardDuty Active Threat Defense cho phép tự động chặn IP độc hại  
- EventBridge + Lambda tạo thành pipeline phản ứng sự cố hoàn toàn tự động  
- IaC & Detection-as-Code giúp bảo mật có thể mở rộng theo tổ chức  

### Thảo luận & networking

- Có cơ hội trao đổi với các chuyên gia AWS và các bạn tham dự  
- Hiểu thêm các lỗi bảo mật phổ biến trong doanh nghiệp Việt Nam  
- Thay đổi cách nhìn: Bảo mật là **quy trình liên tục**, không phải cấu hình một lần rồi để đó  

### Những bài học nhớ nhất

- Zero Trust + Least Privilege là nền tảng  
- Log mọi thứ — nếu không log, bạn không thể điều tra  
- Tự động hóa giúp giảm thời gian xử lý sự cố  
- Chuẩn bị IR từ trước sẽ giảm thiểu thiệt hại đáng kể  

---

### Một số hình ảnh sự kiện
*Thêm ảnh sự kiện tại đây*

> Sự kiện giúp tôi thay đổi tư duy về bảo mật cloud — từ bị động sang chủ động, từ thủ công sang tự động, và từ kỹ thuật đơn lẻ sang quy trình tổng thể theo chuẩn AWS.

---
title: "Event2"
date: 2025-12-09T19:30:30+07:00
draft: true
---

{{% notice warning %}}
⚠️ **Lưu ý:** Thông tin bên dưới chỉ dùng để tham khảo. Vui lòng **không sao chép nguyên văn** vào báo cáo của bạn, bao gồm cả cảnh báo này.
{{% /notice %}}

# Báo Cáo Tóm Tắt: “Bảo vệ trước các mối đe dọa công khai: AWS WAF & Application Protection”

### Mục tiêu sự kiện
- Cung cấp tổng quan về các rủi ro bảo mật mà ứng dụng công khai thường gặp.
- Giải thích cách AWS WAF hoạt động, cách thiết kế rule groups hiệu quả và cách giảm thiểu false positives.
- Trình diễn AWS WAF Bot Control để nhận diện và chặn tự động hóa độc hại.
- Giới thiệu các lớp phòng thủ DDoS của AWS Shield và những cải tiến mới như gói chi phí cố định (flat-rate bundles).
- Giúp người tham dự hiểu cách xây dựng mô hình bảo vệ nhiều lớp bằng Route 53, CloudFront, WAF và Shield.

### Diễn giả
- **Các chuyên gia bảo mật AWS** – chuyên sâu về bảo mật ứng dụng và mạng (không công bố tên trong tài liệu nguồn).

---

# Những Điểm Nổi Bật

### Hiểu về các mối đe dọa Internet hiện đại
- Endpoint công khai khiến ứng dụng dễ bị tấn công với tần suất cao, gây downtime, tăng chi phí và ảnh hưởng tuân thủ bảo mật.
- Hậu quả có thể bao gồm tăng tiêu thụ tài nguyên, rò rỉ dữ liệu, credential stuffing, giảm niềm tin của khách hàng.
- Các nhóm mối đe dọa chính:
  - **Tấn công DoS/DDoS** ở tầng L3/L4 và L7.
  - **Lỗ hổng ứng dụng**, bao gồm CVE phổ biến và OWASP Top 10.
  - **Hoạt động bot**, từ scraping đến đánh cắp tài khoản, đặc biệt tăng mạnh bởi **bot dựa trên AI** (GPT, Claude, Meta AI).

### Xu hướng tấn công gia tăng
- Dữ liệu gần đây cho thấy DDoS tăng đều qua từng năm.
- Client dựa trên AI làm tăng đột biến lưu lượng tự động và khó đoán.
- Giai đoạn 2021–2025 chứng kiến các hành vi tấn công ngày càng tinh vi.

---

# Kiến trúc & Chiến lược bảo vệ

### Tăng cường an ninh biên bằng AWS
- **Amazon Route 53**: DNS có tính sẵn sàng cao, kháng DDoS tốt.
- **Amazon CloudFront**:
  - Đóng vai trò reverse proxy, kết thúc TLS tại edge.
  - Chặn tấn công từ sớm ở edge để giảm tải backend.
  - Hỗ trợ private VPC origin để ẩn ALB/EC2 khỏi Internet công khai.

### AWS Shield (Standard & Advanced)
- Shield cung cấp lọc lưu lượng tầng mạng, bảo vệ SYN/UDP, và giảm thiểu dựa trên health metrics.
- Shield Advanced bổ sung:
  - Tự động tạo rule L7
  - Bảo vệ chi phí khi autoscaling trong tấn công
  - Hỗ trợ từ Shield Response Team (SRT)

### Các gói CloudFront Flat-Rate mới
- Gồm các mức giá cố định (Free, Pro, Business, Premium), bao gồm CDN + WAF + DDoS + DNS + logging + edge compute.
- Giúp kiểm soát chi phí dễ dàng, tránh hóa đơn tăng bất ngờ khi gặp tấn công.
- Lưu lượng bị WAF/Shield chặn **không tính vào quota sử dụng**.

---

# AWS WAF Deep Dive

### Cách WAF hoạt động
- Web ACL gồm rule, thứ tự ưu tiên, managed rule groups và hành động mặc định.
- Hỗ trợ các hành động: **Allow, Block, Challenge, CAPTCHA, Count**.
- Rate-based rule giới hạn lưu lượng theo IP hoặc custom key.
- Labels cho phép rule chaining, ngoại lệ và quyết định theo ngữ cảnh.

### Thứ tự rule khuyến nghị
1. IP allowlists/blocklists  
2. Anti-DDoS managed rules  
3. Rate limiting  
4. Kiểm tra client ẩn danh / xác thực  
5. OWASP/CVE core protections  
6. Bot & fraud detection  
7. Custom business rules (bắt đầu ở **Count**)

### Bot Control
- Phân biệt bot tốt/xấu dựa trên IP reputation, user agent, TLS fingerprint, kiểm tra browser và telemetry.
- Phát hiện bất thường như token reuse, thay đổi IP nhanh, dấu hiệu automation.
- Hỗ trợ Challenge/CAPTCHA trước khi Block.

---

# Key Takeaways

### Tư duy bảo mật
- Xem exposure Internet là rủi ro chính cần mô hình bảo vệ nhiều lớp.
- Bắt đầu từ Count mode để quan sát trước khi áp dụng chặn.
- Kết hợp phòng thủ L3/L4 với firewall L7 chi tiết.

### Kiến trúc kỹ thuật
- CloudFront như tuyến phòng thủ đầu tiên giúp tối ưu chi phí compute & bandwidth.
- Dùng labels, scope-down statements và managed groups để giảm false positives.
- Dùng kỹ thuật interrogation bot cho các endpoint nhạy cảm (login, checkout).

### Chiến lược & chi phí
- Flat-rate bundle giúp dễ dự trù chi phí cho startup và hệ thống production.
- Shield Advanced giảm downtime và chi phí phát sinh trong tấn công.
- Triển khai theo từng giai đoạn + giám sát liên tục để đảm bảo ổn định.

---

# Áp dụng vào công việc

- **Đánh giá mức độ công khai**: Xác định tất cả endpoint công khai và áp dụng rule cơ bản.
- **Kích hoạt Bot Control** cho login, search và API quan trọng.
- **Sử dụng CloudFront** để lọc lưu lượng tại edge và bảo vệ origin.
- **Cấu hình rate limiting** và dùng Shield nếu yêu cầu availability cao.
- **Thử nghiệm các gói flat-rate**, bắt đầu từ Free/Pro, nâng cấp khi workload tăng.
- **Giám sát bằng CloudWatch** để phát hiện bất thường và tinh chỉnh rule liên tục.

---

# Trải nghiệm sự kiện

Tham gia workshop **“Defense from Public Threat: AWS WAF & Application Protection”** mang lại góc nhìn toàn diện và thực tiễn về bảo mật ứng dụng hiện đại.

### Học từ chuyên gia AWS
- Hiểu rõ cách hạ tầng toàn cầu (CloudFront PoPs, Route 53, edge network) phòng thủ quy mô lớn.
- Các tình huống thực tế giúp hình dung rõ ràng hơn về rủi ro và cách giảm thiểu.

### Thực hành
- Tạo rule group, cấu hình rate-based rule, thiết lập ngoại lệ dựa trên labels.
- Khám phá tín hiệu bot và so sánh challenge vs block.
- Hiểu cách private origin trên CloudFront tăng thêm lớp bảo vệ.

### Tìm hiểu cải tiến mới
- CloudFront flat-rate bundles là thay đổi đáng chú ý — đơn giản hóa chi phí trong khi tăng bảo mật.
- Thực hành tối ưu rule, giảm false positives, và quản lý chi phí rule premium bằng scope-down.

### Thảo luận & hợp tác
- Thảo luận về xử lý sự cố, phản ứng DDoS, và tinh chỉnh rule giúp gắn lý thuyết với thực tiễn.
- Nhấn mạnh tầm quan trọng của việc kiểm thử theo giai đoạn.

### Bài học rút ra
- Bảo vệ tự động, thông minh là cần thiết khi tấn công ngày càng phức tạp.
- Quan sát lưu lượng trước khi enforce giúp tránh sự cố vận hành.
- Kết hợp CloudFront, Shield và managed rules mang lại hiệu quả bảo mật & chi phí tối ưu.

---

### Một số hình ảnh sự kiện
*Thêm hình ảnh của bạn tại đây*

> Nhìn chung, workshop giúp mình hiểu sâu hơn về bảo mật ứng dụng hiện đại và trang bị các chiến lược thực tiễn để áp dụng vào hệ thống thực tế.



---
title: "Event4"
date: 2025-11-29T08:30:00+07:00
draft: true
---

{{% notice warning %}}
⚠️ **Lưu ý:** Nội dung dưới đây được viết lại để tham khảo. Vui lòng **không sao chép nguyên văn** vào báo cáo cuối cùng.
{{% /notice %}}

# Báo cáo Tóm tắt: “Cloud Mastery Series #2: DevOps on AWS”

### Mục tiêu của sự kiện
- Củng cố hiểu biết về văn hoá DevOps và các chỉ số hiệu suất như tốc độ triển khai và thời gian khôi phục sự cố (MTTR).  
- Giới thiệu các dịch vụ AWS hỗ trợ xây dựng pipeline CI/CD tự động từ commit đến phát hành.  
- Trình bày khái niệm Infrastructure as Code (IaC) thông qua CloudFormation và CDK nhằm chuẩn hoá việc triển khai tài nguyên.  
- Cung cấp kiến thức nền tảng về Docker và các nền tảng container của AWS cho triển khai hiện đại.  
- Nhấn mạnh tầm quan trọng của giám sát, observability và các thực hành DevOps tốt dựa trên ví dụ thực tế.  

### Diễn giả
- **Bao Huynh** – AWS Community Builder  
- **Thinh Nguyen** – AWS Community Builder  
- **Vi Tran** – AWS Community Builder  

---

## Những điểm nổi bật

### Hạn chế của việc quản lý thủ công (“ClickOps”)  
- Tốn nhiều thời gian cho đội phát triển và vận hành, làm chậm tiến độ triển khai tính năng.  
- Dễ phát sinh lỗi cấu hình do thao tác thủ công.  
- Khó duy trì môi trường đồng nhất giữa các giai đoạn phát triển.  

### Tổng quan về Infrastructure as Code (IaC)  
- Quản lý hạ tầng bằng mã nguồn thay vì thao tác trên console AWS.  
- Tăng tính **tự động**, **nhất quán**, và **giảm lỗi vận hành**.  

### AWS CloudFormation  
- Dịch vụ IaC gốc của AWS, sử dụng YAML hoặc JSON.  
- Hỗ trợ đầy đủ vòng đời stack: tạo, cập nhật, xoá.  
- Tính năng **drift detection** giúp đảm bảo hạ tầng khớp với template.  

### AWS Cloud Development Kit (CDK)  
- Cho phép viết IaC bằng TypeScript, Python, Java, …  
- Cấu trúc Construct:  
  - L1: ánh xạ trực tiếp CloudFormation  
  - L2: trừu tượng cao, mặc định thân thiện với lập trình viên  
  - L3: mẫu kiến trúc sẵn sàng sử dụng cho môi trường sản xuất  
- Các lệnh CLI phổ biến: `init`, `synth`, `deploy`, `diff`, `doctor`  

### Lựa chọn công cụ IaC  
- Tuỳ thuộc chiến lược cloud, kỹ năng đội ngũ và kiến trúc hiện tại.  
- CDK phù hợp cho đội dev; CloudFormation phù hợp cho ops; Terraform phù hợp môi trường đa cloud.  

### Docker & Containers  
- Container đóng gói ứng dụng và dependencies thành các đơn vị nhẹ, dễ di chuyển.  
- Đảm bảo tính nhất quán giữa các môi trường từ local → test → production.  
- Amazon ECR cung cấp lưu trữ, quét bảo mật và quản lý phiên bản container image.  

### Dịch vụ Container trên AWS  
- **ECS:** Quản lý container đơn giản, tích hợp AWS.  
- **EKS:** Kubernetes quản lý đầy đủ cho workload phức tạp.  
- **App Runner:** Triển khai web app serverless nhanh chóng.  

### Pipeline CI/CD trên AWS  
- Chuỗi: CodeCommit → CodeBuild → CodeDeploy → CodePipeline.  
- Hỗ trợ triển khai không downtime bằng blue/green, rolling, hoặc canary.  
- Demo minh hoạ tự động triển khai khi có commit mới.  

### Giám sát & Observability  
- **CloudWatch:** Thu thập logs, metrics, báo động, dashboards.  
- **X-Ray:** Tracing request, phân tích bottleneck và latency.  
- Hướng dẫn thực hành cảnh báo và cải thiện xử lý sự cố.  

---

## Những bài học rút ra

### Tư duy DevOps  
- Khuyến khích hợp tác chặt chẽ giữa đội phát triển và vận hành.  
- Sử dụng **DORA metrics** để đo lường và cải thiện hiệu suất.  
- Liên tục cải tiến dựa trên mục tiêu kinh doanh.  

### Thực hành kỹ thuật  
- IaC đảm bảo tính nhất quán, tăng tốc provision và giảm lỗi cấu hình.  
- CDK giúp xây dựng kiến trúc cloud phức tạp nhanh chóng.  
- Chọn ECS/EKS dựa trên nhu cầu workload và độ phức tạp.  
- Pipeline CI/CD ổn định giúp triển khai nhanh, giảm rủi ro.  

### Observability & Reliability  
- CloudWatch + X-Ray hỗ trợ phát hiện và khắc phục sự cố nhanh.  
- Triển khai canary hoặc blue/green giảm downtime.  
- Kiểm tra drift định kỳ đảm bảo môi trường luôn chính xác.  

### Chiến lược hiện đại hóa  
- Đánh giá hạ tầng hiện tại trước khi di chuyển.  
- Áp dụng migration theo từng giai đoạn để giảm rủi ro.  
- Sử dụng các dịch vụ như App Runner cho triển khai nhanh.  

---

## Áp dụng vào công việc
- Triển khai Git workflow kết hợp CodePipeline để tự động hoá.  
- Thử nghiệm CDK trong dự án nhỏ để cải thiện năng suất.  
- Xây dựng dashboards CloudWatch theo dõi hiệu suất và giảm MTTR.  
- Tổ chức thảo luận nội bộ về kiến trúc container-first.  
- Học và thi chứng chỉ AWS DevOps để nâng cao năng lực.  

---

## Trải nghiệm sự kiện

Tham dự **“Cloud Mastery Series #2: DevOps on AWS”** mang lại cái nhìn thực tế và toàn diện về áp dụng DevOps trên AWS.

### Học hỏi từ các chuyên gia  
- Các diễn giả chia sẻ kinh nghiệm thực tiễn và kỹ thuật tay nghề cao.  
- So sánh ECS, EKS và serverless giúp đưa ra quyết định kiến trúc rõ ràng.  

### Kinh nghiệm thực hành  
- Quan sát pipeline CI/CD tự động hoá toàn bộ vòng đời triển khai.  
- Hiểu cách IaC giảm sai lệch và chuẩn hoá môi trường.  
- Thực hành giám sát và debug bằng CloudWatch và X-Ray.  

### Khai thác hiệu quả công cụ AWS  
- CDK làm IaC trực quan, thân thiện với lập trình viên.  
- App Runner cho triển khai ứng dụng nhanh mà không cần quản lý server.  

### Tương tác & networking  
- Hỏi đáp và thảo luận nhóm giúp làm rõ lựa chọn công cụ và best practice.  
- Thảo luận nhóm nhấn mạnh kết hợp DevOps với giá trị kinh doanh.  

### Bài học kinh nghiệm  
- ClickOps thủ công rủi ro cao – cần tự động hoá.  
- Kết hợp IaC, CI/CD và container tăng tính mở rộng và độ bền hệ thống.  
- Observability + văn hoá DevOps giúp khôi phục nhanh và tăng độ tin cậy.  

---

### Hình ảnh sự kiện  
*Thêm hình ảnh của sự kiện tại đây*  

> Sự kiện giúp nâng cao hiểu biết về DevOps trên AWS, từ văn hóa, kỹ thuật đến công cụ, đồng thời cung cấp hướng dẫn thực tiễn để áp dụng vào dự án thực tế.

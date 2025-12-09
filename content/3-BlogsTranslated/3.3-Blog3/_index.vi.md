---
title: "Blog 2"
date: "2025-12-09"
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

# Tối ưu hóa Amazon EMR runtime cho Apache Spark với EMR S3A

_Bởi Giovanni Matteo Fumarola, Narayanan Venkateswaran, Syed Shameerur Rahman, Sushil Kumar Shivashankar, và Rajarshi Sarkar – ngày 24 tháng 9 năm 2025 – trong Amazon EMR, Analytics, Best Practices, Intermediate (200), Liên kết cố định_

Với Amazon EMR 7.10 runtime, Amazon EMR đã giới thiệu **EMR S3A**, một phiên bản cải tiến của S3A file system connector mã nguồn mở. Trình kết nối nâng cao này hiện được tự động thiết lập làm **trình kết nối S3 file system mặc định** cho các tùy chọn triển khai Amazon EMR, bao gồm:

- Amazon EMR on EC2
- Amazon EMR Serverless
- Amazon EMR on Amazon EKS
- Amazon EMR on AWS Outposts

đồng thời duy trì tính tương thích hoàn toàn với API của Apache Spark mã nguồn mở.

Trong Amazon EMR 7.10 runtime cho Apache Spark, **EMR S3A connector** thể hiện hiệu năng tương đương với **EMRFS** trong các tác vụ đọc, như được chứng minh qua _TPC-DS query benchmark_. Cải thiện hiệu năng đáng kể nhất của trình kết nối này thể hiện ở các tác vụ ghi, với mức tăng:

- **7%** đối với _static partition overwrites_
- **215%** đối với _dynamic partition overwrites_ so với EMRFS

Trong bài viết này, chúng tôi trình bày lợi thế về hiệu năng đọc và ghi được nâng cao khi sử dụng **Amazon EMR 7.10.0 runtime cho Apache Spark với EMR S3A**, so với EMRFS và S3A file system connector mã nguồn mở.

---

## So sánh hiệu năng đọc

Để đánh giá hiệu năng đọc, chúng tôi sử dụng môi trường kiểm thử dựa trên **Amazon EMR runtime version 7.10.0** chạy:

- Spark **3.5.5**
- Hadoop **3.4.1**

Hạ tầng thử nghiệm bao gồm một **Amazon EC2 cluster** gồm chín **r5d.4xlarge instances**:

- Primary node: 16 vCPU, 128 GB memory
- Tám core nodes: tổng cộng 128 vCPU, 1024 GB memory

Quá trình đánh giá hiệu năng được thực hiện bằng phương pháp kiểm thử toàn diện, nhằm đảm bảo kết quả chính xác và có ý nghĩa.

- Dữ liệu nguồn: scale factor **3 TB**
- 17,7 tỷ bản ghi
- Khoảng **924 GB** dữ liệu nén
- Được phân vùng theo định dạng tệp **Parquet**

Hướng dẫn thiết lập và chi tiết kỹ thuật có sẵn trong GitHub repository. Chúng tôi sử dụng **Spark’s in-memory data catalog** để lưu trữ metadata cho TPC-DS databases và tables.

Để tạo ra một phép so sánh công bằng và chính xác giữa **EMR S3A**, **EMRFS**, và các bản triển khai **S3A mã nguồn mở**, chúng tôi đã thực hiện phương pháp kiểm thử gồm ba giai đoạn:

### Giai đoạn 1: Hiệu năng cơ sở (Baseline performance)

- Thiết lập hiệu năng cơ sở bằng cách sử dụng cấu hình mặc định của Amazon EMR với trình kết nối S3A của EMR
- Tạo điểm tham chiếu cho các so sánh sau đó

### Giai đoạn 2: Phân tích EMRFS (EMRFS analysis)

- Giữ nguyên file system mặc định là **EMRFS**
- Giữ nguyên các cấu hình khác

### Giai đoạn 3: Kiểm thử S3A mã nguồn mở (Open source S3A testing)

- Chỉ thay thế tệp `hadoop-aws.jar` bằng phiên bản **Hadoop S3A 3.4.1** mã nguồn mở
- Giữ nguyên cấu hình giống hệt ở các thành phần khác

Môi trường kiểm thử có kiểm soát này rất quan trọng trong quá trình đánh giá vì các lý do sau:

- Có thể **cô lập tác động hiệu năng cụ thể** đến từ việc triển khai trình kết nối S3A
- Loại bỏ các biến tiềm ẩn có thể làm sai lệch kết quả
- Cung cấp các phép đo chính xác về cải thiện hiệu năng giữa bản triển khai S3A của Amazon và phiên bản thay thế mã nguồn mở

---

## Thực thi kiểm thử và kết quả

Trong suốt quá trình kiểm thử, chúng tôi duy trì **tính nhất quán** trong các điều kiện và cấu hình thử nghiệm, đảm bảo rằng mọi khác biệt về hiệu năng quan sát được có thể được quy trực tiếp cho các biến thể trong việc triển khai trình kết nối S3A.

- Tổng cộng **104 truy vấn SparkSQL** được chạy trong **10 lần lặp liên tiếp**
- Thời gian chạy trung bình của mỗi truy vấn trong 10 lần lặp được sử dụng để so sánh

Kết quả:

- Thời gian chạy trung bình trên Amazon EMR 7.10 runtime cho Apache Spark với **EMR S3A** là **1116,87 giây**
- Nhanh hơn **1,08 lần** so với S3A mã nguồn mở
- Tương đương với **EMRFS**

Bảng sau đây tóm tắt các số liệu:

| Metric                                  | OSS S3A | EMRFS   | EMR S3A |
| --------------------------------------- | ------- | ------- | ------- |
| Thời gian chạy trung bình (giây)        | 1208.26 | 1129.64 | 1116.87 |
| Trung bình nhân của các truy vấn (giây) | 7.63    | 7.09    | 6.99    |
| Tổng chi phí \*                         | $6.53   | $6.40   | $6.15   |

\* Các ước tính chi phí chi tiết sẽ được thảo luận sau trong bài viết này.

Biểu đồ (không hiển thị ở đây) minh họa **cải thiện hiệu năng trên mỗi truy vấn** của EMR S3A so với S3A mã nguồn mở trên Amazon EMR 7.10 runtime cho Apache Spark:

- Mức tăng tốc khác nhau giữa các truy vấn
- Truy vấn nhanh nhất đạt tăng **1,51 lần** cho `q3`, khi Amazon EMR S3A vượt trội hơn S3A mã nguồn mở
- Trục ngang: các truy vấn TPC-DS 3TB benchmark được sắp xếp theo thứ tự giảm dần dựa trên mức cải thiện hiệu năng
- Trục dọc: cường độ tăng tốc (tỉ lệ)

---

## So sánh chi phí đọc

Bài benchmark của chúng tôi xuất ra:

- Tổng thời gian chạy
- Số liệu trung bình nhân

để đo hiệu năng runtime của Spark. **Chỉ số chi phí** có thể cung cấp thêm nhiều thông tin chi tiết.

Các ước tính chi phí được tính bằng các công thức sau. Chúng bao gồm chi phí:

- Amazon EC2
- Amazon Elastic Block Store (Amazon EBS)
- Amazon EMR

nhưng **không** bao gồm chi phí GET và PUT của Amazon S3.

```text
Chi phí Amazon EC2 (bao gồm chi phí SSD)
  = số lượng instance * r5d.4xlarge hourly rate * thời gian chạy công việc (giờ)

r5d.4xlarge hourly rate = $1.152 mỗi giờ

Chi phí Amazon EBS gốc (Root Amazon EBS cost)
  = số lượng instance * Amazon EBS per GB-hourly rate * dung lượng EBS gốc * thời gian chạy công việc (giờ)

Chi phí Amazon EMR
  = số lượng instance * r5d.4xlarge Amazon EMR cost * thời gian chạy công việc (giờ)

r5d.4xlarge Amazon EMR cost = $0.27 mỗi giờ

Tổng chi phí = chi phí Amazon EC2 + chi phí Amazon EBS gốc + chi phí Amazon EMR
```

---
title: "Blog 1"
date: "2025-12-09"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# AWS Site-to-Site VPN hiện đã hỗ trợ IPv6 trên các địa chỉ IP bên ngoài

**bởi Ruskin Dantra, SaiJeevan Devireddy và Scott Morrison**  
_Ngày 24 tháng 9 năm 2025 – AWS Site-to-Site VPN, Networking & Content Delivery_

---

Amazon Web Services (AWS) Site-to-Site VPN là một dịch vụ được quản lý hoàn toàn cho phép bạn tạo một kết nối an toàn giữa data center hoặc văn phòng chi nhánh của bạn và các tài nguyên AWS của bạn bằng cách sử dụng IP Security (IPSec) tunnels. Nó cung cấp khả năng kết nối quan trọng cho nhiều loại workload: kết nối các workload on-premises với cloud, kết nối các thiết bị với cloud, và cung cấp liên lạc được mã hóa.

Site-to-Site VPN là một lựa chọn linh hoạt cho các nhóm để có được khả năng kết nối nhanh chóng. Khi một VPN tunnel được cấu hình, bạn phải chọn các địa chỉ IP bên ngoài và bên trong. IPv4 là lựa chọn duy nhất cho cả hai địa chỉ IP bên ngoài và bên trong cho đến năm 2018. Sau đó, chúng tôi đã phát hành hỗ trợ cho IPv6 cho các địa chỉ IP bên trong. Vào tháng 7 năm 2025, chúng tôi đã mở rộng điều này và công bố khả năng chỉ định IPv6 cho các địa chỉ IP bên ngoài.

Người dùng hiện có thể kết nối các mạng IPv6 của họ bằng cách sử dụng Site-to-Site VPN connectivity với địa chỉ IPv6 thuần túy, loại bỏ nhu cầu thực hiện chuyển đổi `IPv6 > IPv4 > IPv6`.

---

## Lợi ích của hỗ trợ IPv6

- **Di chuyển sang IPv6**: Với thông báo mới này, việc di chuyển sang IPv6 trở nên trực tiếp hơn, cho phép người dùng kết nối hai mạng IPv6 bằng cách chỉ sử dụng IPv6.
- **Cạn kiệt IP**: Tận dụng IPv6 cho outer tunnels cho phép bạn tiết kiệm các địa chỉ IPv4 có giá trị trong một môi trường nơi IPv4 đang trở thành một tài nguyên khan hiếm.
- **Giảm chi phí**: Với IPv6 trên các IP bên ngoài, bạn cũng có thể giảm chi phí kết nối hai mạng mà không cần phải trả tiền cho các địa chỉ IPv4 công khai ở bất kỳ phía nào của các tunnel của bạn (phía AWS và phía on-premises của bạn).
- **Quy định và tuân thủ**: Nếu bạn đang làm việc trong các ngành được quản lý như chính phủ, y tế, tài chính, và viễn thông, các địa chỉ bên ngoài IPv6 cho phép bạn đáp ứng các yêu cầu cho các mạng chỉ IPv6.

---

## Các cấu hình được hỗ trợ

IPv6 chỉ được hỗ trợ khi Site-to-Site VPN kết thúc trên một **AWS Transit Gateway** hoặc trên một **AWS Cloud WAN core network edge (CNE)**. Hình 1 cho thấy một ví dụ về một IPv6 Site-to-Site VPN kết thúc trên một Transit Gateway.

**Hình 1: Kết nối IPv6-only VPN đến Transit Gateway**

Việc kết thúc một IPv6 Site-to-Site VPN trên một CNE tuân theo cùng một mô hình như hình trước đó.

---

## Tổng quan về IPv6 Site-to-Site VPN

Để bắt đầu thử nghiệm với một IPv6 Site-to-Site VPN, hãy tải xuống **AWS CloudFormation template** và triển khai trong AWS Region mà bạn chọn. Template chỉ cần một tham số: một địa chỉ email để thông báo cho bạn về bất kỳ sự cố ngừng hoạt động tiềm ẩn nào. Template này cung cấp cơ sở hạ tầng sau đây (được hiển thị trong Hình 2) trong tài khoản của bạn.

**Hình 2: Môi trường triển khai IPv6 Site-to-Site VPN CloudFormation**

Triển khai template này sẽ phát sinh chi phí, được trình bày trong phần _Cost_ của bài viết. Tham khảo phần _Cleaning up_ để biết hướng dẫn gỡ bỏ. Trong phần tiếp theo, chúng tôi sẽ trình bày chi tiết cơ sở hạ tầng được triển khai.

---

## Mô phỏng trung tâm dữ liệu doanh nghiệp

Để mô phỏng một data center doanh nghiệp, template đã triển khai một VPC với cơ sở hạ tầng sau:

- Một Amazon VPC dual stack với hai tiền tố: một tiền tố IPv4 và một tiền tố IPv6.
- Địa chỉ IPv6 của VPC có thể khác nhau tùy thuộc vào việc bạn sử dụng địa chỉ IPv6 do AWS cung cấp hoặc Bring Your Own IP (BYOIP).
- Một internet gateway được gắn vào VPC. Đây là lớp nền (underlay) cho VPN của chúng ta và cho phép cài đặt và cấu hình Amazon Elastic Compute Cloud (Amazon EC2) VPN router, mô phỏng router on-premises của bạn.
- Hai IPv6-only public subnet (chứa Amazon EC2 VPN router).
- Một EC2 instance được triển khai trong IPv6-only public subnet ở trên để mô phỏng VPN router.
- Hai public dual stack subnet.
- Hai NAT gateway được triển khai trong các subnet trên để thực hiện NAT64, cho phép kết nối trực tiếp với Amazon EC2 VPN router bằng AWS Systems Manager Session Manager. Các NAT gateway này cũng rất quan trọng để thông báo cho CloudFormation khi các script đã hoàn tất việc thực thi thông qua các hook `cfn-*`.
- Hai private dual stack subnet để chứa các VPC endpoint, truy cập các dịch vụ AWS khác thông qua AWS PrivateLink.
- Hai IPv6-only private subnet để chứa một instance mà chúng ta có thể ping để kiểm thử.
- Một EC2 instance được triển khai trong IPv6-only private subnet ở trên để mô phỏng test instance.

---

## Hạ tầng AWS

Template kết thúc IPv6 Site-to-Site VPN tại một **Transit Gateway** và chúng tôi đã triển khai cơ sở hạ tầng sau:

- Một Amazon VPC dual stack với hai tiền tố: một tiền tố IPv4 và một tiền tố IPv6.
- Địa chỉ IPv6 của VPC có thể khác nhau tùy thuộc vào việc bạn sử dụng địa chỉ IPv6 do AWS cung cấp hoặc BYOIP.
- Hai private dual stack subnet để chứa Transit Gateway attachment.
- Một Transit Gateway có hỗ trợ IPv6.
- VPC được gắn vào Transit Gateway, liên kết với default route table và truyền các route đến default route table.
- Hai IPv6-only private subnet để chứa một instance mà chúng ta có thể ping để kiểm thử.
- Một EC2 instance được triển khai trong IPv6-only private subnet ở trên để mô phỏng test instance.
- Hai private dual stack subnet để chứa VPC endpoint truy cập các dịch vụ AWS khác thông qua AWS PrivateLink.
- Một EC2 instance được triển khai trong dual stack private subnet ở trên để hoạt động như jump box. Điều này là cần thiết vì VPC này không có NAT gateway để thực hiện NAT64.

---

## Cơ sở hạ tầng chung

- **AWS Secrets Manager** để quản lý VPN pre-shared key.
- **Amazon CloudWatch** để lưu trữ log, metric, và alarm.
- Một **Amazon Simple Notification Service (Amazon SNS)** topic để thông báo cho bạn về các sự cố, ví dụ như tunnel down.
- Một **AWS Key Management Service (AWS KMS)** customer managed key (CMK) để mã hóa log của CloudWatch, secret trong Secrets Manager, và SNS topic.

---

## Hạ tầng VPN

Template cũng triển khai các tài nguyên kết nối VPN sau để xây dựng IPv6 Site-to-Site VPN giữa trung tâm dữ liệu on-premises mô phỏng và AWS:

- Một customer gateway trong VPC đại diện logic cho router on-premises của bạn.
- Một IPv6 Site-to-Site VPN connection kết thúc tại Transit Gateway.
- Cấu hình EC2 instance mô phỏng router.

---

## Hướng dẫn chi tiết IPv6 Site-to-Site VPN

Các bước sau đây sẽ hướng dẫn chi tiết IPv6 Site-to-Site VPN.

### Điều kiện tiên quyết

Bạn cần đảm bảo các điều kiện sau để thực hiện hướng dẫn này:

- CloudFormation template đã được triển khai thành công mà không có lỗi.

---

### Bước 1. Customer gateway

1. Mở **Amazon VPC console** và điều hướng đến  
   **Virtual private network (VPN) > Customer gateways**.

   **Hình 3: Điều hướng đến customer gateways**

2. Chúng tôi đã triển khai một customer gateway cho bạn. Việc tạo một customer gateway cho IPv6 Site-to-Site VPN tuân theo các bước tương tự như đối với IPv4 Site-to-Site VPN.  
   Điểm khác biệt duy nhất là nó trỏ đến địa chỉ IP IPv6 của router của bạn. Trong trường hợp của chúng tôi, nó trỏ đến địa chỉ IPv6 của EC2 instance đang mô phỏng VPN router.

   **Hình 4: Giao diện AWS VPC Console, chế độ xem Customer Gateway được chọn**

3. Nếu bạn điều hướng đến **Amazon EC2 console**, sau đó vào phần **Instances**, sẽ thấy một instance có tên `…-onprem-vpn/vpn-router-instance` với địa chỉ IPv6 tương ứng.

   **Hình 5: EC2 VPN router với địa chỉ IP hiển thị**

---

### Bước 2. IPv6 Site-to-Site VPN

Template cũng đã triển khai một kết nối **IPv6 Site-to-Site VPN**.

**Hình 6: Chế độ xem chi tiết IPv6 S2S VPN**

Các bước kiểm tra:

1. Mở **Amazon VPC console**.
2. Trong thanh điều hướng, dưới mục **Virtual private network (VPN)**, chọn **Site-to-Site VPN connections**.
3. Chọn kết nối VPN được tạo bởi template có tên `…-vpn-connection`.
4. Kết nối này có một **IPv6 Customer gateway address** được liên kết với nó.
5. Điều hướng đến tab **Tunnel details**:
   - Tại đây có hai **IPv6 Outside IP address**, mỗi tunnel một địa chỉ.
   - Ngoài ra còn có hai tiền tố `/126 IPv6 Inside IP address prefix`. Các địa chỉ này được AWS cấp phát từ dải `fd00::/8`.
     - Từ tiền tố này, phía AWS của kết nối là địa chỉ IPv6 khả dụng đầu tiên.
     - Phía của bạn là địa chỉ IPv6 khả dụng thứ hai.
     - Ví dụ, nếu Inside IPv6 prefix của bạn là `fd00:…:cd90/126`, thì:
       - Địa chỉ IPv6 phía AWS là `fd00:…:cd91`
       - Địa chỉ IPv6 phía bạn là `fd00:…:cd92`.

> Để biết thêm chi tiết, tham khảo tài liệu hướng dẫn.

IPv6 Site-to-Site VPN sử dụng **dynamic routing**, quảng bá tiền tố on-premises đến AWS.  
Bạn có thể quan sát việc truyền tải on-premises route (`2001:db8:0:0::/56`) vào **Transit Gateway route table** thông qua **Site-to-Site VPN attachment**.

**Hình 7: Tuyến on-premises được truyền vào Transit Gateway route table**

#### Kiểm tra route từ phía AWS

1. Điều hướng đến **Amazon VPC console**.
2. Trong thanh điều hướng, dưới mục **Transit gateways**, chọn **Transit gateway route tables**.
3. Chọn route table được liên kết với Transit Gateway được tạo như một phần của stack này.
   - Bạn có thể tham khảo biến **CloudFormation output** có tên `AwsTransitGatewayId` để đảm bảo rằng bạn đang xem đúng Transit Gateway route table.

#### Kiểm tra route từ phía on-premises

1. Điều hướng đến **Amazon EC2 console**.
2. Chọn instance có tên `…-onprem-vpc/vpn-router-instance`.
3. Ở góc trên bên phải, chọn **Connect**.
4. Sử dụng tab **Session Manager** và chọn **Connect**, thao tác này sử dụng Systems Manager để kết nối đến Amazon EC2 VPN router.
5. Chạy lệnh sau trong cửa sổ shell:

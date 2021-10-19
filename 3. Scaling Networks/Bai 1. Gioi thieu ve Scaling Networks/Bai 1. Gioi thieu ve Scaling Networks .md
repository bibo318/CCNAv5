**Giới thiệu về Scaling Networks** 

**I. Nội dung chính**

\1. Thiết kế mạng

\2. Lựa chọn thiết bị mạng

\3. Thiết bị quản lý

**II. Nội dung chi tiết**

**1.Thiết kế mạng**

Yêu cầu quy mô mạng

Càng phát triển, mở rộng , mạng doanh nghiệp cần phải :

- Hỗ trợ những ứng dụng quan trọng
- Hỗ trợ mạng lưới hội tụ
- Hỗ trợ nhu cầu kinh doanh đa dạng
- Cung cấp giải pháp quản lý tập trung

Thiết bị doanh nghiệp

Để cung cấp một mạng lưới có độ tin cậy cao, thiết bị cấp doanh nghiệp được cài đặt trong các mạng doanh nghiệp.

![](Aspose.Words.8752bdfb-6434-4895-9749-f1799aef617e.001.png)

Mô hình thiết kế mạng

Mô hình này chia các chức năng mạng thành ba lớp riêng biệt.

![](Aspose.Words.8752bdfb-6434-4895-9749-f1799aef617e.002.png)

Kiến trúc doanh nghiệp của Cisco

Các mô-đun Cisco kiến trúc doanh nghiệp chính bao gồm:

Trụ sở chính doanh nghiệp

- Enterprise Edge
- Service Provider Edge
- Kiểm soát từ xa

Failure Domains

- Failure Domains là khu vực của một mạng mà bị ảnh hưởng khi một thiết bị hoặc dịch vụ mạng xảy ra vấn đề quan trọng.
- Liên kết cần thiết và thiết bị lớp doanh nghiệp giảm thiểu sự gián đoạn của mạng.
- Failure domains nhỏ hơn làm giảm tác động của sự thất bại về năng suất công ty
- Failure Domain nhỏ cũng đơn giản hóa việc xử lý sự cố.
- Triển khai Switch block- mỗi switch block hoạt động độc lập với nhau.
- ` `Một thiết bị bị lỗi không ảnh hưởng đến toàn mạng

Thiết kế mở rộng quy mô

- Sử dụng các thiết bị hỗ trợ việc mở rộng, cụm mô-đun thiết bị.
- Sử dụng các module thiết kế có thể được bổ sung, nâng cấp và sửa đổi, không ảnh hưởng đến thiết kế của các khu chức năng khác của mạng.
- Tạo một sơ đồ phân cấp thứ bậc.
- Sử dụng các bộ định tuyến hay chuyển mạch đa lớp để hạn chế broadcast và hạn chế lưu lượng .

Kế hoạch dự phòng

- Lắp đặt thiết bị dự phòng
- Xây dựng đường mạng dự phòng

Mở rộng băng thông

- Liên kết thiết bị hỗ trợ mở rộng băng thông bằng việc tạo ra liên kết giữa các liên kiết vật lý
- EtherChannel là một hình thưc liên kết hợp sử trong trong các mạng chuyển mạch

Mở rộng mô hình kết nối

Các kết nối có thể mở rộng  bằng cách sử dụng các kết nối không dây

**2.Lựa chọn thiết bị mạng**

Bộ chuyển phát-Switch :

- Chọn yếu tố hình thức:
- Fixed
- Modular
- Stackable
- Non-stackable
- Mật độ cổng
- Forwarding Rates: Năng lực xử lý của Bộ chuyển phát được đánh giá bởi bao nhiêu dữ liệu chuyển đổi có thể xử lý mỗi giây.
- Bộ chuyển phát đa tầng
- Được sử dụng trong các lớp lõi và distribution layer của một tổ chức mạng
- Có thể xây dựng một bảng định tuyến, hỗ trợ một vài giao thức định tuyến, và forward các gói tin IP .

Bộ định tuyến-Router:

Vai trò của bộ định tuyến:

- Kết nối nhiều khu vực
- Cung cấp các đường dự phòng
- Kết nối đến các nhà cung cấp dịch vụ
- Phiên dịch giữa các giao thức và phương tiện truyền thông

Bộ định tuyến Cisco

3 loại bộ định tuyến

- Branch – Sẵn sang 24/7.
- Network Edge – Hiệu suất, bảo mật cao và dịch vụ tin cậy
- Kết nối các trụ sở, data center và các mạng lưới chi nhánh.
- Bộ định tuyến cung cấp dịch vụ

Bộ định tuyến- Router

- Cố định cấu hình- Tích hợp giao diện.
- Modular – Slots cho phép các giao diện khác nhau được thêm vào.

**3. Thiết bị quản lý**

Quản lý In-Band vs. Out-of-Band

- **In-Band** yêu cầu ít nhất 1 interface được kết nối và hoạt động sử dụng Telnet,SSH hoặc HTTP để truy cập vào thiết bị.
- **Out-of-Band** yêu cầu kết nối trực tiếp đến console hoặc cổng AUX và Terminal Emulation khách để truy cập thiết bị

Các lệnh cấu hình cơ bản cho Router

- Hostname
- Passwords (console, Telnet/SSH, và privileged mode)
- Địa chỉ Interface IP 
- Kích hoạt giao thức định tuyến

` `Các lệnh show trong router

- **show ip protocols** – Hiển thị thông tin về giao thức định tuyến được cấu hình.
- **show ip route** –** Hiển thị thông tin bảng định tuyến.
- **show ip ospf neighbor** –** Hiển thị thông tin về OSPF neighbor
- **show ip interfaces** –** Hiển thị thông tin chi tiết về các interface
- **show ip interface brief** –**  Hiển thị thông tin ngắn gọn về các interface
- **show cdp neighbors** – Hiển thị các thông tin chi tiếp về các thiết bị Cisco kết nối trực tiếp

Các lệnh cấu hình Switch

- Hostname
- Passwords
- In-Band access yêu cầu Switch có địa chỉ IP ( gắn cho VLAN 1 )
- Lệnh lưu cấu hình– **copy running-config startup-config** .
- Xóa file cấu hình– **erase startup-config**, sau đó **reload**.
- Xóa thông tin VLAN– **delete flash:vlan.dat**.

Các lệnh show trong Switch

- **show port-security** –** Hiển thị cổng kích hoạt an ninh
- **show port-security address** –** Hiển thị các địa chỉ MAC an toàn
- **show interfaces** –Hiển thị thông tin chi tiết về các interface
- **show mac-address-table** – Hiển thị tất cả địa chỉ MAC mà Switch biết được
- **show cdp neighbors** – Hiển thị tất cả các kết nối trực tiếp các thiết bị Cisco




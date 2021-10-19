**Là bài quan trọng với sinh viên** 

**I. Nội dung chính:**

\1. Giới thiệu Router về: phần cứng, các cổng kết nối và IOS

\2. Quá trình khởi động của Router.

\3. Các Mode lệnh trong IOS: 4 mode

\4. Các lệnh cấu hình Cơ bản Router: mở Packet tracer, vẽ topology, gõ lệnh

**II. Nội dung chi tiết:**

**1. Giới thiệu Router về phần cứng và cấu trúc:** 

**a. Phần cứng:** phần cứng của Router gần tương đồng về các thành phần với PC

|Router|PC|
| :- | :- |
|Main|Main|
|CPU|CPU|
|RAM: là nơi chạy file Runingconfig. Bao gồm: bảng định tuyến, MAC, NAT, ACL|RAM|
|<p>+ NVRAM: là bộ nhớ lưu file cấu hình: Startup config </p><p>+ Flash: là bộ nhớ lưu file IOS</p>|HDD|
**b. Cổng kết nối:** 

|![C:\A719D885\5EA85149-8B74-4B52-B40D-09C2B792024C\_files\image001.png](Aspose.Words.934770bf-2b22-4c5a-a2bf-bfc642e41267.001.png "image001")|<p>Chúng ta có thể truy cập và điều khiển từ máy tính tới Router bằng các đường:</p><p>**-Đường console:** kết nối trực tiếp từ máy tính tới Router bằng cáp Console (một đầu cắm vào cổng com trên máy tính, một đầu cổng console của Router hoặc Switch). Cáp console có tốc độ thấp 56kb/s nên chỉ được dùng thiết lập ban đầu</p><p>**-Telnet or SSH:** kết nối tới Router hoặc Switch thông qua cổng mạng. Kết nối này có tốc độ cao và cho phép truy cập từ xa. Trong đó telnet có tốc độ nhanh hơn. Nhưng không hỗ trợ bảo mật. SSH hỗ trợ bảo mật nhưng tốc độ truyền chậm hơn. Vì vậy người ta thường dùng SSH trong những khu vực không an toàn, và Telnet trong những khu vực mạng an toàn. </p><p>**- AUX:** Chỉ hỗ trợ trên Router: cũng cho phép kết nối tới Router từ xa, thông qua đường truyền Modem. Tuy nhiên loại kết nối này thường không được sử dụng.</p>|
| :- | :- |


**c. IOS (Internetwork Operating System): Hệ điều hành của thiết bị Cisco**

\+ Tương tự như một máy tính, một router hoặc switch  hoạt động thì phải có hệ điều hành. Cisco Internetwork Operating System (IOS) là phần mềm hệ thống trong các thiết bị của Cisco. Nó là công nghệ cốt lõi được mở rộng trên hầu hết các dòng sản phẩm của Cisco

\+ Cisco IOS cung cấp cho các thiết bị với các dịch vụ mạng sau đây

=> Chức năng định tuyến và chuyển mạch

=> Tin cậy và truy cập bảo mật vào tài nguyên mạng

=> Khản năng mở rộng hệ thống.

\+ Chú ý về IOS: 

=> Hệ điều hành hoạt động là khác nhau trên từng thiết bị (Router hoặc Switch)

=> Các thiết bị đều truy cập bằng lệnh

=> File os nặng khoảng 40M. Nó được lưu trong bộ nhớ Flash. Bộ nhớ flash cung cấp lưu trữ không mất dữ liệu.

=> Sử dụng Flash memory có thể copy vào là chạy

**2. Quá trình khởi động của Router:**

=> Bước 1: Khi bật Router điện sẽ được nạp vào ROM

=> Bước 2: ROM sẽ thực hiện quá trình kiểm tra các thiết bị phần cứng gọi là POST (Power on self test)

=> Bước 3: Sau khi kiểm tra phần cứng chạy ổn định sẽ chuyển sang Bootstrap. Bootstrap sẽ liên lạc với IOS, IOS sẽ được load từ bộ nhớ Flash (bootstrap cho phép hệ điều hành nào khở động trước nếu có nhiều IOS). 

=> Bước 4: tiếp theo file cấu hình (Start up config) được copy từ bộ nhớ NVRAM

=> Bước 5:  IOS và Startup Config được load vào RAM tạo thành file chạy Running config.

**3. Các Mode lệnh trong IOS: có 4 mode lệnh**

\+ Router> ----------------------->  Mode User ( Mode có quyền thấp nhất )

\+ Router# ------------------------> Mode Previlidge (Mode quản trị)

\+ Router (config)#--------------> Mode cấu hình

\+ Router (config-if)#-----------> Mode vào cổng

**4. Các lệnh cấu hình Cơ bản Router:**

Router#configure terminal

Router(config)#----------------=> Mode config | Mode global (Mode cấu hình)

Router(config)#**host**name R1 => Đặt tên cho Router

R1(config)#

R1(config)#enable password cisco => Đặt pass enable là cisco (khi chuyển từ Mode người dùng sang Mode quản trị sẽ yêu cầu mật khẩu).

R1(config)#enable secret aptech => Đặt pass enable secret là aptech (pass này sẽ được dùng khi câu lệnh này được thực hiện. Cao hơn pass của enable)

R1(config)#

R1(config)#line console 0

R1(config-line)#password aptech => Đặt pass khi truy nhập vào Router bằng đường Console. 

R1(config-line)#login

R1(config-line)#

R1(config-line)#line vty 0 4

R1(config-line)#password aptech => Đặt pass khi truy nhập vào Router bằng đường telnet

R1(config-line)#login

R1(config-line)#exit

R1(config)#

R1(config)#banner motd !Hello! => Đặt lời chào cho Router/Switch, lưu ý ký tự bắt đầu và ký tự kết thúc của lời chào phải giống nhau.

R1(config)#

R1(config)#interface f0/0

R1(config-if)#--------------=> Mode Interface (mode cấu hình địa chỉ cổng)

R1(config-if)#no shut => Bật cổng của Rotuer lên

R1(config-if)#ip address 192.168.1.1 255.255.255.0 => Đặt địa chỉ IP cho cổng của Router.

R1(config-if)#

R1(config-if)#interface s0/0

R1(config-if)#no shut

R1(config-if)#ip address 172.16.0.1 255.255.255.252

R1(config-if)#clock rate 64000 (bật xung nhịp đối với đầu DCE)

R1(config)#

R1(config)#exit

R1#show running-config => Kiểm tra file cấu hình đang chạy. 

R1#copy running-config startup-config | write => ghi file cấu hình đang chạy vào NVRAM.

R1#show startup-config => Kiểm tra file cấu hình xem đã có những thông tin đang chạy chưa? 

Chú ý: 

=> R1(config-if)#clock rate 64000  => Clock  rate là xung nhịp của các bít truyền. Bít này cách bít kia là 64000 micro/giây

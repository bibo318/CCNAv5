IP Addressing Services

Thursday, November 29, 2012

11:11 AM

**I. Nội dung chính:**

1.Giới thiệu về dịch vụ DHCP

\2. Cấu hình DHCP

\3. Giới thiệu về NAT

\4. Cấu hình NAT Router



**II. Nội dung chi tiết:**

**1. Giới thiệu về dịch vụ DHCP:** là dịch vụ cấp phát địa chỉ IP động. Trong một hệ thống lớn có nhiều máy, thay vì chúng ta phải đi nhập IP bằng tay cho tất cả các máy thì chúng ta dùng DHCP cấp phát IP. 

\+ Để dịch vụ DHCP hoạt động được nó phải có 2 thành phần: DHCP Server và DHCP Client

=> DHCP Server dùng để cấp phát IP động sử dụng Port 68. Gửi IP hoặc nhận thông tin đều ở Port này.

=> DHCP Client dùng để nhận IP, xin cấp phát IP sử dụng Port 67. Xin IP hoặc nhận IP đều dùng ở Port này. 

\+ Có 4 bản tin được sử dụng:

=> Bản tin 1: là Discover

=> Bản tin 2: là Offer

=> Bản tin 3: là Request

=> Bản tin 4: là ACK

\+ Các bước hoạt động: 

=> Bước 1: DHCP Client sẽ gửi một bản tin Broadcast là Discover. Bản tin là thông tin yêu cầu xin địa chỉ IP. Bản tin sẽ được tầng Transport nhận bằng cổng 68 sau đó đóng gói bằng giao thức UDP  rồi truyền xuống dưới. Tầng Network Access sẽ đóng địa chỉ MAC nguồn là máy mình và MAC đích là MAC Broadcast  rồi chuyển ra đường truyền. Do có địa chỉ MAC là Broadcast nên tất cả các máy trong mạng đều nhận được, trong đó có máy DHCP Server.

=> Bước 2: Sau khi DHCP Server nhận được gói tin nó sẽ được tầng Network Access sẽ chuyển lên bên trên để xử lý. Tầng Transport sẽ nhận thông tin rồi chuyển lên Port 67 cho tầng Application.

=> Bước 3: Sau khi DHCP Server xử lý, Server sẽ gửi lại một bản tin Offer bao gồm thông tin địa chỉ IP cấp cho máy Client và thông tinh máy của mình như tên, IP. Rồi chuyển xuống cho tầng Transport đóng gói bằng cổng 67. Tầng Transport sẽ đóng bằng giao thức UDP và tiếp tục chuyển xuống đóng địa chỉ MAC nguồn MAC đích. Tiếp theo dữ liệu sẽ gửi ra đường truyền.

=> Bước 4: Client nhận dữ liệu từ Port 68 và đưa IP vào DHCP Client. Sau đó DHCP Client sẽ gửi lại một bản tin Request là đồng ý sử dụng IP đó để DHCP Server xác nhận

=> Bước 5: DHCP Server nhận được thông tin từ DHCP Client sẽ gửi lại một bản tin ACK để xác nhận là quá trình đã thành công.
**


**2. Cấu hình DHCP:**

**a. Cấu hình cơ bản:**

=> R1(config)#Service DHCP

=> R1(config)#IP dhcp pool IT

=> R1(dhcp-config)#network 192.168.1.0 255.255.255.0  (dải địa chỉ IP sẽ được dùng để cấp cho các DHCP Client)

=> R1(dhcp-config)#default-router 192.168.1.1

=> R1(dhcp-config)#dns-server 8.8.8.8 8.8.4.4

=> R1(dhcp-config)#domain-name bknpower.vn

**b. Cấu hình giới hạn giải không cấp cho Pc mà để cho Server:**

=> Đang trong mode R1(dhcp-config)# exit ra

=> R1(config)#ip dhcp excluded-address 192.168.1.1   192.168.1.10

**c. Cấu hình Relay để chuyền sang mạng khác:**

=> R2(config)#int f0/0

=> R2(config-if)#IP helper-address 192.168.1.6

=> R2(config-if)#end

**d. Lệnh kiểm tra:**

=> Dùng lệnh Show ip DHCP binding (show hết các thành phần cấu hình)

**e. Bài tập cấu hình dịch vụ DHCP và DHCP Relay:**

\+ Cho sơ đồ: 

|![C:\D06B1665\A19EC1F0-8A53-41FF-BEDE-C4CC4D9FE4D2\_files\image001.png](Aspose.Words.2ace914e-97b8-4193-8267-7655d92e2a49.001.png "image001")|
| :- |
**+ Trên Router R1, tiến hành đổi tên thành DHCPServer và cấu hình IP cho cổng f0/0**

=> R1(config)#hostname DHCPServer

=> DHCPServer(config)#interface fastEthernet 0/0

=> DHCPServer(config-if)#ip add 10.0.0.1 255.255.0.0

=> DHCPServer(config-if)#no shut

=> DHCPServer(config-if)#exit

**+ Sau đó, ta tiến hành định tuyến cho Router này luôn. Ở đây sử dụng RIP version 2 .**

=> DHCPServer(config)#router rip

=> DHCPServer(config-router)#network 10.0.0.0

=> DHCPServer(config-router)#version 2

=> DHCPServer(config-router)#no auto-summary

=> DHCPServer(config-router)#exit 

**+ Chuyển qua Router R2, ta cũng đổi tên thành DHCPRealy và lần lượt cấu hình IP cho các cổng f0/0, f0/1 và f1/0**

=> R2>en

=> R2#config t

=> R2(config)#hostname DHCPRelay

=> DHCPRelay(config)#interface fastEthernet 0/0

=> DHCPRelay(config-if)#ip add 10.0.0.2 255.255.0.0

=> DHCPRelay(config-if)#no shut

=> DHCPRelay(config-if)#exit

**+ Cấu hình IP cho cổng f0/1**

=> DHCPRelay(config)#interface fastEthernet 0/1

=> DHCPRelay(config-if)#ip add 192.168.1.1 255.255.255.0

=> DHCPRelay(config-if)#no shut

=> DHCPRelay(config-if)#exit

**+ Cấu hình IP cho cổng f1/0**

=> DHCPRelay(config)#interface fastEthernet 1/0

=> DHCPRelay(config-if)#ip add 192.168.2.1 255.255.255.0

=> DHCPRelay(config-if)#no shut

=> DHCPRelay(config-if)#exit 

**+ Trên Router R2, ta cấu hình định tuyến RIP tới 3 mạng 10.0.0.0/16, 192.168.1.0/24 và 192.168.2.0/24.**

=> DHCPRelay(config)#router rip

=> DHCPRelay(config-router)#version 2

=> DHCPRelay(config-router)#network 10.0.0.0

=> DHCPRelay(config-router)#network 192.168.1.0

=> DHCPRelay(config-router)#network 192.168.2.0

=> DHCPRelay(config-router)#no auto-summary

=> DHCPRelay(config-router)#end 

**+ Chuyển về Router DHCPServer tiếp tục cấu hình DHCP Server, tạo ra các Pool là các mạng cần cấp phát IP.** 

=> DHCPServer(config)#service dhcp

=> DHCPServer(config)#ip dhcp pool network192.168.1.0

=> DHCPServer(dhcp-config)#network 192.168.1.0 255.255.255.0

=> DHCPServer(dhcp-config)#default-router 192.168.1.1

=> DHCPServer(dhcp-config)#dns-server 8.8.8.8

=> DHCPServer(dhcp-config)#exit

=> DHCPServer(config)#service dhcp

=> DHCPServer(config)#ip dhcp pool network192.168.2.0

=> DHCPServer(dhcp-config)#network 192.168.2.0 255.255.255.0

=> DHCPServer(dhcp-config)#default-router 192.168.2.1

=> DHCPServer(dhcp-config)#dns-server 8.8.8.8

=> DHCPServer(dhcp-config)#exit

**+ Bây giờ ta chuyển qua cấu hình DHCP Relay Agent trên Router R2**

=> DHCPRelay#config t

=> DHCPRelay(config)#interface fastEthernet 0/1

=> DHCPRelay(config-if)#ip helper-address 10.0.0.1

=> DHCPRelay(config-if)#exit

=> DHCPRelay(config)#interface fastEthernet 1/0

=> DHCPRelay(config-if)#ip helper-address 10.0.0.1

=> DHCPRelay(config-if)#exit



**3. Giới thiệu về NAT & cấu hình NAT Router (Network Address Translate):** 

**a. Giới thiệu về NAT:** 

\+ Phải NAT ra ngoài để cho phép bên trong truy cập internet. 

|![C:\D06B1665\A19EC1F0-8A53-41FF-BEDE-C4CC4D9FE4D2\_files\image002.png](Aspose.Words.2ace914e-97b8-4193-8267-7655d92e2a49.002.png "image002")|
| :- |
\+ Không gian IP được chia làm 2 phần: Public và Private

=> IP Public là địa chỉ dùng cho định tuyến toàn cầu.

=> IP Private là IP của mạng LAN, mạng nội bộ, được sử dụng bở người quản trị thiết lập. Nó có thể giống nhau giữa các doanh nghiệp này và doanh nghiệp khác. Nó giúp hỗ trợ cho việc tránh hết IP Public.

\- Lớp A: 0 tới 127 => sử dụng 8 bit cho NetID

\- Lớp B: 128 tới 191 => sử dụng 16 bit cho NetID

\- Lớp C: 192 tới 223 => sử dụng 24 bit cho NetID

\+ Khi các máy bên trong gửi ra thì nó tới được đích nhưng khi Server đích gửi về nó sẽ không biết được IP Private kia là ở đâu nên sẽ bị hủy (IP Public mới có trong bảng định tuyến của Router)

\+ Để chuyển được từ IP Private ra IP Public ta dùng cơ chế NAT.

=> NAT chỉ chuyển đổi địa chỉ IP bên trong là 192.168.1.10 ra IP Public là 200.0.0.1.

=> NAT không chuyển đổi thêm bất kỳ thông số nào khác của gói tin.

=> Trong cơ chế NAT nó có một bảng được gọi là bảng NAT:

|192.168.1.10|200.0.0.1|
| :- | :- |
|192.168.1.11|200.0.0.1|


**b. Phân loại các địa chỉ IP trên Sơ đồ:** 

|![C:\D06B1665\A19EC1F0-8A53-41FF-BEDE-C4CC4D9FE4D2\_files\image003.png](Aspose.Words.2ace914e-97b8-4193-8267-7655d92e2a49.003.png "image003")|
| :- |
|Inside Local |Mọi địa chỉ của mình thì gọi là Inside Local|
|Inside Global|Mọi địa chỉ của mình nhưng do nhà cung cấp dịch vụ cấp cho gọi là Inside Global|
|Outside Global|Địa chỉ vừa bên ngoài và của người ta thì gọi là Outside Global|
|Local|Bên trong người dùng gọi là Local|
|Global|Nhà cung cấp dịch vụ gọi là Global|


**4. Cấu hình NAT Router: khảo sát các loại NAT (có 3 loại NAT):**

\+ Static NAT (NAT 1-1).

\+ Dynamic NAT (NAT 1 dải ra 1 dải).

\+ NAT Overloading (NAT có kèm theo Port nguồn).



**a. NAT Static:** Cứ một máy bên trong sẽ gán cứng cho một IP Public bên ngoài tương ứng. Thường áp dụng cho NAT Server

\+ Lệnh khởi tạo Static NAT:

=> R1(config)# ip nat inside source static 192.168.1.10 200.0.0.1 (IP bên trong ra bên ngoài).

\+ Sau khi cấu hình NAT phải vào cổng F0/0 và S0/0/0 gán thì mới có giá trị.

=> R1(config)# int f0/0

=> R1(config-if)# ip nat inside 

=> R1(config)# int s0/0/0

=> R1(config-if)# ip nat outside 



**b. Dynamic NAT:** thường dùng khi có nhiều địa chỉ IP bên trong NAT ra nhiều địa chỉ IP Public bên ngoài

\+ Các bước thực hiện: 

=> Khởi tạo dải bên trong

=> Khởi tạo dải bên ngoài

=> Map 2 dải lại với nhau

\+ Lệnh khởi tạo:

=> R1(config)# access-list 1 permit 192.168.1.0 0.0.0.7  

=> R1(config)# ip nat pool ABC 200.0.0.1 200.0.0.6 netmask 255.255.255.248

=> R1(config)# ip nat inside source list 1 pool ABC

\+ Sau khi cấu hình NAT phải vào cổng F0/0 và S0/0/0 gán thì mới có giá trị.

=> R1(config)# int f0/0

=> R1(config-if)# ip nat inside 

=> R1(config)# int s0/0/0

=> R1(config-if)# ip nat outside

\+ Nhược điểm của 2 kiểu này là bao nhiêu máy bên trong thì phải có bây nhiêu địa chỉ bên ngoài. Thường dùng cho Server dịch vụ thôi.



**c. NAT Overload là:** NAT port hay NAT dải

` `+ Lệnh khởi tạo:

=> R1(config)# access-list 1 permit 192.168.1.0 0.0.0.255

=> R1(config)# ip nat inside source list 1 interface s0/1/0 **overload** (interface là cổng bên ngoài internet kết nối về)

\+ Sau khi cấu hình NAT phải vào cổng F0/0 và S0/0/0 gán thì mới có giá trị.

=> R1(config)# int f0/0

=> R1(config-if)# ip nat inside 

=> R1(config)# int s0/0/0

=> R1(config-if)# ip nat outside

\+ Chú ý: Nếu bên ngoài có nhiều địa chỉ Public thì ta sẽ khởi tạo Pool

=> R1(config)# ip nat pool ABC 200.0.0.1 200.0.0.6 netmask 255.255.255.248

=> R1(config)# ip nat inside source list 1 pool ABC overload
**


**d. Chú ý:** để hệ thống bên trong ra ngoài được Internet ta phải dùng lệnh Default Route

=> R1(config)# ip route 0.0.0.0 0.0.0.0 s0/1/0



**e. Câu lệnh kiểm tra:** trên Router cấu hình NAT: 

\+ R# show ip nat translations

\+ R#clear ip nat translations \*     (\* là xóa tất cả bảng NAT)

\+ R#debug ip nat



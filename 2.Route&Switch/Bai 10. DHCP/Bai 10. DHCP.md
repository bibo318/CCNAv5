Giới thiệu về DHCP

**I. Nội dung chính:**

1.Giới thiệu về dịch vụ DHCP

\2. Cấu hình DHCP

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

|![C:\D06B1665\A19EC1F0-8A53-41FF-BEDE-C4CC4D9FE4D2\_files\image001.png](Aspose.Words.2a4532a1-1b36-417c-8d34-c5d7407516e3.001.png "image001")|
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

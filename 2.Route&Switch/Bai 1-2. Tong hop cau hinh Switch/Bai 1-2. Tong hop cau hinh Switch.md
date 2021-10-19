Tổng hợp cấu hình Switch Cisco

**I. Nội dung tổng quát:**

\1. Chuẩn bị trang thiết bị

\2. Nạp IOS cho Switch

\3. Cấu hình VLAN

\4. Cấu hình VTP

\5. Cấu hình STP

\6. Cấu hình Inter-VLAN

\7. Các lệnh kiểm tra trên Switch



**II. Nội dung chi tiết:**

**1. Chuẩn bị trang thiết bị**

=> Switch Cisco 2960

=> IOS Switch Cisco 2960

=> Dây Console, dây cáp thẳng

=> PC có cổng COM để cắm dây Console

=> Phần mềm PUTY để kết nối Router

=> Phần mềm TFTP Server

**2. Nạp IOS cho Switch:**
a. Nạp theo TFTP Server

b. Nạp bằng lệnh tftpdnld:

\+ Trên máy PC hoặc Server:

=> Cài đặt TFTP Server 

=> Copy IOS của Switch vào thư mục của TFTP 

\+ Trên Switch:

=>  Khởi động lại bằng tắt rồi bật nguồn và nhấn Ctrl + Break

=> Trong Rommon ta thiết lập như sau:

rommon 1 > set                                                               => Xem thông tin

rommon 2 > IP\_ADDRESS=10.10.3.100                      => Địa chỉ IP cho port

rommon 3 > IP\_SUBNET\_MASK=255.255.255.0       => Subnet mask

rommon 4 > DEFAULT\_GATEWAY=10.10.3.1         => Default gateway

rommon 5 > TFTP\_SERVER=10.10.3.1                       => Địa chỉ TFTP server

rommon 6 > TFTP\_FILE=c2600-is-mz.113-2.0.2.Q    => tên file cần nạp 

rommon 7 > sync                                                           => để lưu giá trị vào NVRAM 

rommon 8 > tftpdnld                                                     => Bắt đầu quá trình nạp

**3. Cấu hình VLAN**

**a. Cấu hình cơ bản:**

Switch#configure terminal

Switch(config)#----------------=> Mode config | Mode global (Mode cấu hình)

Switch(config)#**host**name SW1 => Đặt tên cho Switch

SW1(config)#

SW1(config)#enable password cisco => Đặt pass enable là cisco (khi chuyển từ Mode người dùng sang Mode quản trị sẽ yêu cầu mật khẩu).

SW1(config)#enable secret aptech => Đặt pass enable secret là aptech (pass này sẽ được dùng khi câu lệnh này được thực hiện. Cao hơn pass của enable)

SW1(config)#

SW1(config)#line console 0

SW1(config-line)#password aptech => Đặt pass khi truy nhập vào Switch bằng đường Console. 

SW1(config-line)#login

SW1(config-line)#exit

SW1(config)#

SW1(config-line)#line vty 0 4

SW1(config-line)#password aptech => Đặt pass khi truy nhập vào Switch bằng đường telnet

SW1(config-line)#login

SW1(config-line)#exit

SW1(config)#

SW1(config)#banner motd !Hello! => Đặt lời chào cho Switch, lưu ý ký tự bắt đầu và ký tự kết thúc của lời chào phải giống nhau.

SW1(config)#

**b. Cấu hình VLAN**

\+  Đặt tên cho VLAN:

=> SW(config)# Vlan 2

=> SW(config-vlan)# name IT

=> SW(config-vlan)# exit

\+ Gán cổng cho VLAN:

=> SW(config)# interface  range  f0/1-5

=> SW(config-if-range)#switchport access  vlan 2

\+ Gán Trunking cho cổng:

\- Đối với dòng 2900 nó hỗ trợ sẵn dot1Q nên không cần bật. Chỉ cần vào cổng bật Trunk lên là xong

=> SW(config)# interface f0/24

=> SW(config-if)#switchport mode trunk

\- Đối với dòng 3500 trở lên phải vào bật dot1Q hay ISL nó mới chạy. Nếu không bật sẽ báo lỗi:

=> SW(config)# interface f0/24

=> SW(config-if)#switchport trunk encapsulation [dot1Q hay ISL]

=> SW(config-if)#switchport mode trunk

Chú ý: thường gán cổng trunk chạy sang Switch khác hoặc về Router. 

\+ Gán Native VLAN vào VLAN quản lý:

=> SW(config)# Vlan 99

=> SW(config-vlan)# name Managerment

=> SW(config-vlan)# exit

=> SW(config)# interface f0/24

=> SW(config-if)#switchport mode trunk

=> SW(config-if)#switchport trunk native vlan 99

**4. Cấu hình VTP:** 

**a. Câu lệnh cấu hình tổng quan:**

=> SW(config)#vtp  mode [Server | Client | Transparent ]

=> SW(config)#vtp  domain  domain-name

=> SW(config)#vtp pasword  abc

=> SW(config)#vtp version number

=> SW(config)#vtp pruning

=> SW(config)#end

**b. Câu lệnh chi tiết:**

\+ Trên Switch Server:

\- Khởi tạo VTP Server:

=> SW(config)#vtp  mode Server

=> SW(config)#vtp  domain  aptech

=> SW(config)#vtp pasword  abc

=> SW(config)#vtp version 2

=> SW(config)#vtp pruning (Packet tracer không hỗ trợ). 

=> SW(config)#end 

-** Bật đường Trunking của cổng kết nối tới các SW Client:

=> SW(config)#interface f0/24

=> SW(config-if)#switchport mode trunk

\- Khởi tạo tên VLAN:

=> SW(config)#vlan 2

=> SW(config)#name IT

=> SW(config)#exit

=> SW(config)#vlan 3

=> SW(config)#name Sale

=> SW(config)#exit

\+ Trên Switch Transparent:

=> SW(config)#vtp  mode transparent

=> SW(config)#vtp  domain  aptech

=> SW(config)#vtp pasword  abc

=> SW(config)#vtp pruning  (Packet tracer không hỗ trợ).

=> SW(config)#end 

\+ Trên Switch VTP Client:

\- Khởi tạo VTP Client:

=> SW(config)#vtp  mode client

=> SW(config)#vtp  domain  aptech

=> SW(config)#vtp pasword  abc

=> SW(config)#vtp pruning  (Packet tracer không hỗ trợ).

=> SW(config)#end 

\- Gán cổng cho SW: Phải gán cổng cho SW vì VTP Server không gửi thông tin gán cổng cho Client. 

=> SW(config)#interface range f0/1-10

=> SW(config-if-range)#switchport access vlan 2

=> SW(config-if-range)#exit

=> SW(config)#interface range f0/11-20

=> SW(config-if-range)#switchport access vlan 3

=> SW(config-if-range)#exit

**5. Cấu hình STP:**

**a. Một số điểm cần lưu ý khi cấu hình Switch Cisco**

=> Mặc định Switch Cisco là bật mặc định STP. 

=> Mode default là PVST+ là mỗi VLAN chạy một cây STP

=> Switch Cisco không hỗ trợ SPT truyền thống là 802.1D mà phải PVST+ 

**b. Các lệnh hiệu chỉnh STP:** 

\+ Cấu hình Root SW: phải chỉ ra vì nó cần có cấu hình mạnh

=> Tùy chọn 1 trong 2 trường hợp: SW(config)#spanning-tree vlan  n  root [primary | secondary]

vd: SW(config)#spanning-tree vlan  3  root primary (chỉ ra Switch nào làm Root).

=> Chỉ cố định luôn: SW(config)#spanning-tree vlan  n  priority gt (giá trị priority mong muốn phải chia hết cho 4096)

vd: SW(config)#spanning-tree vlan  3  priority 8192 

\+ Cấu hình Port Fast:

=> SW(config)# int f0/10

=> SW(config-ip)# switchport mode access

=> SW(config-ip)# Spanning-tree portfast

**c. Lệnh chống bão Broadcast trên cổng cho STP:**

=> storm-control broadcast level pps 1500 1000 

\+ upper =1500 (gói giới hạn được đi qua)

\+ Low = 1000 (cảnh báo)

=> storm-control {broadcast|multicast|unicast} level {level [level-low] | bps bps [bps-low] | pps pps [pps-low]}

` `for example:

` `block at 80% utilization, unblock at 50%

storm-control broadcast level 80 50

` `or

` `block at 100 pps, unblock at 70 pps

storm-control broadcast pps 100 70

` `storm-control action {shutdown | trap}

**d. Block Unicast và Multicast Flooding:** 

=> Switch# configure terminal

=> Switch(config)# interface gigabitethernet0/1

=> Switch(config-if)# switchport block multicast

=> Switch(config-if)# switchport block unicast

=> Switch(config-if)# end

**6. Cấu hình Inter-VLAN**

\+ Chia thành 3 VLAN là: 2, 3, 4 tương ứng như sau:

=> VLAN 2: IT đường địa chỉ: 192.168.1.0/24

=> VLAN 3: Sale đường địa chỉ: 192.168.2.0/24

=> VLAN 4: Mar đường địa chỉ: 192.168.3.0/24

\+ Cấu hình VTP Server, Client

\+ Cấu hình định tuyến VLAN để các dải ping thông nhau

**Cấu hình định tuyến VLAN:** 

=> R1(config)#int f0/0

=> R1(config-if)#no shut

=> R1(config)#int f0/0.2

=> R1(config-subif)#encapsulation dot1Q 2

=> R1(config-subif)#ip add 192.168.1.1 255.255.255.0

=> R1(config-subif)#exit

=> R1(config)#int f0/0.3

=> R1(config-subif)#encapsulation dot1Q 3

=> R1(config-subif)#ip add 192.168.2.1 255.255.255.0

=> R1(config-subif)#exit

=> R1(config)#int f0/0.4

=> R1(config-subif)#encapsulation dot1Q 4

=> R1(config-subif)#ip add 192.168.3.1 255.255.255.0

=> R1(config-subif)#end

**7. Các lệnh kiểm tra trên Switch**

**a. Các lệnh kiểm tra VLAN:** 

=>SW(config)# Show vlan

=>SW(config)# Show vlan brief

=>SW(config)# Show interfaces trunk

=> chú ý: file cấu hình VLAN đặt trong bộ nhớ flash là: vlan.dad. Không lưu trong file Running config

**b. Các lệnh kiểm tra VTP:** 

=>SW(config)# show vtp status

=>SW(config)# show vtp pasword

=>SW(config)# show vlan

=>SW(config)# Show interfaces trunk

**c. Các lệnh kiểm tra STP:** 

=> Show Spanning-tree vlan  n

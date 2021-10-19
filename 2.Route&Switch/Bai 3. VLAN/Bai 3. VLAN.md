Giới thiệu về VLANs

**I. Nội dung chính:** 

\1. Tại sao phải chia VLAN

a. Xét hệ thống thông thường

b. Xét hệ thống có thiết bị hỗ trợ VLAN

\2. Tìm hiểu về VLAN 

a. Cách cách nhìn về VLAN: nhìn trên một Switch và nhìn trên Broadcast domain

b. Cách áp dụng VLAN cho các phòng ban.

\3. Các loại VLAN: bao gồm 5 loại

\4. VLAN Trunking

\5. Số hiệu VLAN

\6. Cấu hình VLAN



**II. Nội dung chi tiết**

**1. Tại sao phải chia VLAN (Virtual Local Area Network)**

**a. Xét hệ thống bình thường:**

=> Một Công ty giáo dục thuê một tòa nhà có nhiều tầng. Tầng 1 là khối văn phòng có 1 Switch (đây gọi là mạng LAN khối văn phòng bao gồm cả nhân viên tư vấn). Tầng 2  là phòng giám đốc đặt một Switch, Tầng 3 giảng viên đặt một Switch, tầng 4, 5 là của sinh viên. Tất cả các tầng đều nối ra Router và ra internet. Nhưng vào mùa tuyển sinh thì số lớp sẽ ít nhưng tư vấn viên cần nhiều (khối văn phòng chuyển lên một ít ở tầng 4 và 5). Phòng giám đốc cần thu hẹp lại để nhường phòng khác, nhưng phòng ban giám đốc lại chỉ có 3 hoặc 4 người thì thừa ra rất nhiều cổng. Hệ thống sẽ có sự tốn kém khi có thiết bị thay đổi. 

=> Do cả tòa nhà cùng Router và đi ra internet nên cùng dùng một dải mạng, cùng một Broadcast domain. Hệ thống sẽ không có độ bảo mật cao giữa các phòng ban. Khi bị Virus thì cả hệ thống có thể bị lây lan. Khi có một người đứng trong mạng có thể bắt được hết tất cả gói tin toàn mạng đi qua Router.

=> Trong một doanh nghiệp có sử dụng nhiều thành phần và ứng dụng vào hệ thống mạng như: dùng Voice IP, truy cập Web, Mail, truy cập dữ liệu trong hệ thống. Nếu bình thường thì không sao nhưng không may bị tắc nghẽn thì sẽ lỗi cả hệ thống.

**b. Xét hệ thống có thiết bị hỗ trợ VLAN** (thiết bị này đã hỗ trợ từ trước năm 2000)

=> Vẫn các Switch như vậy nhưng khi dùng VLAN nó chỉ cần kéo một dây từ Router về một Switch nào đó, sau đó sẽ chia VLAN

=> Trên một Switch 24 cổng nếu hỗ trợ VLAN thì nó sẽ chia nhỏ khu vực một cách hợp lý: VLAN 1 có cổng từ 1-10, VLAN 2 có cổng từ 11-15, VLAN 3 có cổng từ 16-24.

=> Chú ý: Cisco 2900 hỗ trợ 64 VLAN, 2950 hỗ trợ 255 VLAN, 4500 hỗ trợ 4000 VLAN

**2. Tìm hiểu về VLAN (VLAN là gì):** 

**a. Có 2 cách nhìn về VLAN:**

**+ Nhìn trên một Switch:** VLAN là một switch logical (ta có ổ cứng 80GB vật lý chia thành ổ C, D, E. Các ổ logical này là độc lập)

=> Các VLAN độc lập sẽ không Forwarding sang VLAN khác.

=> VLAN sẽ không có bảng MAC của riêng nó mà nó sử dụng chung bảng MAC của Switch vật lý. Switch vật lý sẽ xây dựng bảng MAC như sau: 

|VLAN|MAC|Cổng| |VLAN|MAC|Cổng| |VLAN|MAC|Cổng|
| :- | :- | :- | :- | :- | :- | :- | :- | :- | :- | :- |
|1|00.0c.0a|F0/1| |2|00.0c.0n|F0/11| |3|00.0c.n1|F0/16|
|1|00.0c.05|F0/2| |2|00.0b.0d|F0/12| |3|00.0c.n2|F0/17|
|1|00.0c.09|F0/3| |2|00.0c.06|F0/13| |3|00.0c.n3|F0/18|
|1|00.0c.00|F0/4| |2|00.0c.08|F0/14| |3|00.0c.n4|F0/19|
=> Trên một Switch vật lý chia thành 3 VLAN là VLAN 1, VLAN 2, VLAN 3. Sau khi chia thì 3 VLAN sẽ tương ứng là 3 Switch độc lập. Trên một Switch 24 cổng ta có VLAN 1 có cổng từ 1-10, VLAN 2 có cổng từ 11-15, VLAN 3 có cổng từ 16-24. Các máy ở VLAN 1 sẽ không trao đổi được với các máy ở VLAN 3 vì 2 VLAN này tương ứng 2 Switch độc lập.

**+ Nhìn trên cả một hệ thống:** VLAN là một Boroadcast domain.

=> Xét trên 2 Switch vật lý: 

\+ Mỗi Switch chia thành 3 VLAN giống nhau. Nguyên tắc là VLAN 1 của SW1 thông VLAN 1 của SW2, VLAN 2 của SW1 thông VLAN 2 của SW2, VLAN 3 thông VLAN 3.

|**SW1**|**SW2**|
| :- | :- |
|VLAN1|VLAN1|
|VLAN2|VLAN2|
|VLAN3|VLAN3|
\+ Để VLAN 1 thông với nhau thì trên SW1 cắm dây vào một cổng VLAN 1 kết nối sang cổng thuộc VLAN 1 của SW2, tương tự với VLAN2 và 3.

\+ Mỗi VLAN sẽ tương ứng một mạng độc lập nên gọi là một Broadcast domain.

**b. Cách áp dụng VLAN cho các phòng ban:**

\- Các phòng ban không phải dịch chuyển: IT, Sale, Mar sẽ gán tương ứng VLAN 1, 2, 3

\- Các phòng ban có dịch chuyển: Sale mở rộng và thêm tầng khác thì trên Switch tầng đó chỉ cần khởi tạo VLAN 2 và cắm vào.

\- Có 2 kiểu kết nối Switch: 

=> Kiểu một là sử dụng số lượng VLAN hạn chế, có 2 Switch kế nối với nhau, mỗi switch sẽ có VLAN 2, 3 kế nối trực tiếp với nhau gọi là Uplink (vd: VLAN 2 của Switch 1 kết nối VLAN 2 của SW2 bằng 1 dây thì các máy bên SW1 sẽ ping sang SW2).

=> Kiểu 2 là sử dụng số lượng VLAN nhiều trên một Switch thì phải sử dụng đường Trunking cho phép nhiều VLAN chạy qua giữa 2 Switch hoặc về Router (đường trunking chỉ sử dụng một dây).

\- Để các mạng LAN khác nhau truyền được dữ liệu thì phải có thiết bị định tuyến. Sử dụng Router định tuyến.

**3. Các loại VLAN:** 

**a. Xét 5 loại VLAN:**

**+ Data VLAN:**  là VLAN phổ biến nhất, được dùng cho các kết nối của người dùng. 

=> Vd: ta tạo ra các VLAN dành cho người dùng tải file, truy cập web, mail, 

**+ Default VLAN:** là VLAN mặc định tất cả các Switch đều có và khởi tạo tất cả các cổng của Switch đều nằm trong VLAN này. VLAN mặc định của Switch Cisco là VLAN 1 và chúng ta không thể thay đổi tên hay xóa VLAN này.

**+ Native VLAN:** là VLAN duy nhất trên Switch mà Frame xuất phát từ nó khi đi qua đường truyền chung cho các VLAN (đường Trunk) không phải đóng gói thêm trường VLAN ID. Mặc định Native VLAN trên mỗi Switch cisco là VLAN1.

=> Switch thường và Switch Cisco trao đổi được thông tin khi SW Cisco để chế độ Native, khi SW Cisco cấu hình VLAN thì SW thường sẽ không hiểu được VLAN ID.

**+ VLAN quản lý:** là bất cứ VLAN nào mà chúng ta cấu hình địa chỉ IP cho interface VLAN tương ứng. Địa chỉ IP này được sử dụng để telnet tới Switch và điều hành hoạt động của Switch từ xa. 

**+ VLAN voice:** là một VLAN có độ ưu tiên cao nhất vì Voice là một VLAN ứng dụng thời gian thực. (mạng nghẽn voice vẫn chạy được).

**b. Xét 3 kiểu VLAN**

\+ Từ 5 loại trên ta chia thành 3 kiểu:

\- Static VLAN: là VLAN tĩnh phân chia theo cổng. Cắm máy vào cổng nào thì nó sẽ theo VLAN đó.

\- Dynamic VLAN: quy định theo địa chỉ MAC, trên Switch gán MAC: 111111 là của PC1 thuộc VLAN 10 thì Pc1 có cắm vào bất kì cổng nào trên Switch nó vẫn thuộc VLAN 10. Để gán được MAC vào VLAN thì ta phải có một VMPS Server (VLAN Mangerment Policy Server)

\- Voice VLAN: chỉ dành riêng cho dữ liệu Voice. 

=> Chú ý: thông thường hay dùng Static VLAN. 

**4. VLAN Trunking:**

a. VLAN trunking trong công nghệ VLAN: là đường truyền giữa 2 Switch được chia làm 2 loại:

\+ 1 là đường Access, cho phép các Frame thông thường đi qua

\+ 2 là đường Trunking cho phép nhiều miền VLAN đi qua. Đường Trunk cho phép tối thiểu là 100Mbps trở lên.

b. Cách thức hoạt động của đường Trunking: 

\+ Đường Trunking nhận diện frame: Khi frame đi vào đường Trunking sẽ được tạo đánh nhãn (taglink), còn khi ra khỏi thì Untrunking. 

=> Khi Farme thuộc VLAN 2 đi vào đường Trunk sẽ được gán nhãn là số 2, khi ra khỏi đường Trunk nó thấy nhãn là số 2 sẽ tách ra và đưa vào VLAN 2.  

=> Khi máy các máy trao đổi thông tin thì các Frame này là nguyên bản. Các thông tin VLAN chỉ được gán thêm khi di chuyển qua đường Trunk.

\+ Switch là Ethernet nên để đưa được thông tin vào trong Frame thì nó nhờ vào một trong 2 giao thức sau: là ISL và dot1Q

=> ISL là chạy mặc định trên Switch layer 3 (Inter Switch Link chỉ dành riêng cho thiết bị Cisco). 

=> dot1Q hộ trợ mặc định trên Switch layer 2 (IEEE 802.1Q).

=> Tìm hiểu về chuẩn dot1Q: 

\- Xét 802.1Q header: ở chế độ bình thường

|Dest.Address|Source Address|Leg./Type|Data|FCS|
| :- | :- | :- | :- | :- |
\- Khi đi vào Trunking:

|Dest.Address|Source Address|**Tag (new)**|Len./Type|Data|FCS|
| :- | :- | :- | :- | :- | :- |
\- Trong Tag có các thành phần dài 4byetes như sau:

|Type (16Bits, 0x8100)|Priority (3Bits)|Flag(1bit)|**VLAN ID (12Bits)**|
| :- | :- | :- | :- |
\- Chỉ trong dot1Q hỗ trợ Native VLAN. Native VLAN ở 2 đầu của đường Trunk phải thống nhất thông số vớ nhau. Bên SW1 là 1 thì bên SW2 cũng phải là 1.

=> Tìm hiểu về chuẩn ISL: Cisco ghép thêm 26 bytes và đầu header:

|ISL Header 26 bytes|Encapsulated Ethernet Frame|CRC 4bytes|
| :- | :- | :- |
\- 26 bytes có các thành phần sau:

|DA|Type|User|SA|LEN|AAA03|HSA |VLAN|BPDU|INDEX|RES|
| :- | :- | :- | :- | :- | :- | :- | :- | :- | :- | :- |
\+ Chú ý: đối với dòng 2900 thì nó hỗ trợ mặc định là 802.1Q còn dòng 3500 trở lên thì phải cấu hình rõ là ISL hay dot1Q

**5. Số hiệu VLAN:** 

=> chạy từ 0 tới 4095:  riêng VLAN 0 và 4095 là không dùng

=> 1 tới 1001 là VLAN thông thường

=> 1002 tới 1005: dùng để giao tiếp với mạng kiểu cũ Tokenring

=> 1006 tới 4094: dùng làm giải mở rộng sẽ cấu hình Transperent (học sau)

=> Các VLAN mặc định sau không được sửa xóa: VLAN 1 là default, 1002 tới 1005. Ban đầu tất cả các cổng của Switch cisco mặc định là VLAN 1. 

**6. Cấu hình VLAN:** 

a. Đặt tên cho VLAN:

=> SW(config)# Vlan 2

=> SW(config-vlan)# name IT

=> SW(config-vlan)# exit

b. Gán cổng cho VLAN:

=> SW(config)# interface  range  f0/1-5

=> SW(config-if-range)#switchport access  vlan 2

c. Gán Trunking cho cổng:

\+ Đối với dòng 2900 nó hỗ trợ sẵn dot1Q nên không cần bật. Chỉ cần vào cổng bật Trunk lên là xong

=> SW(config)# interface f0/24

=> SW(config-if)#switchport mode trunk

\+ Đối với dòng 3500 trở lên phải vào bật dot1Q hay ISL nó mới chạy. Nếu không bật sẽ báo lỗi:

=> SW(config)# interface f0/24

=> SW(config-if)#switchport trunk encapsulation [dot1Q hay ISL]

=> SW(config-if)#switchport mode trunk

Chú ý: thường gán cổng trunk chạy sang Switch khác hoặc về Router. 

d. Gán Native VLAN vào VLAN quản lý:

=> SW(config)# Vlan 100

=> SW(config-vlan)# name Managerment

=> SW(config-vlan)# exit

=> SW(config)# interface f0/24 (phải có 2 lệnh)

=> SW(config-if)#switchport access vlan 100 

=> SW(config-if)#switchport native vlan 100

=> SW(config-if)#exit

=> SW(config)#interface vlan 100

=> SW(config-if)#ip add 192.168.1.1 255.255.255.0

` `e. Cấu hình trên thực tế về VLAN1, VLAN NATIVE, VLAN DEFAULT trên cùn VLAN1 (đi làm cần phần này):

=> SW0(config)#interface vlan 1

=> SW0(config-if)#ip add 11.0.0.254 255.255.255.0

=> SW0(config-if)#no shut

=> SW0(config-if)#exit

=> SW1(config)#interface vlan 1

=> SW0(config-if)#ip add 11.0.0.253 255.255.255.0

=> SW0(config-if)#no shut

=> SW0(config-if)#exit

=> CORE(config)#interface f0/0.1

=> CORE(config-subif)#encapsulation dot1Q 1

=> CORE(config-subif)#ip add 11.0.0.1 255.255.255.0

=> CORE(config-subif)#exit

Trên tất cả các thiết bị đều phải đặt mật khẩu

=> SW(config)#line console 0

=> SW(config-line)#password abc

=> SW(config-line)#login

=> SW(config-line)#exit

=> SW(config)#line vty 0 4

=> SW(config-line)#password abc

=> SW(config-line)#login

=> SW(config-line)#exit

=> SW(config)#enable secret cisco

Trên PC dùng lệnh: telnet 11.0.0.x để truy cập từ xa

f. Các lệnh kiểm tra: 

=>SW(config)# Show vlan

=>SW(config)# Show vlan brief

=>SW(config)# Show interfaces trunk

=>SW(config)# Show mac-address-table 

=> chú ý: file cấu hình VLAN đặt trong bộ nhớ flash là: vlan.dad. Không lưu trong file Running config

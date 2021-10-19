**Link state OSPF**

**I. Nội dung chính**

\1. Sử dụng kiểu Link State, AD=110, Metric=Cost

\2. Hoạt động:

\+ Router ID

\+ Thiết lập Neighbor

\+ Trao đổi LSDB (Link State Database)

\+ Xây dựng bảng định tuyến

\3. Cách tính Metric:  Cost=108 /bandwidth

\4. Cấu hình: 

\+ Wildcard mask

\+ Các lệnh cấu hình 

**II. Nội dung chi tiết**

**1. Link State:** là giao thức xây dựng đường đi tốt nhất (Shortest path first) thông qua giải thuật Dijkstra. Các router chỉ cần trao đổi thông tin của nhau qua gói tin Hello mà không cần gửi cả bảng định tuyến. Sau khi có thông tin nó sẽ xây dựng ra một bảng định tuyến và đường đi tốt nhất.

\+ Chỉ số AD: là chỉ số tin cậy của các giao thức. 

\+ Cost: là giá trị được tính theo công thức 108/Bandwidth  

\+ OSPF chạy trên nền IP còn RIP chạy trên giao thức UDP

\+ Các gói tin IP vận chuyện các gói tin OSPF thì trường Protocol- ID = 89

**2. Hoạt động:** Router chạy theo OSPF thì nó phải trải qua 4 bước:

\+ Router ID

\+ Thiết lập Neighbor

\+ Trao đổi LSDB (Link State Database)

\+ Xây dựng bảng định tuyến

**a. Router ID là gì:** đơn giản là một giá trị dùng định danh cho Router khi dùng giao thức OSPF

\- Có định dạng của một địa chỉ IP A.B.C.D. Có định dạng là địa chỉ IP chứ không phải là địa chỉ IP

\- Lấy IP cao nhất trong các Interface đang hoạt động và ưu tiên cổng Loopback. 

\+ IP cao nhất: là địa chỉ IP cao nhất. IP có octet đầu cao hơn được xem là lớn hơn

Vd:  1, 192.168.1.1,

2, 192.168.1.2,       => là lớn nhất (xét từ 192, sau đó sang 168 sau đó sang 1 và cuối cùng là 2)

3, 172.16.255.255,

4, 10.255.255.254. 

Địa chỉ 2 > 1 > 3 > 4

Vậy ID của Router ở đây là 192.168.1.2

\+ Interface active: là cổng đang (up/up) Status up và protocol up.

\+ Cổng Loopback sẽ được ưu tiên hơn vì nó ít bị hỏng và ổn định. 

**b. Thiết lập quan hệ láng giềng:** 

\+ Các Router sẽ gửi gói tin Hello (10s/1 lần). Được dùng để tìm ra router láng giềng, chuyển một quan hệ láng giềng sang trạng thái 2 bước (2- Way), sau đó Hello giúp giám sát láng giếng khi nó bị lỗi.

\+ Lần đầu tiên gói tin Hello gửi tới địa chỉ 224.0.0.6 

\+ 2 Router phải thỏa mãn các điều kiện sau mới được gọi là láng giềng (phải đảm bảo 5 thông tin):

=> Cùng Area-id: Khi mạng lớn người ta chia làm nhiều vùng, vùng nào hỏng thì chỉ vùng đó chịu tác động. Mỗi một vùng sẽ đặt cho một Area-id. Vùng trung tâm có Area-id phải bằng 0. Mọi vùng khác phải có đường truyền trực tiếp về vùng 0 nó mới truyền được dữ liệu.

=> Cùng Subnet: 2 ip phải cùng Subnet mới ping và trao đổi được thông tin.

=> Phải cùng thông số: Hello/Dead-time ở trên 2 cổng. Mặc định Hello là 10s, Dead là 40s sau 40s nó sẻ hủy kết nối.

=> Phải cùng Xác thực trên 2 cổng. Dành cho mạng lớn (metro). Khi đặt xác thực các router khác không lấy được thông tin.

=> Phải cùng cờ Stub Area Flag: dành cho OSPF đa vùng (học trong CCNP)

\+ Để xem được hàng xóm dùng lệnh: Show IP OSPF Neighbor

**c. Trao đổi LSDB (Link State Database):** Mỗi Router đều chưa một bảng LSDB

\+ LSDP: Link State Database. Do nó lớn nên nó chia nhỏ ra thành các bản LSA để gửi

\+ LSA: Link State Advertisement. Để gửi được LSA thì nó phải đóng gói vào bản tin LSU

\+ LSU: là Link State Update. Để trao đổi và gửi được LSU thì nó có 2 kiểu môi trường gửi:

\- Point - to - Point: 2 router chạy với nhau theo giao thức HDLC hayPPP.  Sau khi nó kết nối được hàng xóm thì chỉ có 2 Router  trao đổi trực tiếp gọi là Full -

\- Broadcast Multiaccess: là nhiều Router kết nối với nhau thông qua một Swtich. R1, R2, R3, R4 cùng kết nối vào 1 Switch. Lúc này nó trao đổi LSDB sẽ khác hoàng toàn. 

\+ Trong 4 Router sẽ bầu ra một Router làm DR-Desigted Router, 3 router còn lại sẽ bầu ra một BDR-Backup DR.

\+ Các Router còn lại sẽ là DR Other. 2 Router là DR Other sẽ không gửi trực tiếp với nhau. Nó sẽ gửi thông tin về DR 1 bản và 1 bản cho BDR. Sau đó DR sẽ gửi phân phối xuống cho các Router còn lại. 

\+ DR Other sẽ gử thông tin về DR bằng địa chỉ 224.0.0.6. DR sẽ gửi LSDB cho DR Other là 224.0.0.5.

\+ Tiêu chí nào được bầu làm DR và BDR:

\- Trên mỗi cổng kết nối của các Router sẽ có một tham số: Priority(0-255) mặc định là 1. Con nào cao nhất là DR và con nào thấp hơn là BDR. 

\- Câu lệnh: R(config)# int F0/1 => R(config -if)# ip ospf  priority (0-255)

\- Nếu không may có Priority là bằng nhau nó sẽ dựa vào Router - ID. Router có Router-id cao nhất là DR

\- Nếu hệ thống đã có DR và BDR nếu cắm thêm một Router mới có DR cao hơn nó vẫn ưu tiên DR đang hoạt động. 

\- Nếu để Priority là 0 nó sẽ không bầu DR hay BDR

**c. Xây dựng bảng định tuyến nó dùng giải thuật Dijkstra để đưa ra đường đi tốt nhất**

**3. Cách tính Metric:**  Cost=10^8 /bandwidth

\+ Băng thông phải đổi ra đơn vị: bps

\+ Vd: 

|BW|Cost|Cách tính|
| :- | :- | :- |
|10Mbps|10|10^8 /107|
|100Mbps|1|10^8 /10^8|
|1,544Mbps|64|10^8 /1,5.106 = 100/1,5|
**4. Cấu hình:** 

**+ Wildcard mask:** là một công cụ lấy ra địa chỉ IP của một dải rất linh hoạt. Nó là một dãy nhị phân 32 bit được dùng kèm với một địa chỉ IP tham chiếu nào đó. Bit của địa chỉ IP tương ứng với Bit 0 là cố định, bit của IP tương ứng với bit 1 sẽ cố định.

Vd: 192.168.1.0/24

Ta có: IP:192.168.1.0

`   `WCM: 0  . 0 .  0.255

Vd: 192.168.1.32/27

Ta có: IP: 192.168.1.001xxxxx

`    `WCM:  0 . 0 . 0 .00011111 => 0.0.0.31

**+ Các lệnh cấu hình:**

\1. Chạy OSPF:

\- R(config)# Router  OSPF  Process-id (1-65535) chỉ có ý nghĩa nội bộ. 

\- R(config-Router)# network 192.168.1.0  0.0.0.31  area  0  (Areal là cùng mạng thành phần này rất quan trọng)

\- R(config-Router)#default-information originate 

\- Router(config-router)#redistribute connected [metric cost] subnet.

b2. Hiệu chỉnh OSPF:

\- Router - ID: 

=> R(config)# Router  OSPF  10

=> R(config-router)# router-id  a.b.c.d (nhập ip vào, IP chính là ID)

=> Sau đó trở ra mode quản trị:

=> R(config)#  Clear ip ospf  process  thì nó mới có hiệu lực

\- Priority:

=> R(config)# int f0/0

=> R(config-if)# ip  ospf  priority 

\- Hello/Dead time:

=> R(config-if)# ip  ospf  hello-interval  thời gian (là giây)

=> R(config-if)# ip  ospf  dead-interval  thời gian (là giây) 

\3. Xác thực trên 2 router:

Vào trong cổng:

=> R(config-if)# ip   ospf   authentiacation  [MD5]

Nếu điền key:

=> R(config-if)# ip   ospf   authentiacation-key   aptech

\4. Các lệnh Show:

=> Show  ip  router  ospf

=> Show  ip  ospf  neighbor

=> Show  ip  ospf  database

=> Show  ip  ospf  interface

=> Show  ip  protocol 

**5. Chú ý:**  dùng lệnh Show  ip  router:

10.0.0.0/24 is subnetted, 1 subnets

O E2 10.0.0.0 [110/20] via 192.168.1.20, 00:00:53, Serial0/1/0 => tương ứng #redistribute connected [metric cost] subnet.

C 192.168.1.0/24 is directly connected, Serial0/1/0

C 192.168.2.0/24 is directly connected, FastEthernet0/0

O 192.168.3.0/24 [110/65] via 192.168.1.20, 00:00:53, Serial0/1/0

O\*E2 0.0.0.0/0 [110/1] via 192.168.1.20, 00:00:11, Serial0/1/0  => tương ứng: #default-information originate 

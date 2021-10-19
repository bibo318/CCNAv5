**Giới thiệu về giao thức EIGRP**

**I.** **Nội dung chính:**

\1. Giới thiệu lại giao thức Distance Vector và Link State

\- Distance Vector: ứng dụng RIPv2

\- Link State: ứng dụng cho OSPF

\- EIGRP: Enhanced internet getway routing protocol  (giao thức độc quyền của Cisco) kết hợp giữa DV và LS

\2. Các đặc điểm hoạt động được cải tiến:

\- Chúng ta sẽ tìm hiểu 11 đặc điểm cải tiến.

\3. Nguyên lý hoạt động: 

\- Dựa trên nguyên lý hoạt động của 3 bảng:

\+ Neghbor table

\+ Topology table

\+ Router table

\4. Các lệnh cấu hình

\5. Cơ chế cần bằng tải của EIGRP

**II. Nội dung chi tiết:** 

**1. Giới thiệu lại giao thức Distance Vector và Link State**

\- EIGRP: là giao thức độc quyền của Cisco kết hợp giữa DV và LS

**2. Các đặc điểm hoạt động được cải tiến:**

\+ Là giao thức nâng cao của Distance Vector (Advanced DV) kết hợp với Link State: có sử dụng tới 3 bảng là Neighbor, Topology, Routing. Bảng topology lưu toàn bộ thông tin đường đi, các tuyến router. Nên nó gần giống Link State.

\+ Tính hột tụ nhanh (Rapid Convergence): do nó tổng hợp được bảng định tuyến topology

\+ Hỗ trợ cơ chế là Classless và có 100% cơ chế chống Loop.

\+ Rất dễ cấu hình, dễ hơn ospf

\+ Hỗ trợ tốt hơn khả năng cập nhật bảng định tuyến (Incremental Update). Đặc điểm của Distance Vector là mỗi router sẽ gửi bảng định tuyến theo định kỳ 30s. Nhưng Router chạy EIGRP chỉ gửi bảng định tuyến cho nhau lần đầu tiên, sau đó chỉ gửi những cập nhật những sự thay đổi cho những Router cần nó mà thôi.

\+ Khả năng cân bằng tải qua những đường không đều nhau. Trong giao thức định tuyến khi router chỉ ra được 2 đường có Metric như nhau thì Router sẽ đẩy gói tin cho cả 2 đường. Cân bằng tải chỉ diễn ra khi 2 đường có Metric như nhau, nhưng EIGRP sẽ cho phép chạy cân bằng tải khi 2 đường có Metric khác nhau theo tỉ lệ phân chia rất khôn khéo.

\+ Thiết kế mạng linh hoạt (so sánh với OSPF). OSPF phải chia ra router nào là mạng chính theo Area. EIGRP sử dụng theo mạng Peer to Peer, chỉ cần cấu hình và cắm vào là chạy.

\+ Sử dụng địa chỉ Multicast: RIPv2 là 224.0.0.9, OSPF: 224.0.0.5, 224.0.0.6. EIGRP: 224.0.0.10.

\+ Hỗ trợ VLSM và mạng gián đoạn.

\+ Có thể hỗ trợ tóm tắt bằng tay trong bất kỳ điểm nào trong mạng. Kỹ thuật tóm tắt địa chỉ là kỹ thuật gom nhiều địa chỉ mạng con thành một địa chỉ IP mạng lớn rồi gửi vào các bảng thông tin định tuyến. Nó làm giảm thiểu kích thước của bảng định tuyến. Thông thường Router nó sẽ tự động Autosammury. Có thể tiến hành tóm tắt bằng tay trên bất kỳ một Router nào (dùng tay đặt câu lệnh). OSPF phải làm trên DR hoặc BDR.

\+ Hỗ trợ định tuyến cho đa giao thức lớp 3: Ipx, Apple talk, IP. OSPF chỉ mình IP

**3. Nguyên lý hoạt động:** 

Các bảng EIGRP sử dụng 3 bảng:

**+ Neighbor table:** là liệt kê các hàng xóm kết nối trực tiếp với mình. Sau khi xây dựng xong Neighbor nó sẽ gửi thông tin sang bảng Topology để xử lý. 

**+ Topology table:** Router lưu lại các bảng Neighbor, Sau đó  nó sẽ sử dụng một thuật toán DUAL (Diffusing Update Algorithm) để tính rồi đưa ra đường đi tốt nhất. Khi có đường đi tốt nhất nó sẽ gửi sang bảng Router table.

**+ Router table:** làm nhiệm vụ định tuyến. Nó định tuyến rất nhanh vì đã có thông tin sẵn được Topology gửi sang.

==> **Neighbor:** Các Router sẽ định kì 5s gửi gói tin Hello / thời gian giữ gói tin hello là 15s (holdtimer). Sau 15s nó coi hàng xóm là chết. Hello và Holdtime ở 2 cổng kết nối 2 Router không cần phải giống nhau (OSPF phải giống).

\+ Cùng AS: là một routing domain. Khi chạy sẽ gép vào một miền để quản lý.Khi khai bảo EIGRP thì router phải chỉ ra cùng một AS thì mới trao đổi được thông tin.

\+ Cùng Subnet: 2 router được đấu nối với nhau bởi địa chỉ IP 1 và 2, Sử dụng Protocol ID là 88. IP phải kết nối thông.

\+ Cùng xác thực: 2 Pasword phải giống nhau. Sử dụng MD5

\+ Cùng tham số K: Metric trong EIGRP là bộ tham số tính rất phức tạp. Là một hàm bao gồm các thông số:

=> Metric = f(BW,delay,Reliability,load). Được điều chỉnh bằng tham số K, từ K1,K2,K3,K4,K5. K ở 2 Router phải khớp nhau. 

\- Công thức tính Metric mặc định: chỉ tính toán trên 2 tham số là: bandwidth và delay.

\+ Metric= (K1x(107/ băng thông) x 256) + (K3 x (tổng độ trễ/10) x 256). Bandwidth tính bằng Kbp, độ trễ tính bằng tổng độ trễ trên toàn tuyến đường (đơn vị là Micro giây).

\- Công thức tính Metric tổng hơp: 

|![C:\4E72CE85\F1ED859C-AB82-4555-A89D-EA45C73EED23\_files\image001.png](Aspose.Words.4b192976-f87d-41ee-bf55-31c77b2f1405.001.png "image001")|![C:\4E72CE85\F1ED859C-AB82-4555-A89D-EA45C73EED23\_files\image002.png](Aspose.Words.4b192976-f87d-41ee-bf55-31c77b2f1405.002.png "image002")|
| :- | :- |
**\*** Neighbor là thiết lập theo từng cặp: Khi thiết lập xong thì được gọi Adjacency (hoạt động luôn). Khác với OSPF là phải bầu DR, BDR. Ở đây EIGRP sau khi thiết lập nó trao đổi luôn dữ liệu. Khi R1, R2, R3 gửi thông tin tới R4 thì nó sẽ tập hợp và xây dựng ra đường tốt nhất sau đó đưa vào bảng Topology.

**\*** Router sẽ trao đổi 5 bản tin là:  Hello, Reply, Request, update, ACK

**- Gói tin Hello:** là đưa ra lời chào trước rồi mới thương thảo. Thiết lập mối quan hệ hàng xóm giữa các Router chạy EIGRP. Chỉ khi quan hệ này được thiết lập các rouer này mới gửi định tuyến cho nhau.

\- **Gói Reply:** Trả lời lại để xác nhận thông tin

\- **Gói Request:** Gửi yêu cầu cập nhật bảng Neighbor

\- **Gói Update:** Cập nhật thông tin các bảng Neighbor

\- **Gói ACK:** EIGRP dùng giao thức vận chuyển tin cậy (Reliable Transprot Protocol - RTP) để gửi thông điệp cập nhật. EIGRP gửi cập nhật, chờ thông tin xác nhận ACK từ mỗi router nhận. Nếu một ACK không nhận được sau 16 lần truyền lại, Router láng giềng sẽ coi như bị chết. (Acknowledgement)

==> **Topology:**  

|![C:\4E72CE85\F1ED859C-AB82-4555-A89D-EA45C73EED23\_files\image003.png](Aspose.Words.4b192976-f87d-41ee-bf55-31c77b2f1405.003.png "image003")|<p> </p><p> </p>| | | |
| :- | :- | :- | :- | :- |
|Network|Next-hop|FD|AD| |
|A|R1|1000|900|=> Successor|
|A|R2|2000|1100| |
|A|R3|3000|800|= > Feasible Successor|
\- Trên một đường đi có 2 giá trị Metric đi kèm:

\+ FD: Feasible Distance => tính từ đầu tới cuối chặng đường (R-R4 = 1000)

\+ AD: Advertised Distance => tính từ router hàng xóm tới cuối R1-R4. Chú ý từ AD này khác với từ khoảng cách quản trị là Administrative Distance (độ tin cậy của các giao thức). 

\+ Một số sách thì AD này còn có tên gọi là RD-Reported Distance.

\+ Bảng topology sẽ lưu tất cả các thông tin vào bảng. Bao gồm tất cả các Router đến tất cả mọi địa chỉ tron mạng.

\- Từ Topology này Router sẽ sử dụng thuật toán DUAL (Diffusing Update Algorithm) chọn ra một đường đi tối ưu:

\+ FDmin = Successor (đường đi nhỏ nhất) => đường R1 gọi là đường Successor 

\+ Trong tất cả các đường còn lại: FD > FDmin mà AD < FDmin = Feasible Successor  => R3 

\+ Đường Successor sẽ đưa vào bảng định tuyến còn Feasible Successor sẽ làm Backup.

\+ Chú ý: Phải đưa ra AD < FDmin thì sẽ không xẩy ra Loop trong hệ thống. Nếu không có AD ( AD > FD min) thì nó sẽ hội tụ chậm hơn một chút vì nó phải  yêu cầu Neighbor gửi gói tin ra hệ thống để lấy thông tin và cập nhật lại bảng Topology. EIGRP không bao giờ bị Loop.

\+ Lệnh để xem: Show  IP EIGRP  Topology

**4. Các lệnh cấu hình:**

a. Cấu hình cơ bản:

\- R1(config)# Router  eigrp  10  (10 là Autonomous-System cấu trúc gần giống OSPF là Process-id. Của OSPF chỉ là phân biệt giữa Router này và router kia. Còn AS ở đây phải giống nhau trên tất cả các Router để thể hiện mạng đó. Gần giống Area-ID của OSPF )

\- R1(config-router)#network  network-number

\- R1(config-router)#redistribute connected (quảng bá những đường Connected)

\- R1(config-router)#redistribute static (sẽ quảng bá cả Defaul Router và Static)

==> Trường hợp 1: xét 3 mạng tổng là khác nhau (10.0.0.0, 172.16.0.0, 192.168.1.0)

|![C:\4E72CE85\F1ED859C-AB82-4555-A89D-EA45C73EED23\_files\image004.png](Aspose.Words.4b192976-f87d-41ee-bf55-31c77b2f1405.004.png "image004")|
| :- |
==> Trường hợp 2: có sử dụng VLSM thì phải sử dụng Wildcard mask

|![C:\4E72CE85\F1ED859C-AB82-4555-A89D-EA45C73EED23\_files\image005.png](Aspose.Words.4b192976-f87d-41ee-bf55-31c77b2f1405.005.png "image005")|
| :- |
==> Trường hợp 3: khi quảng bá nếu để mặc định nó sẽ tự động Auto Summary về đường mạng tổng dẫn tới có thể bị lỗi khi định tuyến.  

|![C:\4E72CE85\F1ED859C-AB82-4555-A89D-EA45C73EED23\_files\image006.png](Aspose.Words.4b192976-f87d-41ee-bf55-31c77b2f1405.006.png "image006")|
| :- |
b. hiệu chỉnh EIGRP:

\- Hello/Hold-time:

=> Router(config-if)#ip hello-interval eigrp as-number seconds

=> Router(config-if)#ip hold-time eigrp as-number seconds

c. Các lệnh Show:

=> Show  ip  router  eigrp

=> Show  ip  eigrp  neighbor

=> Show  ip  eigrp interface

=> Show  ip  protocol

=> Show  ip eigrp topology

**5. Cơ chế cần bằng tải của EIGRP:**

\- EIGRP hỗ trợ cân bằng tải trên 2 đường là FDmin và FD (Successor, Feasible Successor)

\- Câu lệnh:

R1(config)# route  eigrp 200

R1(config-router)# variance  multiplier  (nếu multiplier đặt là 3, đường successor  là 20 ta sẽ có 3x20 =60. Nếu 60 > FD thì nó sẽ chọn FD làm đường cân bằng tải.

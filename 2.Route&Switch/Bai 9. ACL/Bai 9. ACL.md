ACLs: Access Control List

**I. Nội dung chính:**

\1. Giới thiệu về Access List

\2. Tìm hiểu về các loại Access List là Standard và Extanded

\3. Named ACL

\4. Câu lệnh kiểm tra

**II. Nội dung chi tiết:**

**1. Giới thiệu về Access list:**

**a. Access List:** là một công cụ đặc biệt trên hệ điều hành Cisco. ACL là một danh sách điều khiển truy nhập dùng để lọc gói tin lớp 3 và phân loại dữ liệu.

=> Phân loại dữ liệu được áp dụng cho các dịch vụ: NAT, Distribute-list, VPN

=> Lọc gói tin lớp 3. Đóng vai trò là một chốt canh khi gán vào một cổng của Router, chốt canh sẽ cho phép dữ liệu đi qua hay bị chặn.

=> Access list đơn thuần chỉ là một danh sách, nếu chúng ta không áp vào đâu hoặc sử dụng vào mục đích gì thì sẽ không có tác dụng.

**b. Access list dùng để lọc gói tin lớp 3:** 

\+ Xét sơ đồ mạng như sau:

|![C:\8F534E45\5FE46E0B-0C20-44DE-B3A9-CBA1C78F3E21\_files\image001.png](Aspose.Words.b5374c43-4222-45f9-86b9-040c3e64467a.001.png "image001")|
| :- |
\+ Chỉ cho phép mạng 192.168.1.0/24 đi ra Internet thông qua cổng S0/1/0. Access list sẽ có 2 từ khóa: Permit (cho phép) và Deny (chặn)

=> Câu lệnh: R1(config)#access-list 10 permit 192.168.1.0  0.0.0.255   (trong đó: 0.0.0.255 là wildcard mask).

\+ Access-list khởi tạo lên không có tác dụng mà phải đặt lên cổng. Ở đây ta đặt lên cổng S0/1/0 theo chiều Out

=> Câu lệnh: 

\- R1(config)# int f0/0

\- R1(config-if)# ip access-group 10 out

\+ Cách thức làm việc của Access list: 

=> Khi các máy bên trong mạng 192.168.1.0 gửi gói tin ra ngoài Internet dữ liệu sẽ chuyển tới Router và chuyển ra cổng bên ngoài là S0/1/0. Lúc này dữ liệu sẽ gặp chốt Access-list, Access-list sẽ kiểm tra thấy Permit mạng 192.168.1.0 nên nó cho phép đi qua.

=> Khi các máy bên mạng 192.168.2.0 đi ra Access-list trên cổng S0/1/0 sẽ kiểm tra, nó không thấy mạng này trong danh sách cho phép đi qua nên sẽ hủy bỏ.

\+ Chú ý: 

=> Access list theo chiều Out là quản lý dữ liệu từ bên trong ra

=> Access list teo chiều In là quản lý dữ liệu từ bên ngoài đi vào

=> Trên mỗi cổng của Access list chỉ được gán một Access list theo một chiều ( khi đã viết mệnh đề và gán cho mạng 192.168.1.0 theo chiều Out, nếu ta viết mệnh đề gán cho mạng 192.168.2.0 cũng đặt trên cổng S0/1/0 và theo chiều Out sẽ không có kết quả).

=> Nếu đã gán mạng 192.168.1.0 theo chiều Out để giám sát trên cổng S0/1/0 thì ta có thể gán chiều In để giám sát lưu lượng vào cho mạng 192.168.2.0

**2. Tìm hiểu về các loại Access List:** 

|![C:\8F534E45\5FE46E0B-0C20-44DE-B3A9-CBA1C78F3E21\_files\image002.png](Aspose.Words.b5374c43-4222-45f9-86b9-040c3e64467a.002.png "image002")|
| :- |
**a. Standard Access list ( AL tiêu chuẩn**): chỉ kiểm tra IP nguồn (Source IP) của gói tin đi tới

=> R(config)# access-list  n  [permit | deny] địa chỉ IP  wildcard   (n của dạng Stanrd chạy từ 1 tới 99)

=> Gán vào cổng theo chiều nào:

\- R1(config)# int f0/0

\- R1(config-if)# ip access-group n [in, out]

\+ Ví dụ: Cấm mạng 192.168.1.0/24 truy cập vào mạng 192.168.20.1

=> R2(config)# access-list  1  deny  192.168.1.0 0.0.0.255 

=> Gán vào cổng f0/1 theo chiều out :

\- R1(config)# int f0/1

\- R1(config-if)# ip access-group n out

\+  Bảng Access list sẽ xét cấp độ ưu tiên từ các dòng bên trên rồi mới xuống các dòng bên dưới

\- R(config)# access-list  1  deny  192.168.1.0 0.0.0.255  (dòng này thực thi trước)

\- R(config)# access-list  1  permit any   (Sau khi thực hiện yêu cầu trên thì dòng này mới đến lượt)

\- R(config)# access-list  1  deny any  (dòng này mặc định luôn bật ở cuối cùng trong access list)

\+ Khi viết Access list phải chú ý thứ tự các dòng để thiết lập. Khi đã viết rồi chúng ta không thể sửa được mà chỉ bỏ access list đó đi (dùng lệnh no access list 1).

**b. Extanded Access list (AL mở rộng):**

|![C:\8F534E45\5FE46E0B-0C20-44DE-B3A9-CBA1C78F3E21\_files\image001.png](Aspose.Words.b5374c43-4222-45f9-86b9-040c3e64467a.001.png "image001")|
| :- |
\+ Câu lệnh khởi tạo: 

=> R(config)# access-list n [permit/deny] protocol  Source.IP Wildcard  [eq | lt | gt  Source Port]  Des.IP Wildcard [eq | lt | gt  Des.Port] 

\- eq: equal  (bằng)

\- lt: less than (ít hơn)

\- gt: greater than (nhiều hơn)

\- n chạy từ 100 tới 199

\+ Gán vào cổng theo chiều nào:

=> R1(config)# int s0/1/0

=> R1(config-if)# ip access-group n [in, out]

\+ Protocol:

|Application|Protocol|D.Port|
| :- | :- | :- |
|http|TCP|80|
|https|TCP|443|
|telnet|TCP|23|
|SSH|TCP|22|
|FTP|TCP |20, 21|
|TFTP|UDP|69|
|SMTP|TCP|25|
|POP3|TCP|110|
|ping |ICPM|không port (vì lớp internet)|
\+ Ta có thể áp được trên 4 cổng là: R1 (f0/0, s0/1/0), R2 (S0/2/0, F0/1). Nên đặt ở cổng gần nhất thì sẽ không phải mất quảng đường chạy và chiếm băng thông

**+ Ví dụ1:** Viết một Access list cấm toàn bộ mạng 192.168.1.0/24 truy cập tới Server 192.168.20.6/24 theo giao thức Web:

=> R1(config)#access-list 100  deny tcp  192.168.1.0  0.0.0.255  192.168.20.6  0.0.0.0  eq 80

=> R1(config)#access-list 100  permit ip any any   (những gì không chặn sẽ cho đi qua)

=> Gán vào cổng theo chiều In:

=> R1(config)# int f0/0

=> R1(config-if)# ip access-group n in  (chiều in vì các máy mạng 192.168.1.0 sẽ đi vào Router cổng F0/0, chiều Out S0/1/0)

**+ Ví dụ 2:** Viết Access list cấm mạng 192.168.1.0/24 và 192.168.2.0/24 truy cập tới Server 192.168.20.6/24 theo giao thức Web, TFTP:

=> R1(config)#access-list 100  deny tcp  192.168.1.0  0.0.0.255  192.168.20.6  0.0.0.0  eq 80

=> R1(config)#access-list 100  deny udp 192.168.2.0  0.0.0.255  192.168.20.6  0.0.0.0  eq 69

=> R1(config)#access-list 100  permit ip any any   (những gì không chặn sẽ cho đi qua)

=> Gán vào cổng theo chiều Out:

=> R1(config)# int s0/1/0

=> R1(config-if)# ip access-group n out  (chiều in vì các máy mạng 192.168.1.0 sẽ đi vào Router cổng F0/0, chiều Out S0/1/0)

\+ Cách viết ngắn gọn: 

\- Viết đầy đủ: 

=> R1(config)#access-list 100  deny tcp  192.168.1.0  0.0.0.255  192.168.20.6  0.0.0.0  eq 80

\- Viết ngắn gọn:

=> R1(config)#access-list 100  deny tcp  192.168.1.0  0.0.0.255  host 192.168.20.6  eq 80

\- Viết chặn Ping:

=> R1(config)# access-list 100 deny ICMP  192.168.1.0 0.0.0.255 host 192.168.20.6

**+ Ví dụ 3:** Cấm toàn bộ mạng 192.168.1.0 telnet tới R2 (có thể tới mọi router nhưng trừ R2).

=> R2(config)# access-list 2  deny 192.168.1.0  0.0.0.255

=> R2(config)# access-list 2  permit  any

=> R2(config)# line vty 0  4

=> R2(config-line)#access-class 2 in

**3. Named ACL:**

\+ Cú pháp khai báo:

=> R(config)# ip access-list [Standard | Extanded] tên ACL

=> R(config-std-name)# [sequence] permit hoặc deny (....)   (đoạn sau giống như bình thường)

\+ Đặt vào cổng:

=> R(config)# int s0/1/0

=> R(config-ip)# ip access-group tên ACL [int | out]

\+ Không khai báo số Access list nó vẫn tự động tạo ra giữa dòng trên và dòng dưới là tăng lên 10 đơn vị. 

**4. Câu lệnh kiểm tra:**

\+ R# show access-list

\+ R# Show ip interface f0/1  (để kiểm tra cổng nào có đặt Access list)

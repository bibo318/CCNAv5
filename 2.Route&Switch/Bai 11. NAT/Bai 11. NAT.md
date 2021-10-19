Giới thiệu về giao thức NAT

**I. Nội dung chính:**

\1. Giới thiệu về NAT

\2. Cấu hình NAT Router

**II. Nội dung chi tiết:**

**1. Giới thiệu về NAT & cấu hình NAT Router (Network Address Translate):** 

**a. Giới thiệu về NAT:** 

\+ Phải NAT ra ngoài để cho phép bên trong truy cập internet. 

|![C:\D06B1665\A19EC1F0-8A53-41FF-BEDE-C4CC4D9FE4D2\_files\image002.png](Aspose.Words.d4e22bb7-95b3-475c-9a9f-5b0c77b7d300.001.png "image002")|
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

|![C:\D06B1665\A19EC1F0-8A53-41FF-BEDE-C4CC4D9FE4D2\_files\image003.png](Aspose.Words.d4e22bb7-95b3-475c-9a9f-5b0c77b7d300.002.png "image003")|
| :- |
|Inside Local |Mọi địa chỉ của mình thì gọi là Inside Local|
|Inside Global|Mọi địa chỉ của mình nhưng do nhà cung cấp dịch vụ cấp cho gọi là Inside Global|
|Outside Global|Địa chỉ vừa bên ngoài và của người ta thì gọi là Outside Global|
|Local|Bên trong người dùng gọi là Local|
|Global|Nhà cung cấp dịch vụ gọi là Global|
**2. Cấu hình NAT Router: khảo sát các loại NAT (có 3 loại NAT):**

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

\+ Lệnh khởi tạo:

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

**d. Chú ý:** để hệ thống bên trong ra ngoài được Internet ta phải dùng lệnh Default Route

=> R1(config)# ip route 0.0.0.0 0.0.0.0 s0/1/0

**e. Câu lệnh kiểm tra:** trên Router cấu hình NAT: 

\+ R# show ip nat translations

\+ R#clear ip nat translations \*     (\* là xóa tất cả bảng NAT)

\+ R#debug ip nat 

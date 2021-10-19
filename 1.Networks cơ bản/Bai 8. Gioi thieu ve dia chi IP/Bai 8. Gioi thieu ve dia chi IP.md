**Giới thiệu về địa chỉ IP**

**I. Nội dung chính**

\1. Giới thiệu về địa chỉ IP

\2. Giới thiệu về địa chỉ IPv4

\3. Giới thiệu về địa chỉ IPv6

**II. Nội dung chi tiết**

**1. Giới thiệu về địa chỉ IP**

\- Địa chỉ IP được dùng để các máy truyền thông liên mạng.

\- Địa chỉ IP được phát triển qua nhiều phiên bản, tuy nhiên có những phiên bản chỉ dùng để thử nghiệm. Hai phiên bản được ứng dụng trong thực tế là IPv4 (IP phiên bản 4) sử dụng 32 bit dữ liệu và IPv6 (IP phiên bản 6) sử dụng 128 bit dữ liệu.

**2. Giới thiệu về địa chỉ IPv4**

**a. Địa chỉ IPv4 có định dạng như thế nào?**

\- Địa chỉ IPv4 thường được viết theo dạng gồm bốn nhóm số thập phân, ngăn cách nhau bằng dấu chấm. Do 32 bit chia đều cho bốn nhóm số, nên mỗi nhóm sẽ gồm tám bit dữ liệu, thường gọi là một oc-tet, nghĩa là bộ 8-bit nhị phân. Với số bit này, giá trị của mỗi oc-tet sẽ gồm 2^8 = 256 giá trị nằm trong khoảng từ 0 (tám bit toàn 0) đến 255 (tám bit toàn 1). 

\- Ví dụ: 203.162.4.190 hay 192.168.1.2

**b. Địa chỉ IP phân làm bao nhiêu lớp?**

\- Người ta phân địa chỉ IP ra làm 5 lớp (class):

\+ Lớp A: gồm các địa chỉ IP có oc-tet đầu tiên mang giá trị nằm trong khoảng từ 1-126

\+ Lớp B: gồm các địa chỉ IP có oc-tet đầu tiên mang giá trị nằm trong khoảng từ 128-191

\+ Lớp C: gồm các địa chỉ IP có oc-tet đầu tiên mang giá trị nằm trong khoảng từ 192-223

\+ Lớp D: gồm các địa chỉ IP có oc-tet đầu tiên mang giá trị nằm trong khoảng từ 224-239

\+ Lớp E: gồm các địa chỉ IP có oc-tet đầu tiên mang giá trị nằm trong khoảng từ 240-255

\- Trong thực tế, chỉ có các địa chỉ lớp A,B,C là được dùng để cài đặt cho các nút mạng, địa chỉ lớp D được dùng trong một vài ứng dụng dạng truyền thông đa phương tiện, như chuyển tải luồng video trong mạng. Riêng lớp E vẫn còn nằm trong phòng thí nghiệm và dự phòng! 

**c. Tại sao cần có Subnet mask?**

\- Mỗi địa chỉ IP đều đi kèm với thành phần gọi là Subnet mask. Vì giao thức TCP/IP quy định hai địa chỉ IP muốn làm việc trực tiếp với nhau thì phải nằm chung một mạng, hay còn gọi là có chung một Network ID. Subnet mask là một tập hợp gồm 32 bit tương tự địa chỉ IP, nhưng có đặc điểm là phân làm hai vùng, vùng bên trái toàn các bit 1 gọi là NetID, còn vùng bên phải toàn các bit 0 gọi là HostID.

\- Như vậy phần địa chỉ IP nằm tương ứng với vùng các bit 1 của Subnet mask được gọi là vùng Network của địa chỉ đó. Có ba Subnet mask chuẩn là lớp A: 255.0.0.0, lớp B: 255.255.0.0 và lớp C: 255.255.255.0

![](http://echip.vietnamnetjsc.vn/2013/04/06/07/45/Network00402.png "Network00402")

\- Ví dụ, một địa chỉ **192.168.1.2**, là địa chỉ lớp C nên sẽ có subnet mask chuẩn là 255.255.255.0. Ta thấy Subnet mask này tạo một ranh giới giữa các bit 1 và các bit 0 tại vị trí giữa bit 24 và bit 25, tức là giữa oc-tet 3 và oc-tet 4, do đó ba oc-tet đầu của địa chỉ **192.168.1**.2 sẽ là phần Network ID của nó. Nói cách khác **192.168.1.0** là NetID của địa chỉ 192.168.1.2.

|Địa chỉ IP|**192**|**168**|**1**|2|
| - | - | - | - | - |
|Subnet mask|**255**|**255**|**255**|0|
|Subnet mask|**11111111**|**11111111**|**11111111**|00000000|
|Network ID|192|168|1|0|
\- Một ví dụ khác, địa chỉ **172.16.4.2** là địa chỉ lớp B nên sẽ có subnet mask chuẩn là 255.255.0.0. Ta thấy Subnet mask này tạo một ranh giới giữa các bit 1 và các bit 0 tại vị trí giữa bit 16 và bit 17, tức là giữa oc-tet 2 và oc-tet 3, do đó hai oc-tet đầu của địa chỉ **172.16.**4.2 sẽ là phần Network ID của nó. Nói cách khác **172.16.0.0** là NetID của địa chỉ 172.16.4.2.

|Địa chỉ IP|**172**|**16**|4|2|
| - | - | - | - | - |
|Subnet mask|**255**|**255**|255|0|
|Subnet mask|**11111111**|**11111111**|11111111|00000000|
|Network ID|172|16|0|0|
**d. Khi nào thì cần dùng đến Default Gateway?**

\- Giao thức TCP/IP cũng quy định rằng hai địa chỉ IP có cùng NetID thì có thể gửi thông tin trực tiếp cho nhau. Ví dụ như 192.168.1.2 và 192.168.1.3 có cùng NetID là 192.168.1.0 nên gửi thông tin cho nhau một cách đơn giản, vì trong cùng một mạng. 

\- Trường hợp hai địa chỉ IP có NetID khác nhau, ví dụ như **192.168.1.2** có NetID là 192.168.1.0, còn 172.16.4.2 có NetID là **172.16.0.0**, muốn gửi thông tin cho nhau thì phải đi xuyên qua thiết bị Router, bằng cách gửi ra một cổng thoát mặt định, Default Gateway là địa chỉ IP của Router đó. 

\- Trong mạng máy tính gia đình, các địa chỉ máy con thường là 192.168.1.2, 192.168.1.3, 192.168.1.4 ..., khi muốn gửi nhận thông tin ra ngoài Internet, là các địa chỉ IP bất kỳ nào đó, chắc chắn có NetID khác với 192.168.1.0, thì phải gửi ra địa chỉ Default Gateway là 192.168.1.1. Địa chỉ IP 192.168.1.1 này phải được cài đặt sẳn trên Router ADSL của gia đình. Điều này cũng có nghĩa rằng một máy tính trong gia đình muốn kết nối ra Internet thì phải gửi thông tin ra Router ADSL, và thiết bị này sẽ định hướng lại gói tin đi đến nơi cần đến.

**e. IP tĩnh hay IP động?**

\- Một máy tính hay thiết bị mạng có thể được cài đặt địa chỉ IP bằng hai cách: tĩnh và động. Nếu người dùng cài đặt địa chỉ IP bằng cách gõ vào một giá trị xác định cho máy tính, ta gọi đó là cách dùng IP tĩnh. Nếu người dùng cho phép máy tính nhận địa chỉ IP từ một máy chủ DHCP chuyên phân phối IP, ta gọi đó là cách dùng IP động. Cách dùng IP tĩnh tuy không cần phải xây dựng một máy chủ DHCP, nhưng chỉ dùng được khi số lượng máy tính ít. Cách dùng IP động thì địa chỉ IP của máy tính có thể bị thay đổi bất kỳ lúc nào, nên việc quản lý sẽ phức tạp hơn.

**f. Cài đặt địa chỉ IP như thế nào?**

\- Trong Windows XP, bạn cài đặt địa chỉ IP bằng cách dùng menu *Start - Control Panel - Network Connections.* Trong Windows Vista trở lên, thì menu tương ứng là *Start - Control Panel -Network and Sharing Center – Manage Network Connections*. 

\- Sau đó bạn bấm phải chuột trên kết nối mạng cần đổi địa chỉ IP, rồi chọn *Properties*. Trong cửa sổ vừa mở ra, bạn bấm chọn mục *Internet Protocol Version 4 (TCP/IPv4)* rồi bấm vào nút *Properties* ngay phía dưới. Nếu muốn máy tính nhận địa chỉ IP động, bạn bấm vào mục *Obtain an IP address automatically*. Nếu muốn nhập địa chỉ IP tĩnh, bạn chọn mục *Use the following IP address* rồi gõ vào ba giá trị tương ứng là địa chỉ IP, *Subnet mask, và Default gateway.*

![](http://echip.vietnamnetjsc.vn/2013/04/06/07/45/Network00403.png "Network00403")

**3. Giới thiệu về địa chỉ IPv6** (đây là phần nâng cao nên tham khảo ở tài liệu chuẩn của CCNAv5 trong phần IPv6)

\- Địa chỉ IPv6 (Internet protocol version 6) là thế hệ địa chỉ Internet phiên bản mới được thiết kế để thay thế cho phiên bản địa chỉ IPv4 trong hoạt động Internet. Địa chỉ IPv4 có chiều dài 32 bít, biểu diễn dưới dạng các cụm số thập phân phân cách bởi dấu chấm, ví dụ 203.119.9.0. IPv4 là phiên bản địa chỉ Internet đầu tiên, đồng hành với việc phát triển như vũ bão của hoạt động Internet trong hơn hai thập kỷ vừa qua. Với 32 bit chiều dài, không gian IPv4 gồm khoảng 4 tỉ địa chỉ cho hoạt động mạng toàn cầu.- Do sự phát triển như vũ bão của mạng và dịch vụ Internet, nguồn IPv4 dần cạn kiệt, đồng thời bộc lộ các hạn chế đối với việc phát triển các loại hình dịch vụ hiện đại trên Internet. Phiên bản địa chỉ Internet mới IPv6 được thiết kế để thay thế cho phiên bản IPv4, với hai mục đích cơ bản:

\+ Thay thế cho nguồn IPv4 cạn kiệt để tiếp nối hoạt động Internet.   

\+ Khắc phục các nhược điểm trong thiết kế của địa chỉ IPv4.

\- Địa chỉ IPv6 có chiều dài 128 bít, biểu diễn dưới dạng các cụm số hexa phân cách bởi dấu ::, ví dụ 2001:0DC8::1005:2F43:0BCD:FFFF. Với 128 bít chiều dài, không gian địa chỉ IPv6 gồm 2^128 địa chỉ, cung cấp một lượng địa chỉ khổng lồ cho hoạt động Internet.- IPv6 được thiết kế với những tham vọng và mục tiêu như sau:

\+ Không gian địa chỉ lớn hơn và dễ dàng quản lý không gian địa chỉ.

\+ Khôi phục lại nguyên lý kết nối đầu cuối-đầu cuối của Internet và loại bỏ hoàn toàn công nghệ NAT

\+ Quản trị TCP/IP dễ dàng hơn: DHCP được sử dụng trong IPv4 nhằm giảm cấu hình thủ công TCP/IP cho host. IPv6 được thiết kế với khả năng tự động cấu hình mà không cần sử dụng máy chủ DHCP, hỗ trợ hơn nữa trong việc giảm cấu hình thủ công.

\+ Cấu trúc định tuyến tốt hơn: Định tuyến IPv6 được thiết kế hoàn toàn phân cấp.

\+ Hỗ trợ tốt hơn Multicast: Multicast là một tùy chọn của địa chỉ IPv4, tuy nhiên khả năng hỗ trợ và tính phổ dụng chưa cao.

\+ Hỗ trợ bảo mật tốt hơn: IPv4 được thiết kế tại thời điểm chỉ có các mạng nhỏ, biết rõ nhau kết nối với nhau. Do vậy bảo mật chưa phải là một vấn đề được quan tâm. Song hiện nay, bảo mật mạng internet trở thành một vấn đề rất lớn, là mối quan tâm hàng đầu.

\+ Hỗ trợ tốt hơn cho di động: Thời điểm IPv4 được thiết kế, chưa tồn tại khái niệm về thiết bị IP di động. Trong thế hệ mạng mới, dạng thiết bị này ngày càng phát triển, đòi hỏi cấu trúc giao thức Internet có sự hỗ trợ tốt hơn.

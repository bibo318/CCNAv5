**Giới thiệu về tầng Network Access**

**I. Nội dung chính**

**A. Giới thiệu về tầng Physical**

\1. Giới thiệu về tầng vật lý

\2. Chức năng của tầng vật lý

\3. Hạ tầng phát tín hiệu

\4. Thiết bị phần cứng

**B. Giới thiệu về tầng Data Link**

\1. Nhiệm vụ của tầng Data Link

\2. Giao thức của tầng Data Link (LLC, MAC)

\3. Các thiết bị hoạt động trong tầng Data Link

\4. Điều khiển truy cập đường truyền

\5. Đặc điểm của Frame

**II. Nội dung chi tiết**

**- Tầng Network Access trong TCP/IP bao gồm 2 tầng Physical và Data link trong mô hình OSI**

**A. Giới thiệu về tầng Physical**

**1. Giới thiệu về tầng vật lý**

\- Tầng vật lý (physical layer - còn có thể gọi là tầng thiết bị) là tầng thứ nhất trong bảy tầng mô hình OSI. Tầng này chịu trách nhiệm truyền tín hiệu, ngoài ra còn nhận dữ liệu từ tầng Data link đưa xuống và chuyển ngược lên cho Data link.

\- Tầng này là phần cứng (hardware) của mạng truyền thông. Hệ thống dây nối cụ thể, hoặc sự liên kết viễn thông điện từ. 

\- Tầng này còn xử lý truyền bằng tín hiệu sóng, ánh sáng, khống chế xung đột (collision control), và những chức năng ở hạ tầng thấp nhất.

\- Tầng vật lý là hạ tầng cơ sở của mạng truyền thông, cung cấp phương tiện truyền tín hiệu thô sơ ở dạng bit. Hình dáng của các nút cắm điện (electrical connector), tần số để phát sóng là bao nhiêu.

**2. Chức năng của tầng vật lý**

\- Chức năng và dịch vụ chính mà tầng vật lý giải quyết là:

\+ Thiết lập và ngắt mạch một liên kết viễn thông trên một phương tiện truyền thông;

\+ Tham gia vào một tiến trình trong đó tài nguyên được nhiều người sử dụng cùng một lúc, chẳng hạn phân giải sự tranh chấp (contention) và khống chế luồng (flow control);

\+ Biến đổi thể dạng của dữ liệu số (digital data) trong thiết bị của người dùng đồng bộ với tín hiệu được truyền qua đường truyền thông (Communication channel).

**3. Hạ tầng phát tín hiệu**

\- Trong một mạng cục bộ (local area network) viết tắt là LAN hoặc trong một mạng đô thị (metropolitan area network) viết tắt là MAN dùng kiến trúc của kết nối các hệ thống mở (open systems interconnection) (OSI), hạ tầng phát tín hiệu là một phần của tầng vật lý, và tầng này:

\+ Giao diện với hạ tầng khống chế tiếp cận phương tiện (medium access control sublayer)

\+ Thi hành việc mã hóa ký tự (character encoding), truyền thông (transmission), thu nhận tín hiệu, và giải mã (decoding)

\+ Có thể thi hành thêm chức năng cách ly.

**4. Thiết bị phần cứng**

\- Bộ lặp (repeater)

\- Switch, Hub, Access Point

\- Modem

\- Card mạng

\- Dây truyền tín hiệu

Chú ý: Tầng vật lý Liên quan đến sự truyền thông luồng dữ liệu bit không có kết cấu cụ thể, trên tuyến truyền thông. Chịu trách nhiệm về cơ lý, điện lý, và các tính năng quy trình, hòng thiết lập, giữ gìn và ngắt mạch tuyến truyền thông.

**B. Giới thiệu về tầng Data Link**

**1. Nhiệm vụ của tầng Data Link**

\+ Như chúng ta biết Data link nằm trong tầng 2 của mô hình OSI và nó là tầng con của Network Access trong TCP/IP.

\+ Nhiệm vụ đầu tiên là đóng gói các Packet thành Frame phù hợp với công nghệ đường truyền. 

=> Data link sẽ kiên kết dữ liệu với tầng trên. 

=> Điều khiển Frame được đặt vào đường truyền và lấy ra từ đường truyền, bằng việc sử dụng các kỹ thuật điều khiển truy cập đường truyền và phát hiện lỗi.

**2. Giao thức của tầng Data Link**

\+ Để thực hiện được nhiệm vụ đó thì tầng Data link dùng 2 giao thức là LLC (logical link control) và MAC (Media Access Control ) được nằm trong bộ tiêu chuẩn Ethernet. 

=> Trong đó LLC dùng để liên kết dữ liệu với bên trên đồng thời bắt đầu xây dựng frame và chỉ định giao thức hoạt động ở tầng mạng (IP, IPX, Apple talk) 

=> Giao thức MAC dùng để hoàn thiện xây dựng Frame bằng việc thêm vào các địa chỉ, mã bắt đầu và mã kết thúc của một Frame (MAC này khác địa chỉ MAC)

**3. Các thiết bị hoạt động**

\+ Switch là thiết bị chủ yếu là tầng này vì nó có chức năng chuyển mạch, cụ thể là chuyển các Frame.

\+  Switch hoạt động trên 7 tầng nhưng chủ yếu hoạt động ở tầng Data link theo chuẩn Ethernet.

**4. Điều khiển truy cập đường truyền**

\+ Trong giao thức MAC có 2 giao thức hỗ trợ: 

=> CSMA/CD: là công nghệ sử dụng sóng Mang (mang trong từ mang vác) phát hiện xung đột. Các thiết bị khi muốn truyền phải lắng nghe đường truyền. Nếu thấy đường truyền rỗi mới được truyền. Nếu 2 thiết bị cùng lắng nghe, cùng thấy rỗi và cùng truyền sẽ xẩy ra xung đột, khi đó có một tín hiệu JAM được gửi đến tất cả các thiết bị trên đường truyền, Các thiết bị này sẽ đặt một thời gian ngẫu nhiên trước khi quay lại lắng nghe đường truyền

=> CSMA/CA: là công nghệ sử dụng sóng Mang tránh xung đột. Cũng giống như công nghệ trên nhưng trước khi truyền mỗi thiết bị đều báo cho toàn mạng là nó sẽ truyền. Nếu 2 thiết bị cùng muốn truyền thì phải lắng nghe lại trong một khoảng thời gian ngẫu nhiên. Với công nghệ này đường truyền sẽ không bao giờ xẩy ra xung đột. Nhưng độ trễ cao. Nên chủ yếu được truyền trong những đường truyền có tốc độ thấp.

\+ Mỗi cổng của Switch sẽ được gọi một Colision domain

\+ Trong môi trường không chia sẽ là môi trường Point to Point thì sử dụng 2 công nghệ là:

=> Half-duplex là bộ đàm chỉ một chiều

=> Full-duplex là 2 chiều vừa truyền vừa nhận

**5. Đặc điểm của Frame**

|![C:\C5514F05\3EA976D0-7FD8-4857-8961-01E8C9EA3A27\_files\image001.png](Aspose.Words.b5e7f2a2-d1db-4c45-a786-3b5e6322490d.001.png "image001")|
| :- |
\+ Header và trailer là thông tin điều khiển. Thông qua Header và trailer thì nó xác định được: 

=> Thông qua Header và trailer thì nó xác định được các nút giao tiếp.

=> Khi nào truyền thông bắt đầu và khi nào truyền thông kết thúc. 

=> Lỗi xẩy ra trong khi truyền

=> Xác định các trạm trung gian tiếp theo phải đi qua (thiết bị nào tiếp theo sẽ đi qua)

\+ Các thành phần chi tiết trong Frame:

=> FCS (Frame check sequence): dùng mã băm để kiểm tra toàn vẹn

|![C:\C5514F05\3EA976D0-7FD8-4857-8961-01E8C9EA3A27\_files\image002.png](Aspose.Words.b5e7f2a2-d1db-4c45-a786-3b5e6322490d.002.png "image002")|
| :- |


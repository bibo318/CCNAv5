**Giới thiệu về công nghệ Ethernet**

**I. Nội dung chính**

\1. Giới thiệu về công nghệ Ethernet

\2. Các công nghệ và giao thức của Ethernet

\3. Giao thức ARP là gì?

\4. Giao thức RARP là gì?

**II. Nội dung chi tiết**

**1. Giới thiệu về công nghệ Ethernet**

\- Ethernet là công nghệ dành cho mạng LAN.  

\- Ethernet định nghĩa một loạt các chuẩn nối dây và phát tín hiệu cho tầng vật lý. Sử dụng giao thức MAC để điều khiển truy nhập dữ liệu vào đường truyền và lấy dữ liệu từ đường truyền chuyển lên bên trên. 

\- Ethernet đã được chuẩn hóa thành IEEE 802.3. Cấu trúc mạng hình sao, hình thức nối dây cáp xoắn (twisted pair) của Ethernet đã trở thành công nghệ LAN được sử dụng rộng rãi nhất từ thập kỷ 1990 cho tới nay, nó đã thay thế các chuẩn LAN cạnh tranh khác như Ethernet cáp đồng trục (coaxial cable), token ring, FDDI (Fiber distributed data interface), và ARCNET. Trong những năm gần đây, Wi-Fi, dạng LAN không dây đã được chuẩn hóa bởi IEEE 802.11, đã được sử dụng bên cạnh hoặc thay thế cho Ethernet trong nhiều cấu hình mạng.

**2. Các công nghệ và giao thức của Ethernet**

**a. Công nghệ và giao thức** 

\- Ethernet là chuẩn công nghệ tương ứng với 2 tầng Data link và Physical trong mô hình OSI.

\- Công nghệ chính của mạng dây là IEEE 802.2 và IEEE 802.3.

\- Ethernet hỗ trợ băng thông truyền dữ liệu là 10, 100, 1000, 10,000, 40,000 và 100,000 Mbps (100 Gbps)

\- Hai giao thức chính trong tầng Data link là Logical link control (LLC) và Media Access Control (MAC). Giao thức LLC dùng để giao tiếp với Layer 3, chuyển dữ liệu từ Layer 3 xuống cho MAC và lấy dữ liệu từ MAC chuyển lên. Giao thức MAC dùng để điều khiển dữ liệu truy nhập vào đường truyền và lấy dữ liệu từ đường truyền lên. Trong giao thức MAC có 2 tính năng: chuyển đổi dữ liệu thành Frame và điều khiển truy nhập đường truyền. 

![](Aspose.Words.9755ed60-11d4-44e9-9bd3-520985278300.001.png)

**b. Giao thức MAC sử dụng** **Cơ chế CSMA/CD** 

\- Đây là cơ chế đa truy nhập cảm biến sóng mang dò được truy cập.** Khi xảy ra đụng độ giữa các tín hiệu trên đường truyền, mặc dù trước đó các máy truyền tín hiệu đều đã thăm dò xem đường truyền có rảnh không thì lúc đó các máy truyền sẽ đẩy các mẩu tín hiệu JAM , điều này sẽ làm cho xung đột trở nên trầm trọng hơn, khi đó tất cả các máy đều biết là có xảy ra xung đột. Lúc này mỗi máy sẽ tự khởi tạo cơ chế timer, đảm bảo rằng bộ timer của mỗi máy là khác nhau, sau đó bộ timer của các máy truyền tín hiệu sẽ giảm dần về 0, rồi sẽ xúc tiến hoạt động trở lại. Như vậy các bộ timer là hoàn toàn khác nhau và không xảy ra vấn đề đụng độ trên đường truyền ( thuật toán được sử dụng trong cơ chế này là backoff algorithm ).

**c. Cấu trúc gói tin truyền trong LAN của Ethernet**

![](Aspose.Words.9755ed60-11d4-44e9-9bd3-520985278300.002.png)

\- Ethernet II là chuẩn định dạng Frame sử dụng trong TCP/IP networks. 

**d. Địa chỉ MAC**

\- Địa chỉ MAC là loại địa chỉ vật lí của môi trường layer 2 được gán trên card mạng của máy tính, và là địa chỉ duy nhất  trên thế giới , còn có tên gọi khác là địa chỉ phẳng.

\- Địa chỉ MAC là 1 dãy nhị phân gồm 48bits được chia thành 2 phần: 24 bits trước và 24 bits sau. Trong 24 bits trước thì có 2 bits đầu tiên dùng để chỉ thị những tính năng đặc biệt của địa chỉ, còn lại là  22 bits OUI định danh cho nhà sản suất, phần 24 bits còn lại là Vendor Assigned định danh cho từng thiết bị do nhà sản suất đó sản xuất ra.

\- Đinh dạng của địa  chỉ MAC được thể hiện dưới dạng số hexa. Vd: 00:00:0c:43:2e:08 ( mỗi 1 số hexa được thể hiện bằng 4 bits nhị phân ).

|![](Aspose.Words.9755ed60-11d4-44e9-9bd3-520985278300.003.png)|![](Aspose.Words.9755ed60-11d4-44e9-9bd3-520985278300.004.png)|
| :- | :- |
**3. Giao thức ARP là gì?**

\- Khi một thiết bị mạng muốn biết địa chỉ MAC của một thiết bị mạng nào đó mà nó đã biết địa chỉ ở tầng network (IP, IPX…) nó sẽ gửi một ARP request bao gồm địa chỉ MAC address của nó và địa chỉ IP của thiết bị mà nó cần biết MAC address trên toàn bộ một miền broadcast. Mỗi một thiết bị nhận được request này sẽ so sánh địa chỉ IP trong request với địa chỉ tầng network của mình. Nếu trùng địa chỉ thì thiết bị đó phải gửi ngược lại cho thiết bị gửi ARP request một gói tin (trong đó có chứa địa chỉ MAC của mình). 

\- Trong một hệ thống mạng đơn giản, ví dụ như PC A muốn gửi gói tin đến PC B và nó chỉ biết được địa chỉ IP của PC B. Khi đó PC A sẽ phải gửi một ARP broadcast cho toàn mạng để hỏi xem "địa chỉ MAC của PC có địa chỉ IP này là gì ?"  Khi PC B nhận được broadcast này, nó sẽ so sánh địa chỉ IP trong gói tin này với địa chỉ IP của nó. Nhận thấy địa chỉ đó là địa chỉ của mình, PC B sẽ gửi lại một gói tin cho PC A trong đó có chứa địa chỉ MAC của B. Sau đó PC A mới bắt đầu truyền gói tin cho B.

\- Tiến trình của ARP được mô tả như sau:

\+ Máy trạm yêu cầu: có IP, yêu cầu địa chỉ MAC.

\+ Máy trạm yêu cầu: tìm kiếm trong bảng ARP.

\+ Nếu tìm thấy sẽ trả lại địa chỉ MAC.

\+ Nếu không tìm thấy, tạo ARP Request  phát quảng bá tới các trạm khác.

\+ Tuỳ theo gói tin trả lời, ARP cập nhật vào bảng ARP.

**4. Giao thức RARP là gì?**

\- RARP là giao thức phân giải địa chỉ ngược, cho trước địa chỉ MAC, tìm địa chỉ IP tương ứng

\- RARP đòi hỏi một hoặc nhiều máy chủ lưu trữ để duy trì một cơ sở dữ liệu bản đồ của địa chỉ lớp liên kết đến các địa chỉ giao thức tương ứng. Media Access Control (MAC) địa chỉ cần thiết để được cấu hình riêng trên các máy chủ của quản trị viên. RARP được giới hạn chỉ phục vụ các địa chỉ IP.

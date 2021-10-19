Transport

**I. Nội dung chính:**

\1. Vai trò của tầng Transport

\2. Giới thiệu về giao thức TCP

\3. Giới thiệu về giao thức UDP

\4. Giới thiệu về Port

\5. Vai trò của TCP trong truyền thông tin cậy

\6. Điều khiển lưu lượng

**II: Nội dung chi tiết:**

**1. Vai trò của tầng Transport:** 

\+ Transport làm nhiệm vụ vận chuyển thông tin từ nguồn tới đích. Dữ liệu nhận từ tầng Application chuyển xuống thông qua các cổng dịch vụ, rồi đóng gói lại bằng giao thức TCP hoặc UDP để vận chuyển đi.

\+ Cho phép truyền đồng thời nhiều dịch vụ. 

=> Transport sử dụng cơ chế phân mảnh (Segmentation) và quản lý phân mảnh nên có thể truyền nhiều dịch vụ và tiết kiệm băng thông đường truyền, dễ truyền và sửa lỗi. Đồng thời khi truyền dữ liệu từ nguồn tới đích sẽ có kích thước khác nhau. Để dữ liệu chuẩn theo kích thước truyền thì sẽ phân đoạn thành nhiều mảnh. 

=> Bên máy A gửi dữ liệu sử dụng cơ chế phân mảnh thì bên máy B sẽ nhận dữ liệu theo đúng trật tự ban đầu bên gửi

\+ Hỗ trợ truyền thông tin cậy khi được yêu cầu: sử dụng cơ chế bắt tay 3 bước để xác nhận thông tin.

\+ Cho phép quản lý lỗi: thông qua giao thức TCP nó sẽ truy vết quá trình truyền thông từ nguồn tới đích. Đồng thời khi có lỗi xẩy ra nó sẽ yêu cầu truyền thông lại các mảnh bị hỏng. 

\+ Nhận diện các dịch vụ khác nhau: khi cho phép truyền nhiều ứng dụng sẽ gán cho các nhãn theo gói tin để biết đâu là DNS, Web, Mail.

=> Bước 1: Khi người dùng cùng lúc mở IE truy cập trang <http://www.google.com> và <http://ftp.aptech.com>. 

=> Bước 2: Dữ liệu xuống Transport sẽ được gán nhãn cho Web là A và cho FTP là B

=> Bước 3: Dữ liệu sẽ được phân mảnh thành: A1, A2, A3, A4 và B1, B2, B3

=> Bước 4: Khi khi dữ liệu được truyền sang máy nhận nó sẽ sắp xết đúng thứ tự A và B

**2. Giới thiệu về giao thức truyền thông tin cậy TCP:** (Transmission Control Protocol)

\+ Transport sử dụng giao thức TCP là truyền thông tin cậy.

\+ Dữ liệu được đóng gói theo TCP sẽ có các khuôn dạng thêm vào đầu các  Data từ Application xuống gọi là thông tin điều khiển Header. Header nặng 20bytes

=> Trong TCP số trường trong Header nhiều nên đọc sẽ lâu.

\+ Các trường trong Header của giao thức TCP:

|![C:\B1841625\29414B52-8D9E-4E32-9F7E-A306E8576FD0\_files\image001.png](Aspose.Words.93fb8841-4edb-4f32-b433-30b432124b07.001.png "image001")|
| :- |
**=>Source Port (16bit):** là Port tự sinh bên máy người dùng. Mở IE hoặc Firefox ta nhập một yêu cầu là truy cập  Google.com nó sẽ sinh ra một Port. Port này dùng để chuyển yêu cầu xuống Transport. Khi dữ liệu từ Server truyền lại nó sẽ  được Transport chuyển dữ liệu đúng lên Port này.

**=> Destination Port (16bit):** là Port đích. Đây là Port của dịch vụ. Web là 80 hoặc 443, FTP là 20, 21...

**=> Sequence number (32bit):** đánh số thứ tự của gói tin. Khi một yêu cầu từ IE gửi xuống là một gói tin. Các giói tin này sẽ được đánh nhãn. Khi phân mảnh và ráp mảnh nó sẽ dựa vào nhãn này để biết gói tin của dịch vụ nào.

**=> ACK (32bit):** dùng để báo rằng đã nhận được dữ liệu. Dữ liệu bên truyền gửi đi bị hỏng ACK cũng báo lại để bên gửi truyền lại dữ liệu. ACK sẽ chỉ ra byte mong đợi kế tiếp chứ không phải là byte nhận được cuối cùng. Trường ACK chỉ ra số byte chứ không phải chỉ ra Segment của TCP.

**=> Header Length (4bit):** độ dài của Header

**=> Reserved (6bit):** để dành chưa sử dụng tới

**=> Code bit (6 bit):** Cho ta biết nhiệm vụ của Segment hiện thời. Có 8 bít nhưng 2 bít đầu là để trống nên chỉ dụng 6 bít làm cờ. 

\- Cờ SYN và ACK bật lên sẽ chỉ ra một Segment có phải là Segment đầu tiên hay là thứ 2 trong một kết nối TCP.

==> Một Segment có cờ SYN bật lên sẽ là Segment đầu tiên trong một kết nối TCP

==> Một Segment có cả cờ SYN và ACK sẽ là Segment thứ 2 trong một kết nối.

==> Các cờ này sẽ cho phép các máy dễ nhận ra các yêu cầu kết nối mới

\- Cờ SYS bật lên để báo thiết lập phiên truyền.

\- Cờ RST bật lên để biết cần gửi lại những dữ liệu bị hỏng khi đường truyền bị ngắt đột ngột (dữ liệu truyền là tiếp theo)

\- Cờ FIN bật lên để biết kết thúc truyền dữ liệu.

**=> Window(16bit):** đây là kích thước cửa sổ trượt, được sử dụng để điều khiển lưu lượng truyền.

**=> Checksum (16bit)**: tính toán và kiểm tra sự toàn vẹn của Header và dữ liệu.

**3. Giới thiệu về giao thức UDP(User Datagram Protocol):** 

\+ Transport sử dụng giao thức UDP là truyền thông tốc độ cao.

\+ Dữ liệu được đóng gói theo UDP sẽ có các khuôn dạng thêm vào đầu các Data từ Application xuống gọi là thông tin điều khiển Header. Header nặng 8 bytes

=> Trong UDP số trường trong Header ít nên nó đọc rất nhanh.

\+ UDP không có các trường truyền thông tin cậy. 

|![C:\B1841625\29414B52-8D9E-4E32-9F7E-A306E8576FD0\_files\image002.png](Aspose.Words.93fb8841-4edb-4f32-b433-30b432124b07.002.png "image002")|
| :- |
=> **Source Port (16bit):** là Port tự sinh bên máy người dùng. Mở IE hoặc Firefox ta nhập một yêu cầu là truy cập  Google.com nó sẽ sinh ra một Port. Port này dùng để chuyển yêu cầu xuống Transport. Khi dữ liệu từ Server truyền lại nó sẽ  được Transport chuyển dữ liệu đúng lên Port này.

**=> Destination Port (16bit):** là Port đích. Đây là Port của dịch vụ. Web là 80 hoặc 443, FTP là 20, 21...

**=> Length (16bit):** độ dài của Header và dữ liệu

**=> Checksum (16):** tính toán và kiểm tra sự toàn vẹn của Header và dữ liệu.

**4. Giới thiệu về Port:**

\+ Để các phần mềm và các chương trình ứng dụng giao tiếp và truyền thông với nhau thì chúng dựa vào các Port. 

\+ Port 0-1023 là đặt theo Port chuẩn của quốc tế. 

\+ Từ 1024 tới 49151 là các dải cung cấp cho các dịch vụ sau này.

\+ Từ 49151 tới 65535 là Port tự sinh trên các máy Client khi người dùng gửi yêu cầu.

=> Port tự sinh vì trên một máy nếu mở 10 trang web khác nhau thì phải tự sinh Source Port nguồn để thông tin gửi về đúng với nó, còn nếu cùng port thì sẽ lộn ngay.

=> Cổng ngẫu nhiên sẽ giúp bảo mật hơn vì không ai biết mình đang sử dụng cổng nào sẽ tránh được tấn công.

\+ Khi có Port nó sẽ phân luồng dữ liệu tốt hơn.

\+ Port của giao thức TCP và UDP:

|![C:\B1841625\29414B52-8D9E-4E32-9F7E-A306E8576FD0\_files\image003.png](Aspose.Words.93fb8841-4edb-4f32-b433-30b432124b07.003.png "image003")|
| :- |
**5. Vai trò của TCP trong truyền thông tin cậy:** 

\+ Thành phần xác định độ tin cây của TCP là sử dụng Sequence number và ACK.

|![C:\B1841625\29414B52-8D9E-4E32-9F7E-A306E8576FD0\_files\image004.png](Aspose.Words.93fb8841-4edb-4f32-b433-30b432124b07.004.png "image004")|![C:\B1841625\29414B52-8D9E-4E32-9F7E-A306E8576FD0\_files\image005.png](Aspose.Words.93fb8841-4edb-4f32-b433-30b432124b07.005.png "image005")|
| :- | :- |
|**Quá trình bắt tay 3 bước, khởi tạo phía máy khách**|**Quá trình kết thúc bắt tay 3 bước, khởi tạo từ máy khách**|
|![C:\B1841625\29414B52-8D9E-4E32-9F7E-A306E8576FD0\_files\image006.png](Aspose.Words.93fb8841-4edb-4f32-b433-30b432124b07.006.png "image006")|![C:\B1841625\29414B52-8D9E-4E32-9F7E-A306E8576FD0\_files\image007.png](Aspose.Words.93fb8841-4edb-4f32-b433-30b432124b07.007.png "image007")|
**+ Quá trình bắt tay 3 bước:** xét quá trình truy cập Webserver

=> Bước 1: Dữ liệu yêu cầu đi từ tầng Application xuống sẽ được tầng Transport khởi tạo cổng nguồn là 45994, đánh số thứ tự của gói tinh này là 200 (trường Sequence đánh số 200). Giao thức TCP sẽ đóng thêm cổng đích là 80 vào gói tin. Đồng thời cờ SYN được bật. Cờ SYN bật lên để yêu cầu thiết lập phiên truyền.

=> Bước 2: Sau khi Server Web sẽ nhận dữ liệu và xử lý thì tầng Transport sẽ đóng cổng nguồn là 80 và cổng đích là 45994, số thứ tự gói tin Web Server gửi đi là 1540 ( trường Sequence đánh số 1540). ACK sẽ bằng số Sequence của Client gửi sang và tăng lên một để báo nhận thành công (ACK=201). Cờ SYN và ACK cùng bật để thông báo đây là phiên truyền thứ 2.

=> Bước 3: Client nhận được dữ liệu truyền về từ Server nó sẽ báo lại là nhận thành công. Lúc này cổng nguồn của phiên thiếp lập vẫn là 45994, cổng đích là 80. Số thứ tự gói tin được được trường Sequence đánh là 201 chính bằng số ACK của Server gửi về. Số ACK gửi đi là 1541, bằng số Sequence của Server gửi sang và tăng lên một để báo nhận thành công. 

**6. Điều khiển lưu lượng:** 

\+ Giao thức TCP sử dụng trường Window nằm trong trong Header để kiểm soát dòng lưu lượng. Máy nhận sẽ sử dụng trường Window khai báo kích thước cửa sổ nhận (tính bằng đơn vị byte).

\+ Giao thức TCP bên truyền sẽ sử dụng một cửa sổ trượt với kích thước của sổ trượt nhỏ hơn 2 giá trị:

=> Giá trị đầu tiên là giá trị của cửa sổ bên nhận gửi về

=> Giá trị thứ 2 là cửa số nghẽn (Congestion Window)

\+ Cơ chế hoạt động: Sau mỗi lần truyền thông thành công giá trị trường thứ 2 (Congestion Window) sẽ tăng gấp đôi (giá trị này là lượng dữ liệu gửi đi trước khi có một xác nhận gửi về). Nếu đường truyền có lỗi giá trị trường windows sẽ giảm đi một nữa. Cho tới khi không còn lỗi nữa và dựng lại ổn định tại đó. Quy định dữ liệu của Segment là 1500 bytes.

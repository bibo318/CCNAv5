﻿**Truyền thông qua mạng**

**I. Nội dung chính** 

\1. Nền tảng của truyền thông

\2. Các bước truyền thông qua mạng

\3. Cách thức làm việc của mạng LAN, WAN, Internet trong truyền thông

\4. Tìm hiểu về giao thức (Protocol) trong truyền thông.

\5. Mô hình OSI là gì? tại sao phải phân lớp?

\6. Địa chỉ mạng là gì?

**II. Nội dung chi tiết:** 

**1. Nền tảng của truyền thông:** để các máy tính và các thiết bị trong mạng truyền thông được với nhau thì hệ thống mạng phải có phần cứng và phần mềm. Từ phần cứng và phần mềm ta chia thành 4 thành phần: 

\+ Thiết bị đầu cuối: máy tính, laptop, Server, điện thoại…. Các thiết bị này đều phải cài đặt Hệ điều hành hoặc phần mềm.

\+ Đường truyền: dây, Switch, Router, Modem được kết nối lại với nhau. Để kết nối gần ta dùng dây cáp đồng, kết nối xa thì dùng dây cáp quang hoặc dùng sóng vệ tinh.

\+ Thông tin: nội dung website, thư điện tử, nội dung chat... Dữ liệu này này sẽ được chia thành các mảnh để đưa vào đường truyền gọi là Segment. Để trao đổi được thông tin thì phải có người gửi và người nhận. 

\+ Giao thức (rule): cho phép truy cập tới dịch vụ gì, được đi theo đường nào, dữ liệu được tải ra sao, giao thức nào được áp dụng là gì. Vd: truyền theo Web phải sử dụng theo port 80 hoặc 443.

**2. Các bước truyền thông qua mạng:** 

Xét trường hợp cụ thể là truy cập vào trang Google.

**=> Bước 1:** mở trình duyệt IE hoặc Firefox trên máy tính gõ : <http://google.com>. Do IE là phần mềm sử dụng giao thức http, https (port 80, 443). Bộ giao thức này nằm ở tầng Application. Ai muốn viết phần mềm hoặc lập trình web thì phải tuân thủ.

**=> Bước 2:**  yêu cầu được nhập vào là ký tự trên bàn phím, máy tính sẽ chuyển đổi ra tín hiệu nhị phân (bit 0, 1) để cho máy tính hiểu. Để chuyển đổi được thì máy tính có hẳn riêng một bộ phận làm phiên dịch là tầng Presentation.

**=> Bước 3:** Trước yêu cầu được truyền đi máy tính sẽ có một bộ phận đàm phán phiên để truyền gọi là Session. Session ở đây nó sẽ tạo ra một kết nối trực tiếp tới Server google, được Server google đồng ý nó mới truyền yêu cầu. Sau khi kết thúc phiên nó sẽ đóng kết nối.

**=> Bước 4:** Để yêu cầu đi được (yêu cầu là dữ liệu) thì phải có bộ phận đóng gói dữ liệu đó là tầng Transport. Transport sẽ nhận dữ liệu từ Port 80 của giao thức http đi từ tầng Application xuống rồi đóng thêm giao thức để truyền thông là TCP hay UDP để truyền. Giao thức TCP ở tầng Transport có nhiệm vụ băm nhỏ dữ liệu ra thành các Segment (data và header). Trong header có cổng nguồn và cổng đích. Các Segment sẽ chuyển xuống tầng Network để xử lý (dữ liệu từ tầng này trở lên là độc lập với đường truyền). 

**=> Bước 5:** Tầng Network sẽ sử dụng IPv4 và IPv6 nhưng chủ yếu là IPv4. Khi các Segment đưa xuống sẽ đóng vào gói Data lớn hơn. Trong này sẽ có IP nguồn và IP đích (địa chỉ máy gửi là máy mình và địa chỉ máy nhận là địa chỉ Server Google). Sau đó sẽ đưa xống bên dưới là tầng Data Link.

**=> Bước 6:** Data link đóng vào địa chỉ MAC ( MAC nguồn và MAC đích). MAC của máy PC1 và MAC cổng Gateway. Data link sẽ đóng vào đầu là Header và cuối là Trailer. Sau đó đưa xuống đường vật lí (physical).

**=> Bước 7:** Đường vật lí là tín hiệu điện 0,1 được gửi đi (tín hiệu điện này khác với tín hiệu điện dữ liệu)

**=> Bước 8:** Sau khi gửi ra Router thì nó sẽ nhận các tín hiệu và đóng gói rồi phân tích địa chỉ MAC. Router sẽ xem địa chỉ MAC đích là ai nếu đúng nó sẽ xác định để xử lý. Nếu đúng nó tách ra và đưa lên tầng Network để xác định địa chỉ IP của đích tới. Sau khi xác định xong sẽ đóng gói lại và chuyển ra cổng bên ngoài. Router sẽ sử dụng bảng định tuyến để gửi ra đúng cổng cần chuyển. Tương tự các thiết bị Router kế tiếp sẽ nhận và gửi đi sau đó gửi tới đích là Server Google.

**=> Bước 9:** Sau khi xử lý Server sẽ gửi lại dữ liệu yêu cầu vào đường truyền. 

=> Bước 10: Sau khi dữ liệu tới đích nó sẽ gửi lên cửa sổ IE và kết thúc quá trình truyền thông.

**3. Cách thức làm việc của mạng LAN, WAN, Internet trong truyền thông:** 

\+ Trong mạng LAN: Các PC, Switch, Router giao tiếp với nhau bằng địa chỉ MAC.

\+ Dữ liệu từ mạng LAN đi ra ngoài internet phải thông qua Modem hoặc Router.

\+ Từ Router ở công ty sẽ gửi tới router của nhà cung cấp dịch vụ. 

\+ Các nhà cung cấp dịch vụ sẽ liên kết Router lại với nhau để chuyển đi quốc tế.

\+ Trên Các Router có bảng định tuyến để định đúng đường đi. 

**4. Tìm hiểu về giao thức (Protocol) trong truyền thông:** 

\+ Giao thức dùng để định dạng cấu trúc của gói tin. Gói tin đi theo Web thì phải theo định dạng của Web, Mail định dạng theo Mail... Do đó trên tầng ứng dụng có thể dùng cùng lúc nhiều dịch vụ mà không sợ xung đột nhau.

\+ Cho phép truy cập tới đâu: thông qua giao thức chúng ta có thể điều hướng người dùng truy cập tới Server trong công ty hay truy cập ra Server bên ngoài internet. Truy cập tới dịch vụ này hay tới dịch vụ khác.

\+ Được tải những phần dữ liệu nào: trong hệ thống có nhiều phòng ban, dựa vào giao thức ta có thể phân quyền truy cập tài nguyên. Người dùng có thể copy dữ liệu trên phòng ban của mình hoặc cả phòng ban khác.

\+ Cho phép truyền hoặc tải bao nhiêu dữ liệu qua đường truyền: đường truyền là 100Mbps/s chúng ta có thể giới hạn tải xuống 20Mbps hoặc 50Mbps.

**5.  Tại sao phải phân lớp? Mô hình OSI là gì?** 

**a. Mô hình OSI là:** Open System Interconnection, tạm dịch là Mô hình tham chiếu kết nối các hệ thống mở, là một mô hình phân lớp nổi tiếng. Được phát thảo vào năm 1971 và hoàn thiện vào năm 1984. Mô hình này chia thành 7 lớp: Application, Presentation, Session, Transport, Network, Data link, Physical.

|![C:\F51D68C5\5DC8EB67-5A50-42BE-BC32-2B58CA69098E\_files\image001.png](Aspose.Words.4af1800a-9897-4707-8e06-0aefbe0be5d7.001.png "image001")|![C:\F51D68C5\5DC8EB67-5A50-42BE-BC32-2B58CA69098E\_files\image002.png](Aspose.Words.4af1800a-9897-4707-8e06-0aefbe0be5d7.002.png "image002")|![C:\F51D68C5\5DC8EB67-5A50-42BE-BC32-2B58CA69098E\_files\image003.jpg](Aspose.Words.4af1800a-9897-4707-8e06-0aefbe0be5d7.003.jpeg "image003")|
| :- | :- | :- |
**+ Application:** Tầng ứng dụng là tầng gần với người sử dụng nhất. Nó cung cấp phương tiện cho người dùng truy nhập các thông tin và dữ liệu trên mạng thông qua chương trình ứng dụng. Tầng này là giao diện chính để người dùng tương tác với chương trình ứng dụng. Một số ví dụ về các ứng dụng trong tầng này bao gồm: Web, Mail, FTP, Telnet...

**+ Presentation:** Tầng trình diễn nó thực hiện các tác vụ như chuyển đổi dữ liệu, mã hóa dữ liệu, nén dữ liệu. Chẳng hạn: chuyển đổi tệp văn bản sang mã ASCII hay ngược lại. Presentation sẽ chuyển đổi dữ liệu ra tín hiệu nhị phân (bit 0, 1) để cho máy tính hiểu rồi chuyển lại để người dùng xem được.

**+ Session:** Tầng phiên kiểm soát các (phiên) hội thoại giữa các máy tính. Tầng này thiết lập, quản lý và kết thúc các kết nối giữa trình ứng dụng trong mạng và trình ứng dụng ở xa. Mô hình OSI cho phép tầng này kết nối hoặc ngắt các phiên giao dịch và trách nhiệm kiểm tra và phục hồi phiên.

**+ Transport:** là tầng quản lý kết nối đầu cuối. Nó không quan tâm tới đường đi thế nào vì có các tầng Network, Data link, Physical làm nhiệm vụ. Ở đây nó chỉ quan tâm tới dữ liệu của người dùng truyền thông thế nào. Đảm bảo dữ liệu truyền an toàn. Tầng Transprot nó xem 2 máy sau khi thiết lập là làm việc trực tiếp với nhau kể cả khoảng cách xa như ở Việt Nam và Mỹ. Tầng này là nơi các thông điệp được chuyển sang thành các gói tin TCP hoặc UDP. Ở tầng Transport này địa chỉ được đánh là address ports, thông qua address ports để phân biệt được ứng dụng trao đổi.

**+ Network:** dùng để định danh địa chỉ nguồn và địa chỉ đích. Chọn ra đường đi tốt nhất tới đích dựa vào giao thức định tuyến. Chúng sử dụng địa chỉ IP để định địa chỉ. Network sẽ lấy dữ liệu từ tầng Data link để kiểm tra địa chỉ, nếu khi tách ra đúng địa chỉ của nó sẽ chuyển lên tầng bên trên để xử lý. Khi dữ liệu từ bên trên chuyển xuống nó sẽ đóng IP của máy mình và IP máy đích rồi chuyển xuống tầng Data link.

**+ Data link:** là lớp liên kết dữ liệu. Dùng để điều khiển việc đưa dữ liệu vào đường truyền và lấy dữ liệu từ đường truyền chuyển lên bên trên là tầng Network xử lý. Data link cung cấp tính năng dò lỗi dữ liệu khi truyền, đảm bảo dữ liệu truyền đến đích phải đủ. 

**+ Physical:** Chức năng là truyền một dòng bit qua đường truyền vật lý. Nó định nghĩa ra về đường truyền, tín hiệu truyền, thiết bị cần áp dụng. Giữa PC và Switch phải đấu nối thế nào, theo cáp đồng hay cáp quang, cự ly truyền là bao xa. Nói chung đường truyền vật lý liên quan tới cơ, điện, quang để đưa bit nhị phân đi tới đích.

**b. Tại sao phải phân lớp:** để truyền thông được chúng ta phải xây dựng một hệ thống mạng. Trong hệ thống mạng bao gôm thiết bị vật lý, đường truyền, dữ liệu và các giao thức. Một công ty không thể sản xuất và thiết kế được hết bấy nhiêu chức năng, nên người ta phải phân ra các lớp công việc để phát triển phù hợp.

\+ Các ưu điểm khi phân lớp:

=> Giảm tải độ phức tạp của hệ thống khi truyền dữ liệu. Khi phân lớp người ta không phải sản xuất từ trên xuống dưới mà chỉ cần làm một phần công việc. Sản phẩm sẽ tốt hơn, tương thích với nhiều thành phần của các dòng sản phẩm khác nhau. 

=> Trong mô hình OSI người ta phân ra thành các lớp chuẩn. Người sản xuất phải dựa vào chuẩn đó để xây dựng và phát triển. Do đó các lớp sẽ giao tiếp được với nhau. Từ đó tạo ra sự chuẩn hóa của các dòng sản phẩm

=> Do có sự chuẩn hóa về sản phẩm nên nó sẽ tương thích về công nghệ. Ngày này máy IBM có thể truyền tới máy HP

=> Thúc đẩy kỹ thuật module hóa: ai mạnh về lớp nào sẽ sản suất chuyên môn lớp đó. 

=> Thúc đẩy phát triển của công nghệ.

=> Người dùng dễ học hơn: không phải học hết cả 7 lớp một lúc mà học lần lượt đều được.

**6. Địa chỉ mạng là:** trong hệ thống mạng chúng ta có 2 loại địa chỉ là địa chỉ IP và địa chỉ MAC

\+ Địa chỉ IP(Internet Protocol): là chỉ của một máy tính khi tham gia vào mạng nhằm giúp cho các máy tính có thể chuyển thông tin cho nhau một cách chính xác, tránh thất lạc. Có thể coi địa chỉ IP trong mạng máy tính giống như địa chỉ nhà của bạn để nhân viên bưu điện có thể đưa thư đúng cho bạn chứ không phải một người nào khác.

=> Chú ý: địa chỉ IP khác với giao thức IP

\+ Địa chỉ MAC (Media Access Control): là địa chỉ vật lý của thiết bị. Mỗi thiết bị MAC là duy nhất. Cho phép các trạm cuối (terminal) hoặc các nút mạng liên lạc với nhau trong một mạng, điển hình là mạng LAN. 

=> Chú ý: địa chỉ MAC khác với giao thức MAC.

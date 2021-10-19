**Giới thiệu về Network Layer**

**I. Nội dung chính**

\1. Giới thiệu về tầng Network

\2. Giới thiệu về IPv4 header

\3. Giới thiệu về IPv6 header

**II. Nội dung chi tiết**

**1. Giới thiệu về tầng Network**

**a. giới thiệu**

\- Tầng Network là tầng thứ 3 từ dưới lên trong mô hình OSI.

![](Aspose.Words.1c5c425d-146d-41cc-8eda-fadb02f2b602.001.png)

\- Tất cả các thiết bị đầu cuối hoặc thiết bị định tuyến khi truyền thông đều có tầng network

![](Aspose.Words.1c5c425d-146d-41cc-8eda-fadb02f2b602.002.png)

**b. Nhiệm vụ của tầng Network**

\- Thông qua tầng Network ta có thể đặt được địa chỉ IP cho các thiết bị đầu cuối.

\- Chuyển đổi dữ liệu từ Segments thành Packets (Encapsulation).

\- Định tuyến đường đi của các gói tin (Routing).

\- Chuyển đổi dữ liệu từ Frames thành Packets (De-encapsulating).

**c. Giao thức chính trong tầng Network**

\- Internet Protocol version 4 (IPv4)

\- Internet Protocol version 6 (IPv6)

**2. Giới thiệu về IPv4 header**

![](Aspose.Words.1c5c425d-146d-41cc-8eda-fadb02f2b602.003.png)

\- VER (4 bits): Version hiện hành của IP được cài đặt.

\- IHL(4 bits): độ dài phần header, tính theo đơn vị word.

\- Type of service(8 bits): Thông tin về loại dịch vụ

\- Total Length (16 bits): Chỉ độ dài Datagram.

\- Identification (16bits): Định danh cho một Datagram .

\- Flags(3 bits): Liên quan đến sự phân đoạn các Datagram

\- Fragment Offset (13 bits): Chỉ vị trí của Fragment trong Datagram.

\- Time To Live (TTL-8 bits): Thời gian sống

\- Protocol (8 bits): Chỉ giao thức tầng trên: TCP hay UDP.

\- Header Checksum (16 bits): Mã kiểm soát lỗi CRC

\- Source Address (32 bits): địa chỉ của trạm nguồn.

\- Destination Address (32 bits): Địa chỉ của trạm đích.

\- Option (có độ dài thay đổi): Sử dụng trong trường hợp bảo mật, định tuyến đặc biệt.

\- Padding (độ dài thay đổi): Vùng đệm cho phần Header luôn kết thúc ở 32 bits

\- Data (độ dài thay đổi): Độ dài dữ liệu tối đa là 65.535 bytes, tối thiểu là 8 bytes.

**3. Giới thiệu về IPv6 header (phần nâng cao)**

![](Aspose.Words.1c5c425d-146d-41cc-8eda-fadb02f2b602.004.png)

**a. Khác biệt cơ bản giữa IPv4 header và IPv6 header.**

\- IPv6 là một cải tiến về version của thủ tục Internet hiện thời, IPv4. Tuy nhên, nó vẫn là một thủ tục Internet. Một thủ tục là một tập các quy trình để giao tiếp. Trong thủ tục Internet, thông tin như địa chỉ IP của nơi gửi và nơi nhận của gói tin dữ liệu được đặt phía trước dữ liệu. Phần thông tin đó được gọi là header. Cũng tương tự như khi xác định địa chỉ người nhận và người gửi khi bạn gửi một bưu phẩm qua đường thư tín.

\- Trường địa chỉ nguồn (Source Address) và địa chỉ đích (Destination Address) có chiều dài mở rộng đến 128 bít.

\- Mặc dù trường địa chỉ nguồn và địa chỉ đích có chiều dài mở rộng tới gấp 4 lần số bít, song chiều dài header của IPv6 không hề tăng nhiều so với header của IPv4. Đó là bởi vì dạng thức của header đã được đơn giản hoá đi trong IPv6.

\- Một trong những thay đổi quan trọng là không còn tồn tại trường options trong header của IPv6. Trường Options này được sử dụng để thêm các thông tin về các dịch vụ tuỳ chọn khác nhau. VD thông tin liên quan đến mã hoá có thể được thêm vào tại đây.

\- Vì vậy, chiều dài của IPv4 header thay đổi tuỳ theo tình trạng. Do sự thay đổi đó, các router điều khiển giao tiếp theo những thông tin trong IP header không thể đánh giá chiều dài header chỉ bằng cách xem xét phần đầu gói tin. Điều này làm cho khó khăn trong việc tăng tốc xử lý gói tin với hoạt động của phần cứng.

\- Trong địa chỉ IPv6 thì những thông tin liên quan đến dịch vụ kèm theo được chuyển hẳn tới một phân đoạn khác gọi là header mở rộng “extension header”. Trong hình vẽ trên là header cơ bản. Đối với những gói tin thuần tuý, chiều dài của header được cố định là 40 byte. Về xử lý gói tin bằng phần cứng, có thể thấy trong IPv6 có thể thuận tiện hơn IPv4.

\- Một trường khác cũng được bỏ đi là Header Checksum. Header checksum là 1 số sử dụng để kiểm tra lỗi trong thông tin header, được tính toán ra dựa trên những con số của header. Tuy nhiên, có một vấn đề nảy sinh là header chứa trường TTL (Time to Live), giá trị trường này thay đổi mỗi khi gói tin được truyền qua 1 router. Do vậy, header checksum cần phải được tính toán lại mỗi khi gói tin đi qua 1 router. Nếu giải phóng router khỏi công việc này, chúng ta có thể giảm được trễ.

\- Thực ra, tầng TCP phía trên tầng IP có kiểm tra lỗi của các thông tin khác nhau bao gồm cả địa chỉ nhận và gửi. Vậy có thể thấy các phép tính tương tự tại tầng IP là dư thừa, nên Header Checksum được gỡ bỏ khỏi IPv6.

\- Trường có cùng chức năng với “Service Type” được đổi tên là Traffic Class. Trường này được sử dụng để biểu diễn mức ưu tiên của gói tin, ví dụ có nên được truyền với tốc độ nhanh hay thông thường, cho phép thiết bị thông tin có thể xử lý gói một cách tương ứng. Trường Service Type gồm TOS (Type of Service) và Precedence. TOS xác định loại dịch vụ và bao gồm: giá trị, độ tin cậy, thông lượng, độ trễ hoặc bảo mật. Precedence xác định mức ưu tiên sử dụng 8 mức từ 0-7.

\- Trường Flow Label có 20 bít chiều dài, là trường mới được thiết lập trong IPv6. Bằng cách sử dụng trường này, nơi gửi gói tin hoặc thiết bị hiện thời có thể xác định một chuỗi các gói tin, ví dụ Voice over IP, thành 1 dòng, và yêu cầu dịch vụ cụ thể cho dòng đó. Ngay cả trong IPv4, một số các thiết bị giao tiếp cũng được trang bị khả năng nhận dạng dòng lưu lượng và gắn mức ưu tiên nhất định cho mỗi dòng. Tuy nhiên, những thiết bị này không những kiểm tra thông tin tầng IP ví dụ địa chỉ nơi gửi và nơi nhận, mà còn phải kiểm tra cả số port là thông tin thuộc về tầng cao hơn. Trường Flow Label trong IPv6 cố gắng đặt tất cả những thông tin cần thiết vào cùng nhau và cung cấp chúng tại tầng IP.

\- IPv6 có mục tiêu cung cấp khung làm việc truyền tải thông minh, dễ dàng xử lý cho thiết bị bằng cách giữ cho header đơn giản và chiều dài cố định.

**b. Chức năng của header mở rộng (extension header) trong IPv6**

\- Header mở rộng (extension header) là đặc tính mới trong thế hệ địa chỉ IPv6.

\- Trong IPv4, thông tin liên quan đến những dịch vụ thêm vào được cung cấp tại tầng IP được hợp nhất trong trường Options của header. Vì vậy, chiều dài header thay đổi tuỳ theo tình trạng.

\- Khác thế, địa chỉ IPv6 phân biệt rõ ràng giữa header mở rộng và header cơ bản, và đặt phần header mở rộng sau phần header cơ bản. Header cơ bản có chiều dài cố định 40 byte, mọi gói tin IPv6 đều có header này. Header mở rộng là tuỳ chọn. Nó sẽ không được gắn thêm vào nếu các dịch vụ thêm vào không được sử dụng. Các thiết bị xử lý gói tin (ví dụ router), cần phải xử lý header cơ bản trước, song ngoại trừ một số trường hợp đặc biệt, chúng không phải xử lý header mở rộng. Router có thể xử lý gói tin hiệu quả hơn vì chúng biết chỉ cần nhìn vào phần header cơ bản với chiều dài như nhau.

\- Header mở rộng được chia thành nhiều loại tuỳ thuộc vào dạng và chức năng chúng phục vụ. Khi nhiều dịch vụ thêm vào được sử dụng, phần header mở rộng tương ứng với từng loại dịch vụ khác nhau được đặt tiếp nối theo nhau.

\- Trong cấu trúc header IPv6, có thể thấy 8 bít của trường Next Header. Trường này sẽ xác định xem extension header có tồn tại hay không, khi mà header mở rộng không được sử dụng, header cơ bản chứa mọi thông tin tầng IP. Nó sẽ được theo sau bởi header của tầng cao hơn, tức hoặc là header của TCP hay UDP, và trường Next Header chỉ ra loại header sẽ theo sau

![](Aspose.Words.1c5c425d-146d-41cc-8eda-fadb02f2b602.005.png)

\- Mỗi header mở rộng (extension header) cũng chứa trường Next Header và xác định header mở rộng nào sẽ theo sau nó. Node đầu cuối khi nhận được gói tin chức extension header sẽ xử lý các extension header này theo thứ tự được sắp xếp của chúng.

\- Dạng của extension header: Có 6 loại của extension header: Hop-by-Hop Option, Destination Option, Routing, Fragment, Authentication, and ESP (Encapsulating Security Payload). Khi sử dụng cùng lúc nhiều extension header, thường có một khuyến nghị là đặt chúng theo thứ tự như thế này.

\+ Hop-by-Hop Option: Phía trên có đề cập là thông thường, chỉ có những node đầu cuối xử lý các extension header. Chỉ có một ngoại lệ của quy tắc này là header Hop-by-Hop Option. Header này, như tên gọi của nó, xác định một chu trình mà cần được thực hiện mỗi lần gói tin đi qua một router.

\+ Destination Option: Destination Option header được sử dụng để xác định chu trình cần thiết phải xử lý bởi node đích. Có thể xác định tại đây bất cứ chu trình nào. Chúng tôi đã đề cập là thông thường chỉ có những node đích xử lý header mở rộng của IPv6. Như vậy thì các header mở rộng khác ví dụ Fragment header có thể cũng được gọi là Destination Option header. Tuy nhiên, Destination Option header khác với các header khác ở chỗ nó có thể xác định nhiều dạng xử lý khác nhau.

\+ Routing: Routing header được sử dụng để xác định đường dẫn định tuyến. Ví dụ, có thể xác định nhà cung cấp dịch vụ nào sẽ được sử dụng, và sự thi hành bảo mật cho những mục đích cụ thể. Node nguồn sử dụng Routing header để liệt kê địa chỉ của các router mà gói tin phải đi qua. Các địa chỉ trong liệt kê này được sử dụng như địa chỉ đích của gói tin IPv6 theo thứ tự được liệt kê và gói tin sẽ được gửi từ router này đến router khác tương ứng.

\+ Fragment: Fragment header được sử dụng khi nguồn gửi gói tin IPv6 gửi đi gói tin lớn hơn Path MTU, để chỉ xem làm thế nào khôi phục lại được gói tin từ các phân mảnh của nó. MTU (Maximum Transmission Unit) là kích thước của gói tin lớn nhất có thể gửi qua một đường dẫn cụ thể nào đó. Trong môi trường mạng như Internet, băng thông hẹp giữa nguồn và đích gây ra vấn đề nghiêm trọng. Cố gắng gửi một gói tin lớn qua một đường dẫn hẹp sẽ làm quá tải. Trong địa chỉ IPv4, mối router trên đường dẫn có thể tiến hành phân mảnh (chia) gói tin theo giá trị của MTU đặt cho mỗi giao diện. Tuy nhiên, chu trình này áp đặt một gánh nặng lên router. Bởi vậy trong địa chỉ IPv6, router không thực hiện phân mảnh gói tin (các trường liên quan đến phân mảnh trong header IPv4 đều được bỏ đi).

Node nguồn IPv6 sẽ thực hiện thuật toán tìm kiếm Path MTU, để tìm băng thông hẹp nhất trên toàn bộ một đường dẫn nhất định, và điều chỉnh kích thước gói tin tuỳ theo đó trước khi gửi chúng. Nếu ứng dụng tại nguồn áp dụng phương thức này, nó sẽ gửi dữ liệu kích thước tối ưu, và sẽ không cần thiết xử lý tại tầng IP. Tuy nhiên, nếu ứng dụng không sử dụng phương thức này, nó phải chia nhỏ gói tin có kích thướng lớn hơn MTU tìm thấy bằng thuật toán Path MTU Discovery. Trong trường hợp đó, những gói tin này phải được chia tại tầng IP của node nguồn và Fragment header được sử dụng.

\+ Authentication and ESP: Ipsec là phương thức bảo mật bắt buộc được sử dụng tại tầng IP. Mọi node IPv6 phải thực thi Ipsec. Tuy nhiên, thực thi và tận dụng lại là khác nhau, và Ipsec có thực sự được sử dụng trong giao tiếp hay không phụ thuộc vào thời gian và từng trường hợp. Khi Ipsec được sử dụng, Authentication header sẽ được sử dụng cho xác thực và bảo mật tính đồng nhất của dữ liệu, ESP header sử dụng để xác định những thông tin liên quan đến mã hoá dữ liệu, được tổ hợp lại thành extension header. Trong IPv4, khi có sử dụng đến Ipsec, thông tin được đặt trong trường Options.

IPv6 ứng dụng một hệ thống tách biệt các dịch vụ gia tăng khỏi các dịch vụ cơ bản và đặt chúng trong header mở rộng (extension header), cao hơn nữa phân loại các header mở rộng theo chức năng của chúng. Làm như vậy, sẽ giảm tải nhiều cho router, và thiết lập nên được một hệ thống cho phép bổ sung một cách linh động các chức năng, kể cả các chức năng hiện nay chưa thấy rõ ràng.

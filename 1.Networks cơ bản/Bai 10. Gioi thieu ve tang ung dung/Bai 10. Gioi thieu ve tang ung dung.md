Chức năng của tầng ứng dụng và các giao thức sử dụng

**I. Nội dung chính:**

\1. Vai trò của tầng ứng dụng.

\2. Mô tả về tầng ứng dụng trong mô hình OSI và TCP/IP.

\3. Mô hình quản lý các dịch vụ trong tầng ứng dụng.

\4. Giới thiệu về các dịch vụ và giao thức trong tầng ứng dụng.

**II. Nội dung chi tiết:**

**1. Vai trò của tầng ứng dụng (Application):** là tầng cung cấp giao diện chính để người dùng tương tác với chương trình ứng dụng. Thông qua các phần mềm, dịch vụ, giao thức sẽ giúp cho người dùng truy nhập các thông tin và dữ liệu trên mạng. Một số ví dụ về các ứng dụng trong tầng này bao gồm: Web, Mail, FTP, Telnet...

**2. Mô tả về tầng ứng dụng trong mô hình OSI và TCP/IP:**

\+ Mô hình OSI là mô hình phần tầng 7 lớp. Thông qua mô hình này giúp cho người học người sản xuất dễ tiếp cận và nghiên cứu hơn.

\+ Mô hình TCP/IP là một bộ các giao thức truyền thông. Nó là chồng giao thức mà Internet và hầu hết các mạng máy tính chạy trên đó. Bộ giao thức này được đặt tên theo hai giao thức chính của nó là TCP (Giao thức điều khiển vận chuyển dữ liệu) và IP (Giao thức Liên mạng).

|![C:\E5941AA5\960AD48C-E505-445E-8391-0EFA6CF17FE4\_files\image001.png](Aspose.Words.a0804f6d-8626-4d6e-b0c9-b3b8cfbe636f.001.png "image001")|
| :- |
\+ Mô tả về tầng ứng dụng trong OSI và TCP/IP: 

=> Trong mô hình OSI thì tầng ứng dụng được tách biệt ra để dễ học và phân tích. Tầng ứng dụng được mô tả là tầng để người dùng có thể ra lệnh, yêu cầu các thao tác thông qua các chương trình ứng dụng. Từ các chương trình ứng dụng ở tầng 7 nó sẽ được Presentation phiên dịch ra để máy tính hiểu, còn tầng Session sẽ đàm phán phiên truyền.

=> Trong TCP/IP: Application nó bao gồm 3 tầng đó là Application, Presentation, Session. Dữ liệu ở tầng ứng dụng chuyển luôn xuống tầng Transport. Cách thức làm việc vẫn đủ 3 tầng nhưng trên thiết bị  sẽ được đóng gọn hơn.

**3. Mô hình quản lý các dịch vụ trong tầng ứng dụng:**

a. Client Server: là máy con (đóng vài trò máy khách) gửi một yêu cầu (request) đến máy chủ (đóng vai trò người cung dịch vụ), máy chủ sẽ xử lý và trả kết quả về cho máy con. Ta thường thấy là dịch Web, Mail, DNS....

b. Peer to Peer: là mạng ngang hàng. Ngang hàng về mặt chức năng và ứng dụng. Hoạt động các ứng dụng đều đặt ở tầng 7. Hai máy trực tiếp nói chuyện với nhau vì tầng 7 không phụ thuộc vào đường truyền.

**4. Giới thiệu về các dịch vụ và giao thức trong tầng ứng dụng là:** DNS, Web, Mail, Telnet, FTP, VPN



|**Tên dịch vụ**|**Tên tiếng anh**|**Giao thức dịch vụ**|**Giao thức truyền thông**|**Port dịch vụ**|
| :- | :- | :- | :- | :- |
|DNS|Domain Name System|DNS|TCP/UDP|53|
|Web|<p>+ Hypertext Transfer Protocol </p><p>+ Hypertext Transfer Protocol Secure</p>|<p>HTTP</p><p>HTTPS</p>|<p>TCP</p><p>TCP</p>|<p>80</p><p>443</p>|
|Mail|<p>+ Simple Mail Transfer Protocol</p><p>+ Post Office Protocol </p>|<p>SMTP</p><p>POP (POP3)/IMAP</p>|<p>TCP</p><p>UDP</p>|<p>25</p><p>110, 143</p>|
|DHCP|+ Dynamic Host Configuration Protocol|<p>DHCP Server</p><p>DHCP Client</p>|<p>UDP</p><p>UDP</p>|<p>67</p><p>68</p>|
|FTP|File Transfer Protocol|FTP|TCP|<p>20 (truyền dữ liệu)</p><p>21(giao tiếp phiên truyền)</p>|
|Telnet|Telnet|Telnet|TCP|23|
|SSH|Secure Shell| | | |
|Chat|Internet chat|IM|TCP|531|
| | | | | |


|![C:\E5941AA5\960AD48C-E505-445E-8391-0EFA6CF17FE4\_files\image002.png](Aspose.Words.a0804f6d-8626-4d6e-b0c9-b3b8cfbe636f.002.png "image002")|
| :- |
**a. Dịch vụ DNS:** là một dịch vụ phân giải tên miền có cơ sở dữ liệu phân cấp, phân tán đồng thời có chứa cơ chế ánh xạ từ tên miền tới những địa chỉ IP và ngược lại. DNS sử dụng Port giao tiếp là 53. 

\+ Để hoạt động được thì DNS phải có 2 thành phần: DNS Server và DNS Client.

=> DNS Server dùng để phân giải tên miền ra IP và ngược lại là IP sang tên miền. Thông qua tìm kiếm trên cơ sở dữ liệu của nó, nếu không có nó sẽ đi hỏi DNS khác.

=> DNS Client dùng để phân giải cho máy người dùng. Khi người dùng truy cập tên miền DNS Client sẽ nhờ sang DNS Server phân giải. 

\+ Trong DNS Server có 2 thành phần chính là:

=> Forward lookup zone sẽ phân giải các bản ghi từ Tên sang địa chỉ IP

=> Reverse lookup zone sẽ phân giải các bản ghi từ IP sang Tên

\+ DNS Server sử dụng 2 giao thức để hoạt động là TCP và UDP:

=> TCP dùng để đóng gói khi 2 Server DNS trao đổi dữ liệu với nhau. Đảm bảo an toàn cho dữ liệu.

=> UDP dùng để đóng gói khi Client yêu cầu phân giải tên miền.

\+ Cách thức hoạt động: 

=> Bước 1: Trên máy người dùng truy cập Website: htttp://google.com.vn bằng IE. Lập tức IE sẽ nhờ DNS Client phân giải tên miền google.com.vn sang địa chỉ IP.

=> Bước 2: Gói tin của DNS client sẽ được chuyển xuống tầng Transport và đóng gói giao thức UDP. Sau đó chuyển xuống Network.

=> Bước 3: Network sẽ đóng IP nguồn là IP máy tính, IP đich sẽ là IP DNS Server. Ta hay nhập ở dòng Preferred DNS.

=> Bước 4: Đã có IP nguồn và IP đích, dữ liệu sẽ chuyển xuống tầng bên dưới và truyền tới đúng DNS Server 

=> Bước 5: Khi yêu cầu gửi tới DNS Server nó sẽ tìm trong cơ sở dữ liệu của mình xem tền miền đó ứng địa chỉ IP của Server Website nào.

=> Bước 6: Sau khi tìm được nó sẽ gửi lại cho máy có DNS Client yêu cầu.

=> Bước 7: IP của Server Website đã sẵn sàng cho tầng Network đóng vào gói dữ liệu của gói tin truy cập Website

**b. Dịch vụ Mail:** là dịch vụ thư điện tử. Thay vì nội dung thư của bạn được viết lên giấy và chuyển đi qua đường bưu điện thì email được lưu dưới dạng các tệp văn bản trong máy tính và được chuyển đi qua đường Internet. Với email, người nhận cho dù ở xa bạn nửa vòng trái đất hay ngay cùng phòng làm việc với bạn, việc gửi và nhận thư cũng đều được thực hiện gần như ngay lập tức.

\+ Để dịch vụ Mail hoạt động được thì phải đảm bảo 2 thành phần: Mail Server, Mail Client.

**=> Mail Server:** dùng để nhận mail từ người dùng rồi chuyển Mail đi. Sau khi nhận được mail chuyển lại, sẽ phân phối mail sang cho người dùng. Trong Mail Server có 2 thành phần chính là MTA (Mail Transfer Agent) dùng để quản lý mail, MDA (Mail Delivery Agent) dùng để phân phối mail cho client.

**=> Mail Client:** dùng để gửi mail của người dùng đi lên Mail Server và nhận từ Server về để hiển thị cho người dùng xem.

\+ Mail Client sử dụng theo POP sẽ cắt toàn bộ Mail trên Server về, nếu sử dụng theo IMAP là lấy theo tiêu đề về. Tiêu đề nào lựa chọn thì sẽ lấy về. Giữ lại một bản trên Server.

\+ Các bước hoạt động: 

=> Bước 1: Mail Client gửi mail lên Server bằng giao thức SMTP thông qua Port 25 

=> Bước 2: Mail Server sẽ nhận mail từ Client bằng giao thức SMTP thông qua Port 25, quản lý bằng MTA, và gửi mail đi.

=> Bước 3: Mail Server sẽ nhờ DNS Client của mình gửi tới  DNS Server để phân giải từ tên miền Mail (vd:mail.google.com) ra địa chỉ IP của Mail Server đó.

=> Bước 4: Sau khi có địa chỉ IP của Mail Server kia thì Mail Server sẽ  liên lạc trực tiếp, rồi gửi và nhận Mail từ Mail Server đó qua Port 25. Sau đó sẽ chuyển sang Mail Box thông qua MDA để người dùng lấy về.

=> Bước 5: Người dùng sẽ lấy Mail từ trong Mail Box thông qua giao thức POP3.

**c. Dịch vụ DHCP:** là dịch vụ cấp phát địa chỉ IP động. Trong một hệ thống lớn có nhiều máy, thay vì chúng ta phải đi nhập IP bằng tay cho tất cả các máy thì chúng ta dùng DHCP cấp phát IP. 

\+ Để dịch vụ DHCP hoạt động được nó phải có 2 thành phần: DHCP Server và DHCP Client

=> DHCP Server dùng để cấp phát IP động sử dụng Port 67. Gửi IP hoặc nhận thông tin đều ở Port này.

=> DHCP Client dùng để nhận IP, xin cấp phát IP sử dụng Port 68. Xin IP hoặc nhận IP đều dùng ở Port này. 

\+ Có 4 bản tin được sử dụng:

=> Bản tin 1: là Discover

=> Bản tin 2: là Offer

=> Bản tin 3: là Request

=> Bản tin 4: là ACK

\+ Các bước hoạt động: 

=> Bước 1: DHCP Client sẽ gửi một bản tin Broadcast là Discover. Bản tin là thông tin yêu cầu xin địa chỉ IP. Bản tin sẽ được tầng Transport nhận bằng cổng 68 sau đó đóng gói bằng giao thức UDP  rồi truyền xuống dưới. Tầng Network Access sẽ đóng địa chỉ MAC nguồn là máy mình và MAC đích là MAC Broadcast  rồi chuyển ra đường truyền. Do có địa chỉ MAC là Broadcast nên tất cả các máy trong mạng đều nhận được, trong đó có máy DHCP Server.

=> Bước 2: Sau khi DHCP Server nhận được gói tin nó sẽ được tầng Network Access sẽ chuyển lên bên trên để xử lý. Tầng Transport sẽ nhận thông tin rồi chuyển lên Port 67 cho tầng Application.

=> Bước 3: Sau khi DHCP Server xử lý, Server sẽ gửi lại một bản tin Offer bao gồm thông tin địa chỉ IP cấp cho máy Client và thông tinh máy của mình như tên, IP. Rồi chuyển xuống cho tầng Transport đóng gói bằng cổng 67. Tầng Transport sẽ đóng bằng giao thức UDP và tiếp tục chuyển xuống đóng địa chỉ MAC nguồn MAC đích. Tiếp theo dữ liệu sẽ gửi ra đường truyền.

=> Bước 4: Client nhận dữ liệu từ Port 68 và đưa IP vào DHCP Client. Sau đó DHCP Client sẽ gửi lại một bản tin Request là đồng ý sử dụng IP đó để DHCP Server xác nhận

=> Bước 5: DHCP Server nhận được thông tin từ DHCP Client sẽ gửi lại một bản tin ACK để xác nhận là quá trình đã thành công.

\+ Trên hệ thống mạng Client nào gửi gói tin tới DHCP tới trước sẽ nhận được. Lỗi hay xẩy ra sẽ xung đột DHCP nếu hệ thống có nhiều thiết bị cấp phát.

**d. Dịch vụ Web:** là dịch vụ liên kết trang siêu văn bản. Dùng để truyền thông tin tới người dùng một cách đa dạng và phong phú.

\+ Dịch vụ Web dùng 2 cách để gửi dữ liệu tới người dùng đó là HTTP (không bảo mật) và HTTPS (có bảo mật).

\+ Để dịch vụ Web hoạt động được nó phải có 2 thành phần: Web Server và Web Client

=> Web Server là nơi cung cấp dữ liệu Web. Người ta xây dựng lên một Website để người dùng truy cập vào. Web Server sẽ chạy ở Port 80 hoặc 443.

=> Web Client là phía người dùng. Người dùng mở IE hoặc Firefox truy cập vào tên miền của trang Web.

\+ Các bước hoạt động: 

=> Bước 1: Người dùng truy cập tên miền Website bằng Web Client là IE hoặc Firefox. Web Client sẽ sinh ra một Port cao và dữ liệu từ tầng Application sẽ chuyển xuống tầng Transport.

=> Bước 2:. Đồng thời Web Client sẽ nhờ DNS Client phân giải hộ tên miền ra địa chỉ IP Web Server.

=> Bước 3: Transport nó thấy dữ liệu là Web nó sẽ đóng Port cao và Port Web Server là 80 hoặc 443 bằng giao thức TCP rồi truyền xuống dưới.

=> Bước 4: Dữ liệu sẽ được tầng Internet đóng IP máy mình và IP máy Web Server (IP Web Server được DNS Client nhờ DNS Server phân giải hộ).

=> Bước 5: Sau khi dữ liệu đóng IP sẽ đưa xuống tầng Network Access. Tầng này sẽ dùng giao thức MAC kết hợp với các giao thức khác để truyền gói tin tới Swicht, tới Router và tới Máy chủ Web Server.

=> Bước 6: Sau khi dữ liệu tới được Web Server nó sẽ được chuyển lên tầng Internet để kiểm tra IP, nếu đúng sẽ chuyển lên tầng Transport và chuyển lên tầng Application theo Port 80 hoặc 443. 

=> Bước 7: Webserver sẽ xử lý yêu cầu và Sau đó dữ liệu được đóng lại và gửi xuống đường truyền. Gói tin sẽ truyền lại tới máy Webclient

=> Bước 8: Khi Client nhận được nó sẽ được Transport chuyển lên IE hoặc Firefox đúng vào Port cao khi khởi tạo (do có Port cao này nên ta có thể mở nhiều cửa sổ trên một trình duyệt với nhiều Website khác nhau mà không sợ bị trùng). 

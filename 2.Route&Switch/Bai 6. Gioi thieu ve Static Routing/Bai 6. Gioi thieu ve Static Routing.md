**Giới thiệu về định tuyến tĩnh**

**Nội dung chi tiết**

\- Như chúng ta đã biết, router thực hiện việc định tuyến dựa vào một công cụ gọi là bảng định tuyến (routing table). Nguyên tắc là mọi gói tin IP khi đi đến router sẽ đều được tra bảng định tuyến, nếu đích đến của gói tin thuộc về một entry có trong bảng định tuyến thì gói tin sẽ được chuyển đi tiếp, nếu không, gói tin sẽ bị loại bỏ. Bảng định tuyến trên router thể hiện ra rằng router biết được hiện nay có những subnet nào đang tồn tại trên mạng mà nó tham gia và muốn đến được những subnet ấy thì phải đi theo đường nào.

Để hiểu rõ vấn đề, ta cùng xem xét ví dụ 1:

![Hinh-1-So-do-vi-du-1](http://www.ntps.edu.vn/images/blog/Hinh-1-So-do-vi-du-1.jpg "Hinh-1-So-do-vi-du-1")

Hình 1 – Sơ đồ ví dụ 1.

\- Trên hình 1 là hai router đại diện cho hai chi nhánh khác nhau của một doanh nghiệp : R1 cho chi nhánh 1 và R2 cho chi nhánh 2. R1 sử dụng cổng f0/0 của nó đấu xuống mạng LAN của chi nhánh 1, mạng này sử dụng subnet 192.168.1.0/24. Tương tự, R2 sử dụng cổng f0/0 của nó đấu xuống mạng LAN của chi nhánh 2, mạng này sử dụng subnet 192.168.2.0/24. Subnet sử dụng cho kết nối leased – line nối giữa hai chi nhánh (qua các cổng serial của hai router) là 192.168.12.0/30.

Mặc định ban đầu, khi ta chưa cấu hình định tuyến trên các router R1 và R2 thì hai mạng LAN của hai chi nhánh R1 và R2 chưa thể đi đến nhau được (tức là, nếu lấy một PC trong LAN 1, chẳng hạn như PC1 ping thử đến một PC trong LAN 2, ví dụ PC4, ping sẽ không thành công). Lý do của điều này là các router R1 và R2 chưa có thông tin về các mạng LAN của nhau trong bảng định tuyến do đó không thể chuyển gói tin đi đến các mạng LAN này. Ta kiểm tra bằng cách hiển thị bảng định tuyến trên các router R1 và R2. Câu lệnh để hiển thị bảng định tuyến trên router là ‘show ip route’ :

Bảng định tuyến của R1:

R1#show ip route

Gateway of last resort is not set

`     `192.168.12.0/30 is subnetted, 1 subnets

C       192.168.12.0 is directly connected, Serial2/0

C   192.168.1.0/24 is directly connected, FastEthernet0/0

Bảng định tuyến của R2:

R2#show ip route

*(đã bỏ bớt một số dòng)*

Gateway of last resort is not set

`     `192.168.12.0/30 is subnetted, 1 subnets

C       192.168.12.0 is directly connected, Serial2/0

C   192.168.2.0/24 is directly connected, FastEthernet0/0

\- Từ kết quả hiển thị, ta thấy rằng mỗi router ban đầu chỉ học được thông tin về những subnet kết nối trực tiếp với nó. Ví dụ: router R1 biết rằng có mạng 192.168.12.0/30 kết nối trực tiếp vào cổng serial 2/0 và mạng 192.168.1.0/24 kết nối trực tiếp vào cổng fast ethernet 0/0 của nó. Các router hoàn toàn không có thông tin gì về các subnet ở xa, không kết nối trực tiếp với mình. Do đó, giả sử PC1 muốn ping PC4, nó sẽ đóng gói một gói tin IP ICMP với địa chỉ nguồn là 192.168.1.1 và đích đến là 192.168.2.2. Khi gói tin này đi lên đến router R1, R1 tra bảng định tuyến thấy rằng đích đến 192.168.2.2 không thuộc về bất kỳ subnet nào mà R1 có trong bảng định tuyến nên nó drop bỏ gói tin này.

\- Vậy để hai mạng 192.168.1.0/24 và 192.168.2.0/24 có thể đi đến nhau được, các router phải điền được thông tin về hai mạng này vào trong bảng định tuyến của mình. Có hai cách thức để thực hiện điều đó: một là người quản trị tự điền tay các thông tin – định tuyến tĩnh, hai là các router tự trao đổi thông tin định tuyến với nhau và tự điền các thông tin còn thiếu vào bảng định tuyến của mình – định tuyến động. Ở đây ta khảo sát cách thực hiện là định tuyến tĩnh.

\- Việc cấu hình định tuyến tĩnh trên router Cisco được thực hiện bằng cách sử dụng lệnh có cú pháp như sau:

Router(config)#ip route *destination\_subnet* *subnetmask* {*IP\_next\_hop* | *output\_interface*} [*AD*] 

Trong đó:

destination\_subnet: mạng đích đến.

Subnetmask: subnet – mask của mạng đích.

IP\_next\_hop: địa chỉ IP của trạm kế tiếp trên đường đi.

output\_interface: cổng ra trên router.

AD: chỉ số AD của route khai báo, sử dụng trong trường hợp có cấu hình dự phòng.

Cụ thể trong ví dụ này:

Từ R1 muốn đi đến mạng 192.168.2.0/24 , ta phải đi ra khỏi cổng s2/0. Để thể hiện điều đó vào bảng định tuyến, ta thực hiện cấu hình:

R1(config)#ip route 192.168.2.0 255.255.255.0 s2/0

Tương tự, Từ R2 muốn đi đến mạng 192.168.1.0/24 , ta phải đi ra khỏi cổng s2/0. Cấu hình:

R2(config)#ip route 192.168.1.0 255.255.255.0 s2/0

Sau khi đã cấu hình xong các route cho các mạng 192.168.1.0/24 và 192.168.2.0/24, ta thực hiện kiểm tra bằng cách hiển thị bảng định tuyến trên mỗi router:

Bảng định tuyến của R1:

R1#show ip route

Gateway of last resort is not set

`     `192.168.12.0/30 is subnetted, 1 subnets

C       192.168.12.0 is directly connected, Serial2/0

C    192.168.1.0/24 is directly connected, FastEthernet0/0

S    192.168.2.0/24 is directly connected, Serial2/0

Bảng định tuyến của R2:

R2#show ip route

Gateway of last resort is not set

`     `192.168.12.0/30 is subnetted, 1 subnets

C       192.168.12.0 is directly connected, Serial2/0

S    192.168.1.0/24 is directly connected, Serial2/0

C    192.168.2.0/24 is directly connected, FastEthernet0/0

\- Ta thấy rằng các thông tin còn thiếu trước đây đã xuất hiện trên bảng định tuyến của các router R1 và R2. Các entry mới điền thêm này được ký hiện bởi kí tự “S” ở đầu dòng thể hiện rằng các thông tin định tuyến này được học vào bảng định tuyến thông qua định tuyến tĩnh ( ta cũng để ý rằng các dòng mô tả các mạng kết nối trực tiếp được ký hiệu bởi kí tự “C” – connected – kết nối trực tiếp).

Khi các PC đã chỉ default – gateway đầy đủ lên các cổng đấu nối của các router, ping kiểm tra giữa các PC thuộc hai mạng LAN sẽ thành công:

![Hinh-2-Ping-kiem-tra-giua-PC1-va-PC4](http://www.ntps.edu.vn/images/blog/Hinh-2-Ping-kiem-tra-giua-PC1-va-PC4.jpg "Hinh-2-Ping-kiem-tra-giua-PC1-va-PC4")

Hình 2 – Ping kiểm tra giữa PC1 và PC4 từ PC1.

\- Bên cạnh việc chỉ đường bằng cổng ra (output interface), ta cũng có thể chỉ đường trong câu lệnh bằng địa chỉ IP next – hop, đây chính là địa chỉ IP của trạm kế tiếp trên đường đi đến mạng đích.

Trên R1:

R1(config)#ip route 192.168.2.0 255.255.255.0 192.168.12.2

Trên R2:

R2(config)#ip route 192.168.1.0 255.255.255.0 192.168.12.1

Như ta đã thấy trên hình 1, từ R1 muốn đi đến mạng 192.168.2.0/24 thì phải đi qua trạm kế tiếp là R2 có địa chỉ IP là 192.168.12.2 và từ R2 muốn đi đến mạng 192.168.1.0/24 thì phải đi qua trạm kế tiếp là R1 có địa chỉ IP là 192.168.12.1.

\- Hai kiểu cấu hình này có tác dụng như nhau, điểm khác biệt là route static được khai báo theo kiểu output – interface sẽ có AD = 0 còn route static được khai báo theo kiểu IP next – hop sẽ có AD = 1. Ngoài ra nếu cổng ra là một cổng multi – access thì ta nên sử dụng kiểu khai báo IP next – hop (vấn đề này sẽ được đề cập và giải thích chi tiết trong một bài viết khác).

Ví dụ trên đây đã mô tả một cách cơ bản nhất cách khai báo static route trên các router. Tiếp theo, ta cùng khảo sát một ví dụ khác phức tạp hơn, sơ đồ lần này sẽ có 03 router:

![Hinh-3-So-do-vi-du-2](http://www.ntps.edu.vn/images/blog/Hinh-3-So-do-vi-du-2.jpg "Hinh-3-So-do-vi-du-2")

Hình 3 – Sơ đồ ví dụ 2.

Yêu cầu đặt ra là cấu hình định tuyến tĩnh trên các router đảm bảo cho mọi địa chỉ trên sơ đồ thấy nhau.

Tương tự như ví dụ 1, trên mỗi router ta sẽ thực hiện điền thông tin về các subnet không kết nối trực tiếp vào bảng định tuyến của mỗi router sử dụng câu lệnh câu hình static route:

Trên R1:

R1(config)#ip route 192.168.2.0 255.255.255.0 s2/0

R1(config)#ip route 192.168.23.0 255.255.255.0 s2/0

R1(config)#ip route 192.168.3.0 255.255.255.0 s2/0

Trên R2:

R2(config)#ip route 192.168.1.0 255.255.255.0 s2/0

R2(config)#ip route 192.168.3.0 255.255.255.0 s2/1

Trên R3:

R1(config)#ip route 192.168.1.0 255.255.255.0 s2/1

R1(config)#ip route 192.168.12.0 255.255.255.0 s2/1

R1(config)#ip route 192.168.2.0 255.255.255.0 s2/1

Lưu ý rằng chúng ta phải điền đầy đủ thông tin định tuyến trên tất cả các router, vì nếu như chỉ cần một router nào đó trên đường đi của gói tin bị thiếu route, gói tin sẽ bị drop giữa đường. Chẳng hạn, giả sử ta quên cấu hình chỉ đường đi đến mạng 192.168.3.0/24 trên R2. Gói tin xuất phát từ mạng 192.168.1.0/24 đi đến mạng 192.168.3.0/24 khi đi đến R1 sẽ được chuyển tiếp qua cổng s2/0 để đi tiếp (vì điều này đã được chỉ ra trong cấu hình định tuyến tĩnh của R1), tuy nhiên khi đi đến R2 nó sẽ bị drop bỏ vì R2 thiếu thông tin của mạng 192.168.3.0/24.

Ta cùng xem xét tiếp ví dụ thứ 3 về cấu hình đường dự phòng trong đó có sử dụng đến tham số AD trong câu lệnh cấu hình:

![Hinh-4-So-do-vi-du-3](http://www.ntps.edu.vn/images/blog/Hinh-4-So-do-vi-du-3.jpg "Hinh-4-So-do-vi-du-3")

Hình 4 – Sơ đồ ví dụ 3.

Lần này yêu cầu đặt ra như sau: cấu hình định tuyến tĩnh đảm bảo R1 đi đến LAN 2 của R2 theo đường đi ra cổng s2/0 là chính, đường s2/1 là dự phòng, ngược lại, R2 lại đi đến LAN 1 của R1 theo đường đi ra cổng s2/1 là chính, đường s2/0 là dự phòng. Có nghĩa là, R1 khi chuyển gói tin đi LAN 2 của R2 luôn sử dụng cổng ra là s2/0, khi cổng s2/0 này down thì tự động chuyển đường qua s2/1, khi cổng s2/0 up lại, lại chuyển về sử dụng cổng s2/0. Tương tự với R2.

Để thực hiện yêu cầu này, chúng ta sử dụng tham số AD trong câu lệnh cấu hình định tuyến tĩnh. Như đã nói, static route có thể có hai chỉ số AD là 0 (khi cấu hình chỉ cổng ra) và 1 (khi cấu hình chỉ next – hop). Ta có thể thay đổi các giá trị mặc định này để phục vụ cho việc cấu hình dự phòng.

Nhắc lại rằng AD dùng để so sánh độ ưu tiên giữa các route. Khi tồn tại nhiều đường đi đến cùng một đích đến, đường đi nào có chỉ số AD nhỏ hơn, đường đi đó sẽ được đưa vào bảng định tuyến để sử dụng, những đường còn lại có AD cao hơn sẽ được dùng để dự phòng cho đường chính thức. Do đó ta chỉ việc chọn AD nhỏ hơn (ví dụ là 5) cho đường chính và chọn AD lớn hơn (ví dụ là 10) cho đường phụ.

Cấu hình trên R1:

R1(config)#ip route 192.168.2.0 255.255.255.0 Serial2/0 5

R1(config)#ip route 192.168.2.0 255.255.255.0 Serial2/1 10

Cấu hình trên R2:

R2(config)#ip route 192.168.1.0 255.255.255.0 Serial2/1 5

R2(config)#ip route 192.168.1.0 255.255.255.0 Serial2/0 10

Ta thực hiện kiểm tra kết quả cấu hình trên R1:

Đầu tiên, ta hiển thị bảng định tuyến để xem đường nào đã được đưa vào bảng:

R1#show ip route

`     `192.168.12.0/30 is subnetted, 1 subnets

C       192.168.12.0 is directly connected, Serial2/0

`     `192.168.21.0/30 is subnetted, 1 subnets

C       192.168.21.0 is directly connected, Serial2/1

C    192.168.1.0/24 is directly connected, FastEthernet0/0

S    192.168.2.0/24 is directly connected, Serial2/0

Ta thấy đường được đưa vào bảng định tuyến để sử dụng có cổng ra là s2/0 đúng như yêu cầu.

Tiếp theo ta thử tính dự phòng bằng cách shutdown cổng s2/0 của R1:

R1(config)#interface s2/0

R1(config-if)#shutdown

R1(config-if)#

\*Mar 1 00:15:48.971: %LINK-5-CHANGED: Interface Serial2/0, changed state to administratively down

\*Mar 1 00:15:49.971: %LINEPROTO-5-UPDOWN: Line protocol on Interface Serial2/0, changed state to down

Đường chính đã không còn, ta hiển thị lại bảng định tuyến để chắc chắn rằng đường phụ (đi ra cổng s2/1) đã được đưa vào bảng định tuyến:

R1#show ip route

`     `192.168.12.0/30 is subnetted, 1 subnets

C       192.168.12.0 is directly connected, Serial2/0

`     `192.168.21.0/30 is subnetted, 1 subnets

C       192.168.21.0 is directly connected, Serial2/1

C    192.168.1.0/24 is directly connected, FastEthernet0/0

S    192.168.2.0/24 is directly connected, Serial2/1

Ta thực hiện mở lại cổng s2/0 và kiểm tra rằng đường đi qua cổng này lại được đưa lại vào bảng định tuyến để sử dụng:

R1(config)#interface s2/0

R1(config-if)#no shutdown

R1(config-if)#

\*Mar 1 00:19:36.767: %LINK-3-UPDOWN: Interface Serial2/0, changed state to up

R1(config-if)#

\*Mar 1 00:19:37.775: %LINEPROTO-5-UPDOWN: Line protocol on Interface Serial2/0, changed state to up

R1#show ip route

`     `192.168.12.0/30 is subnetted, 1 subnets

C       192.168.12.0 is directly connected, Serial2/0

`     `192.168.21.0/30 is subnetted, 1 subnets

C       192.168.21.0 is directly connected, Serial2/1

C    192.168.1.0/24 is directly connected, FastEthernet0/0

S    192.168.2.0/24 is directly connected, Serial2/0

Thực hiện kiểm tra tương tự trên R2.

\- Nhìn chung, định tuyến tĩnh có ưu điểm là khá dễ hiểu và cũng dễ cấu hình. Thêm nữa, định tuyến tĩnh còn có một ưu điểm khác là không gây hao tốn tài nguyên mạng do không có sự trao đổi thông tin định tuyến giữa các router. Tuy nhiên nhược điểm của định tuyến tĩnh là hoàn toàn không thích hợp với những mạng có quy mô lớn (ta không thể cấu hình tay khai báo các route khi số lượng lên đến hàng trăm được!) và không hội tụ với mọi sự thay đổi trên sơ đồ mạng khi mà cổng ra vẫn ở trạng thái up/up. Để khắc phục các nhược điểm này, chúng ta phải sử dụng định tuyến động bằng cách chạy một giao thức định tuyến nào đó. 


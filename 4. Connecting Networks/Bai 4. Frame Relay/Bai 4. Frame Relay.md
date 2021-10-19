Frame Relay

Thursday, November 29, 2012

9:42 AM

**I. Nội dung chính**

\1. Giới thiệu về Frame Relay

\2. Thuật ngữ của công nghệ Frame Relay:

\3. Các kiểu sơ đồ đấu nối Frame Relay:

\4. Frame Relay Subinterfaces:

\5. Frame Relay Address Mapping:

6.Cấu hình Frame Relay:



**II. Nội dung chi tiết:**

**1. Giới thiệu về Frame Relay:**

\+ Khi một doanh nghiệp có nhiều chi nhánh nằm cách xa nhau cần phải kết nối thì ta có thể thuê các đường Leased-Line sử dụng công nghệ PPP. Đường Leased-Line có ưu điểm là một đường vật lý riêng biệt cho chúng ta, nhưng chi phí cao và đắt. 

\+ Ngoài công nghệ PPP người ta còn sử dụng công nghệ Frame Relay, ATM để đấu nối WAN. 

|![C:\07340E25\12F96FF1-58F8-4D99-8A11-6F1E942B1FB0\_files\image001.png](Aspose.Words.01d846d8-f9d9-413f-bc7f-24a83b039236.001.png "image001")|
| :- |
\+ Frame Relay là một dạng công nghệ mở rộng LAN vào trong mạng WAN.

=> Frame Relay hoạt động ở tầng 2 của mô hình OSI.

=> Khi kết nối nhiều mạng chi nhánh lại ta chỉ cần một đường vật lý từ Switch chạy Frame Relay. Từ một đường vậy lý này Swich chạy Frame Relay sẽ chạy tạo ra nhiều đường kết nối ảo (Virtual Circuits).

=> Các gói tin này sẽ được đóng theo dạng Frame Relay.

=> Frame Relay trên Switch sẽ thiết lập trước các đường đi. Đảm bảo độ tin cậy cho truyền tin.



**2. Thuật ngữ của công nghệ Frame Relay:**

|![C:\07340E25\12F96FF1-58F8-4D99-8A11-6F1E942B1FB0\_files\image002.png](Aspose.Words.01d846d8-f9d9-413f-bc7f-24a83b039236.002.png "image002")|
| :- |
**a.  Xét các Router kết nối các mạng của một doanh nghiệp**

=> Nếu sử dụng đường Leased-Line thì 4 Router phải mất 12 đường vật lý kết nối.

=> Nếu sử dụng Frame Relay thì 4 Router chỉ mất 4 đường vật lý kết nối tới Swich chạy Frame Relay của nhà cung cấp dịch vụ.

**b. Các thuật ngữ:**

\+ Đường vật lý kết nối các router về Switch Frame Relay gọi là Local Access Loop. 

=> Đường Local Access Loop có tốc độ bằng một đường T1 = 1,544 Mbps/s

=> Tốc độ truy nhập của đường Local Access Loop được gọi là Access Rate, nó chỉ nằm ở phần truy cập từ Router tới nhà cung cấp dịch vụ ISP mà thôi.

\+ Các Router trao đổi thông tin với Switch Frame Relay bằng các bản tin LMI (Local Management Interface):

=> LMI dùng để theo dõi kết nối từ Router khách hàng lên Frame Relay Switch.

=> Các giá trị trong LMI là DLCI (Data Link connection Identifier). DLCI dùng để định danh các đường mạch ảo thường trực PVC (Permanent Virtual Circuits). Bốn đường ảo sẽ có 4 DLCI khác nhau.

=> DLCI chỉ có giá trị trong nội bộ một đường vật lý (từ Switch Frame Relay về Router). Sang đường vật lý khác có thể điền giá trị DLCI giống nhau.

\+ Đường PVC (Permanent Virtual Circuits): là đường mạch ảo thường trực, nó được thiết kế liên tục ổn định. Khi các Router không trao đổi dữ liệu đường này vẫn tồn tại.

=> Khi thuê đường PVC thì chúng ta sẽ có cam kết với nhà cung cấp dịch vụ về tốc độ đường truyền, được gọi là CIR

=> CIR (committed information rate): là tốc độ thực sự của đường PVC đơn vị là (bps). Nếu người dùng gửi quá tốc độ cho phép của CIR thì sẽ có bít DE bật lên xử lý.

=>  Bit DE (Discard Eligibility): khi người dùng gửi các Frame vào lớn hơn tốc độ cho phép thì sẽ được đánh dấu bằng bit DE, bình thường truyền sẽ không sao nhưng khi có sự nghẽn mạng thì những Frame này sẽ bị hủy bỏ.

=> Bit FECN (Forward Explicit Congestion Notification): là bit chỉ báo đang có nghẽ. Khi frame đi vào sẽ được đánh bit này. Khi bị nghẽn nó sẽ chuyển lên các tầng bên trên cho các giao thức TCP/UDP xử lý để truyền chậm lại

=> Bit BECN (Backward Explicit Congestion Notification): là báo nghẽn chiều ngược lại (FECN là chiều gói tin đi, BECN là chiều về)

\+ Đường SVC (switched virtual circuits): có tính chất quay số. Khi Router gửi dữ liệu thì được thiết lập. Khi Router gửi xong thì ngắt kết nối.



**3. Các kiểu sơ đồ đấu nối Frame Relay:**

|![C:\07340E25\12F96FF1-58F8-4D99-8A11-6F1E942B1FB0\_files\image003.png](Aspose.Words.01d846d8-f9d9-413f-bc7f-24a83b039236.003.png "image003")|![C:\07340E25\12F96FF1-58F8-4D99-8A11-6F1E942B1FB0\_files\image004.png](Aspose.Words.01d846d8-f9d9-413f-bc7f-24a83b039236.004.png "image004")|
| :- | :- |
\+ Kiểu Full Mesh: 

=> Các Router có các đường kết nối dùng để backup cho nhau

\+  Kiểu Star (Hub-and-Spoke):

=> Các Router có một đường kết nối tới một Router chính. Khả năng dự phòng không cao (giống mạng LAN của chúng ta nhưng thay bằng Router. Nhưng giá thành thuê đường truyền lại thấp hơn nhiều so với Full Mesh

\+  Kiểu Partial-Mesh: Một số node nào quan trọng thì cho kết nối backup, cái nào không quan trọng thì bỏ qua.

\+ Môi trường Frame Relay: là môi trường đa truy nhập.

=> Nó không thể gửi gói tin Broadcast từ các Router này tới Router kia được.



**4. Frame Relay Subinterfaces:**

|<p>![C:\07340E25\12F96FF1-58F8-4D99-8A11-6F1E942B1FB0\_files\image005.png](Aspose.Words.01d846d8-f9d9-413f-bc7f-24a83b039236.005.png "image005")</p><p> </p>|<p> </p><p>RA</p><p> </p><p> </p><p> </p><p>RB</p><p> </p><p> </p><p>RC</p>|
| :- | :- |
\+ Giả sử sau khi các Router chạy định tuyến với nhau bằng giao thức Distance Vector nào đó (RIP, EIGRP). Thì  Router R thấy được mạng A, R thấy được B, R thấy được C. Nhưng các Router sẽ không thấy được mạng của nhau vì nó sử dụng tính năng Split Horizon. Tính năng Split Horizone sẽ không gửi quảng bá những bảng định tuyến nó đã học trở về cổng đó.

\+ Giải pháp khắc phục là người ta chia Subinterfaces:

=> Chia Subinterface trên cổng S0/0 tương ứng với 3 đường. Ở đây chia Subinterface trên cổng WAN.



**5. Frame Relay Address Mapping:** 

\+ Khi đưa dữ liệu xuống đóng thì cần phải tương quan giữa lớp 3 và lớp 2

\+ Số DLCI sẽ gán cho các đường PVC kết nối tới Router

\+ Khi chuyển gói tin tương quan giữa IP đầu xa và DLCI đầu gần sẽ sử dụng 2 cơ chế: Inverse ARP (tự động map) hoặc Frame Relay Map (điền bằng tay)

|![C:\07340E25\12F96FF1-58F8-4D99-8A11-6F1E942B1FB0\_files\image006.png](Aspose.Words.01d846d8-f9d9-413f-bc7f-24a83b039236.006.png "image006")|
| :- |


**6.Cấu hình Frame Relay:**

**a. Cấu hình cơ bản:** 

=> R1(config)# int s0/0/0

=> R1(config-if)# no shut

=> R1(config-if)# ip add 10.0.0.1 255.255.2550

=> R1(config-if)# encapsulation Frame-Relay  (không dùng câu lệnh này nó sẽ đóng gói theo HDLC)

=> R1(config-if)# no Frame-relay IARP

=> R1(config-if)# Frame-relay map IP 10.0.0.2 102  broadcast (Frame relay không gửi broadcast nên nó phải giả broadcast).

**b. Cấu hình Point to Point:** 

=> R1(config)# int s0/0/0

=> R1(config-if)# no shut

=> R1(config-if)# encapsulation Frame-Relay

=> R1(config-if)# exit

=> R1(config)#interface serial 0/0/0  102  point-to-point

=> R1(config-if)#ip address 10.0.0.1 255.255.2550

=> R1(config-if)# frame-relay interface-dlci  102

=> R1(config-if)# exit

=> R1(config)#interface serial 0/0/0  103  point-to-point

=> R1(config-if)#ip address 10.0.0.1 255.255.2550

=> R1(config-if)# frame-relay interface-dlci  103



=> R2(config)# int s0/0/0

=> R2(config-if)# no shut

=> R2(config-if)# encapsulation Frame-Relay

=> R2(config-if)# exit

=> R2(config)#interface serial 0/0/0  201  point-to-point

=> R2(config-if)#ip address 10.0.0.2 255.255.2550

=> R2(config-if)# frame-relay interface-dlci  201

=> R2(config-if)# exit

=> R2(config)#interface serial 0/0/0  103  point-to-point

=> R2(config-if)#ip address 10.0.0.2 255.255.2550

=> R2(config-if)# frame-relay interface-dlci  203



**c. Cấu hình Multipoint:**

=> R1(config)# int s0/0/0

=> R1(config-if)# no shut

=> R1(config-if)# encapsulation Frame-Relay

=> R1(config-if)# exit

=> R1(config)#interface s0/0/0.102  multipoint

=> R1(config-if)#ip address 10.17.0.1 255.255.2550

=> R1(config-if)# frame-relay map ip 10.17.0.2  120  broadcast

=> R1(config-if)# frame-relay map ip 10.17.0.3  130  broadcast

=> R1(config-if)# frame-relay map ip 10.17.0.4  140  broadcast



**d. Các lệnh kiểm tra.**

=> R1# show interface s0/0/0 (kiểm tra Frame relay trên cổng)

=> R1# show frame-relay LMI

=> R1# Show frame-relay map







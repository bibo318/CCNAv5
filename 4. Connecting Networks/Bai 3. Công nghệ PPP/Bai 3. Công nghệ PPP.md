PPP (Point-to-Point)

Tuesday, November 27, 2012

10:07 AM

**I. Nội dung chính:**

\1. Giới thiệu về công nghệ đóng gói trên WAN

\2. Giới thiệu về giao thức PPP 

\3. Các bước thiết lập phiên PPP

\4. Tìm hiểu giao thức xác thực PAP, CHAP

\5. Các bước cấu hình xác thực



**II. Nội dung chi tiết:**

**1. Giới thiệu về công nghệ đóng gói trên WAN:**

|![C:\0F9BEC85\EF2C07A4-3830-483E-9B41-A6D690BF869C\_files\image001.png](Aspose.Words.e50a0cf5-a368-448f-bef6-f59426dfbd84.001.png "image001")|
| :- |
** 

**2. Giới thiệu về giao thức PPP:** 

\+ Giao thức PPP sử dụng kết nối điểm tới điểm từ Router này tới Router kia hoặc sử dụng trên một đường quay số, hoặc sử dụng trên một đường ADSL (ADSL sử dụng PPPoE: Point-to-Point Protocol over Ethernet).

\+ PPP có thể mang nhiều giao thức khác nhau như TCP/IP, IPX, Apple talk... thông qua sử dụng bộ phận NCP (Network Control Protocol). 

\+ PPP có thể điều khiển việc thiết lập các đường Link và tùy chỉnh thiết lập đường Link bằng bộ phận LCP (Link Control Protocol).

\+ Dữ liệu được đóng gói lớp 2 theo PPP. 



**3. Các bước thiết lập phiên PPP:**

\+ Pha đầu tiên là thiết lập đường Link giữa 2 Router

\+ Pha thứ 2 là xác thực lẫn nhau giữa 2 Router này thông qua giao thức xác thực PAP, CHAP.

\+ Pha thứ 3 là triển khai giao thức PPP sau khi thiết lập
**


**4. Tìm hiểu giao thức xác thực PAP, CHAP:**

**a. Giao thức xác thực PAP:**

\+ Sử dụng bắt tay 2 bước:

|![C:\0F9BEC85\EF2C07A4-3830-483E-9B41-A6D690BF869C\_files\image002.png](Aspose.Words.e50a0cf5-a368-448f-bef6-f59426dfbd84.002.png "image002")|
| :- |
=> Bước 1: Router bên A muốn truy nhập sang Router bên B thì phải gửi thông tin là: User name, Pasword dưới dạng Clear text

=> Bước 2: Router B đồng ý và chấp nhận kết nối

\+ Dạng gói tin gửi sang là Clear text nên không bảo mật về User name, Password



**b. Giao thức xác thực CHAP:**

\+ Sử dụng bắt tay 3 bước:

|![C:\0F9BEC85\EF2C07A4-3830-483E-9B41-A6D690BF869C\_files\image003.png](Aspose.Words.e50a0cf5-a368-448f-bef6-f59426dfbd84.003.png "image003")|
| :- |
=> Bước 1: Router A bên HQ (headquarter là trung tâm) gửi sang Router kia một mẫu tin Challenge

=> Bước 2: Router B sử dụng hàm băm để băm mẫu tin và User name, Password của mình kia rồi gửi lại thông tin là Response

=> Bước 3: Router HQ kiểm tra thông tin. Nếu thấy phù hợp nó sẽ gửi đáp trả là xác nhận.

\+ Gói tin Response gửi sang đã được băm ra nên nó bảo mật được User name, Password.



**5. Các bước cấu hình xác thực:**

**a. Các bước cấu hình PAP:**

Cấu hình trên R1:

=> R1 (config)# username R2 password **cisco** (password phải giống nhau)

Cấu hình xác thực:

=> R1 (config)# int S0/0

=> R1 (config-if)# encapsulation PPP

=> R1 (config-if)# ppp authentication pap

=> R1 (config-if)# ppp pap sent-username R1 password cisco

Cấu hình bên R2:

=> R2 (config)# username R1 password **cisco** (password phải giống nhau)

Cấu hình xác thực:

=> R2 (config)# int S0/0

=> R2 (config-if)# encapsulation PPP

=> R2 (config-if)# ppp authentication pap

=> R2 (config-if)# ppp pap sent-username R2 password cisco

**b. Các bước cấu hình CHAP:**

Cấu hình trên R1:

=> R1 (config)# username **cisco** pass **123456a@** (password phải giống nhau)

Cấu hình xác thực:

=> R1 (config)# int S0/0

=> R1 (config-if)# encapsulation PPP

=> R1 (config-if)# ppp authentication chap

=> R1 (config-if)# ppp chap hostname **bkap**

=> R1 (config-if)# ppp chap password **123456a@**

Cấu hình bên R2:

=> R2 (config)# username **bkap** password **123456a@** (password phải giống nhau)

Cấu hình xác thực:

=> R1 (config-if)# encapsulation PPP

=> R1 (config-if)# ppp authentication chap

=> R1 (config-if)# ppp chap hostname **cisco**

=> R1 (config-if)# ppp chap password **123456a@**

**c. Câu lệnh kiểm tra:**

=> show interfaces serial

=> debug ppp authentication

**d. Bổ sung:**

Compression (nén dung lượng khi truyền: chỉ dùng trên Router thật):

Router(config-if)#compress [predictor | stac]

Link Quality Monitoring (giám sát và giới hạn băng thông truyền):

Router(config-if)#ppp quality percentage

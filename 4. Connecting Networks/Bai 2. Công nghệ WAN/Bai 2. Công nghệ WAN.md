Công nghệ WAN

Thursday, November 29, 2012

11:11 AM

**I. Nội dung chính**

\1. Giới thiệu về mạng WAN

\2. So sánh công nghệ mạng LAN và WAN

\3. Dịch vụ sử dụng trong WAN

\4. Thiết bị sử dụng trong mạng WAN

\5. Tần vật lý mạng WAN

\6. Giao thức Data link chạy trên mạng WAN



**II. Nội dung chi tiết:**

**1. Giới thiệu về mạng WAN (Wide Area Network):** là mạng diện rộng kết nối các máy tính trong phạm vi giữa các tòa nhà, các thành phố hay một quốc gia, một vùng lãnh thổ hoặc giữa các vùng lãnh thổ trong một châu lục bằng đường viễn thông hoặc tín hiệu vệ tinh.

|![C:\26430AE5\3E2D4815-D947-46CA-99B4-FF897F71BDA6\_files\image001.png](Aspose.Words.df0d988a-8b08-489d-a2ee-f669fb36f3d7.001.png "image001")|
| :- |


**2. So sánh công nghệ mạng LAN và WAN:**

|So sánh|WANs|LANs|
| :- | :- | :- |
|Mô hình vật lý|khu vực có vị trí địa lý rộng|trong tòa nhà, trong công ty|
|Quyền hạn sử dụng|<p>Phải đi thuê đường truyền của nhà cung cấp dịch vụ để đấu nối</p><p>các hệ thống mạng lại với nhau</p>|Sở hữu riêng trong công ty|


**3. Dịch vụ sử dụng trong WAN:**

|![C:\26430AE5\3E2D4815-D947-46CA-99B4-FF897F71BDA6\_files\image002.png](Aspose.Words.df0d988a-8b08-489d-a2ee-f669fb36f3d7.002.png "image002")|
| :- |
\+ Dịch vụ của WAN nó nằm từ tầng Network trở lên

\+ Khi triển khai ra hệ thống truy nhập WAN thì nó nằm ở tầng Physical và Data link

=> Physical là nó đến thiết bị vật lý, đường truyền tín hiệu

=> Data link nó đến các công nghệ: HDLC (truy cập điểm tới điểm)...



**4. Thiết bị sử dụng trong mạng WAN:**

|![C:\26430AE5\3E2D4815-D947-46CA-99B4-FF897F71BDA6\_files\image003.png](Aspose.Words.df0d988a-8b08-489d-a2ee-f669fb36f3d7.003.png "image003")|
| :- |
\+ Router: có cổng đấu nối WAN như cổng Searial, hay công nghệ đường truyền quang FTTH sử dụng cổng fastethernet kết nối

\+ Terminal Server: cho phép truy nhập vào để cấu hình nhiều Router ở đầu xa cùng lúc

\+ Modem: là các bộ điều chế tín hiệu dùng cho các đường ADSL

\+ DSU/CSU: (Data Service Unit và Channal Service Unit) dùng chuyển đổi định dạng vật lý từ đường truyền này sang đường kia

\+ Trong có sử dụng thêm những con Router Core: 

=> ATM Swtich (Asynchronous Transfer Mode), không phải máy rút tiền ATM.

=> Frame Relay Switch: là những thiết bị chuyển mạch Frame Relay
**


**5. Tần vật lý mạng WAN:** 

|![C:\26430AE5\3E2D4815-D947-46CA-99B4-FF897F71BDA6\_files\image004.png](Aspose.Words.df0d988a-8b08-489d-a2ee-f669fb36f3d7.004.png "image004")|![C:\26430AE5\3E2D4815-D947-46CA-99B4-FF897F71BDA6\_files\image005.png](Aspose.Words.df0d988a-8b08-489d-a2ee-f669fb36f3d7.005.png "image005")|
| :- | :- |
\+ DSU/CSU là khối thiết bị do nhà cung cấp dịch vụ lắp cho mình

\+ Để kết nối Router của mình với nhà cung cấp dịch vụ sẽ dùng cáp V35

\+ DTE (Data Terminal Equipment) là phía người sử dụng

\+ DCE (Data Circuit Terminaling Equipment) là phía cuối của nhà cung cấp dịch vụ

\+ Cổng cáp WIC-1T:

=> Các đầu nối về Router đều là Searial hết

=> Đầu nối về nhà cung cấp dịch vụ hay sử dụng là đầu nối V.35 (tùy vào nhà cung cấp).



**6. Giao thức Data link chạy trên mạng WAN:**

\+ HDLC hay sử dụng dạng kết nối kênh trắng điểm tới điểm (Leased lines)

\+ PPP hay sử dụng dạng kết nối kênh trắng (Leased lines)

\+ Frame Relay

\+ ATM

=> Các tùy chọn khi triển khai:

|![C:\26430AE5\3E2D4815-D947-46CA-99B4-FF897F71BDA6\_files\image006.png](Aspose.Words.df0d988a-8b08-489d-a2ee-f669fb36f3d7.006.png "image006")|
| :- |
=> PSTN: là công nghệ chuyển mạch kênh dùng cho điện thoại bây giờ. Khi 2 điện thoại đang liên lạc nó sẽ không liên lạc bất kỳ ai.

=> Frame Relay, ATM là chuyển mạch gói.







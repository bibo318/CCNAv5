**Spanning Tree Protocol**

**I. Nội dung chính:**

\1. Giới thiệu về Switch dự phòng và Loop tầng 2

\2. Cơ chế hoạt động của STP: dựa vào 4 bước

\+ Bầu chọn Root-SW

\+ Bầu chọn Root Port

\+ Bầu chọn Designated Port

\+ Khóa cổng: Blocking Port

\3. Các bộ định thời gian Spanning Tree

\+ Hello timer: 2s

\+ Forword delay timer: 15s

\+ Max-Age-Timer: 20s

\4. Cơ chế giao thức Spanning Tree chạy trên thiết bị Cisco: pVST+ (per VLAN STP)

\5. Cấu hình STP

\6. Lệnh chống bão Broadcast trên cổng cho STP



**II. Nội dung chi tiết:** 

**1. Giới thiệu về Switch dự phòng và Loop tầng 2:** 

**a. Tính dự phòng:** hệ thống xây dựng tính dự phòng để duy trì ổn định 

|![C:\8B6B1AA5\82355F07-3614-4CE0-8B8B-0A29494D54E4\_files\image001.png](Aspose.Words.133562e8-a963-4185-aa63-4c79902e6ca7.001.png "image001")|
| :- |
**b. Loop và bão Broadcast:**

\+ Khi cấu hình kết nối backup nó sẽ xẩy ra Loop và cơn bão broadcast cỏ thể xây ra.

|![C:\8B6B1AA5\82355F07-3614-4CE0-8B8B-0A29494D54E4\_files\image002.png](Aspose.Words.133562e8-a963-4185-aa63-4c79902e6ca7.002.png "image002")|![C:\8B6B1AA5\82355F07-3614-4CE0-8B8B-0A29494D54E4\_files\image003.png](Aspose.Words.133562e8-a963-4185-aa63-4c79902e6ca7.003.png "image003")|
| :- | :- |
\+ Loop xẩy ra khi: ta có Pc1 tới Pc4, khi pc1 gửi gói tin tới Switch 2, Switch 2 sẽ gửi gói tin tới S3 và S1 vì Swtich mặc định là forward ra đường Trunking và cùng vlan. Tới S1 nó lại forward ra f0/3 và forward tới đường Trung 3. Sau đó S3 lại gửi lại cho S2, tương tự no sẽ chạy lòng vòng rồi dẫn ra Loop.

\+ Broadcast khi Pc cần  giử toàn mạng. Dữ liệu sẽ tới Switch 2 sau đó Switch 2 sẽ gửi sang Switch 3. no sẽ chạy lòng vòng.



**2. Cơ chế hoạt động của STP:** dựa vào 4 bước

\+ Xét 4 Swtich A, B, C, D kết nối như sau:

|![C:\8B6B1AA5\82355F07-3614-4CE0-8B8B-0A29494D54E4\_files\image004.png](Aspose.Words.133562e8-a963-4185-aa63-4c79902e6ca7.004.png "image004")|
| :- |
\+ Các gói tin trao đổi dữ liệu giữa các Switch là BPDU(Bridge Protocol Data Unit): là loại gói tin sử dụng trong STP 

**a. Xét bầu Root-SW:** 

\+ Trong BPDU có thành phần quan trọng là Bridge-ID. 

\+ Bridge-ID dài 8 bytes: 

=> 2bytes: là của Priority => Priority chạy từ 0 tới 65535.  Giá trị mặc định là: 32768

=> 6 bytes là của địa chỉ MAC

\+ Đầu tiên Switch nào cũng cho mình ra Root-SW. Nhưng sau một hồi trao đổi BPDU thì nó chọn ra Switch có Bridge-ID nhỏ làm Root

=> (B-ID)min = Root-SW

=> Để biết được (B-ID)min nó sẽ xem thông số Priority của ai nhỏ nhất. nếu cả 2 có Priotity bằng nhau nó sẽ xét tới MAC. Vì MAC là duy nhất trên thế giớ nên phải có tham số nhỏ nhất. 

=> Trên địa chỉ MAC nó sẽ xét từ trái qua phải: 00:1F:29:e5:1d:22 và 00:1F:29:e5:1d:21 thì MAC 2 là nhỏ hơn.

\+ Khi Switch A có MAC là nhỏ nhất vậy sau khi trao đổi thông tin các Router sẽ bầu Switch A là Root-SW

\+ Khi có Root-SW: thì nó định kỳ gửi 2s một lần. Các Switch khác chỉ được foword thông tin của BPDU

**b. Xét bầu Root-Port:** 

\+ Trên tất cả các Switch không phải là Root-SW phải bầu ra một Root-Port

\+ Root-Port: là Port cung cấp đường về Root-SWcho con Switch đang xét mà có tổng chi phí là nhỏ nhất. 

=> Mỗi cổng của Switch khi tham gia đều có một giá trị là Cost, Cost sẽ biến đổi tùy thuộc vào Bandwidth trên cổng.

|Bandwidth|Cost|Bandwidth|Cost|
| :- | :- | :- | :- |
|10Mbps|100|1Gbps|4|
|100Mbps|19|10Gbps|2|
=> Switch A đi sang D cổng 1 thì có giá trị là 19 (A tính bằng 0, sang D là 19). Từ D về là 19. 

=> Switch A đi sang D theo cổng 2 thì có giá trị là 57 (A sang B, sang C tới D). vậy Cost nhỏ nhất là 19 suy ra Root-Port là cổng hướng DA

|![C:\8B6B1AA5\82355F07-3614-4CE0-8B8B-0A29494D54E4\_files\image005.png](Aspose.Words.133562e8-a963-4185-aa63-4c79902e6ca7.005.png "image005")|![C:\8B6B1AA5\82355F07-3614-4CE0-8B8B-0A29494D54E4\_files\image006.png](Aspose.Words.133562e8-a963-4185-aa63-4c79902e6ca7.006.png "image006")|
| :- | :- |
|Trường hợp C có Cost về cổng B và D bằng nhau|Trường hợp C có 2 cổng về B |
=> Trường hợp đường về 2 cổng của Switch C là bằng nhau mà chỉ duy nhất dược một Switch Port: thì cổng nào nối với Bridge-ID nhỏ hơn thì sẽ làm Root-Port.

=> Trường hợp C nối lên B là 2 dây, B có Bridge-ID < D thì C sẽ dựa vào 2 thành phần:

\- Dựa vào Port priority: chạy từ 0-255 mặc định là 128

\- Port Number:  là cổng f0/1 và f0/2 thì f0/1 là Root Port

**c. Designated Port:** trên mỗi phân đoạn mạng phải bầu ra Designated Port. Nó cung cấp đường về Root-SW cho phân đoạn mạng mà có tổng chi phí là nhỏ nhất.

\+ Phân đoạn mạng: A tới B là một phân đoạn, B tới C là một phân đoạn

|![C:\8B6B1AA5\82355F07-3614-4CE0-8B8B-0A29494D54E4\_files\image007.png](Aspose.Words.133562e8-a963-4185-aa63-4c79902e6ca7.007.png "image007")|
| :- |
=> Xét một thực thể đứng giữa D và C. Ta xét theo nguyên tắc đi vào thì tính đi ra không tính vậy có đường từ X =>D =>A là 19. Đường X=>C=>B=>A là 38 vậy nó sẽ chọn đường có giá trị là 19 vậy cổng bị khóa có giá trị là 38

d. Khóa cổng (Blocking Port): Khi xác định được cổng có Designated Port bé nó sẽ khóa cổng còn lại

**3. Các bộ định thời Spanning Tree**

\+ Hello timer: 2s

=> khoảng thời gian định kỳ Root-SW gửi BPDU

\+ Forword delay timer: 15s

=> Để hiểu được ta phải kết hợp với các trạng thái cổng STP Port States

|Disabled|` `Cổng bị tắt|
| :- | :- |
|Blocking|Một port chỉ được nhận BPDU, không được gửi BPDU, Không được học địa chỉ MAC, không được forword data|
|Listening|Nhận và gửi BPDU, không học MAC, không gửi Data|
|Learning|Nhận và gửi BPDU, thêm học địa chỉ MAC, không được chuyển Data|
|Forwarding|nhận, gửi BPDU, được học địa chỉ MAC, được chuyển Data|
=> cổng nào bị khóa sẽ đưa vào trạng thái blocking.

=> cổng không bị khóa nó chưa được gửi ngay mà đi vào trạng thái Listening và chờ 15s

=> sau đó chuyển sang Learning mới được học

=> sau đó mới chuyển sang Forwarding.

=> dùng để chống Loop

\+ Max-Age-Timer: một cổng đang nhận BPDU mà không nhận được nữa thì nó sẽ bật lên trong vòng 20s để làm thời gian chờ bật lại. 

**4. Cơ chế giao thức Spanning Tree chạy trên thiết bị Cisco: pVST+ (per VLAN STP)**

\+ Switch Cisco sẽ cho một VLAN chạy một cây Spanning Tree.

\+ Trường Priority của của Bridge-ID sẽ khác so với Bridge-ID bình thường

=> Có tổng là 2bytes là 16 bit. 4bit đầu là Priority. Từ bit 11 trở về bit 0 là lưu thông tin VLAN mà cây Spanning Tree đang chạy

|**15**|**14**|**13**|**12**|11|10|9|8|7|6|5|4|3|2|1|0|
| :- | :- | :- | :- | :- | :- | :- | :- | :- | :- | :- | :- | :- | :- | :- | :- |
=> Trường Priority đầu có 4 bit vậy nó có 24 (2 mũ 4 bit) là 16 giá trị.

=> Cách tính của PVST+

\- 1.212 = 4096 (0001)

\- 1.213=8192  (0010)

\- 1.212 +1.213= 12288 (0011)

\- Ta thấy Priority chạy PVST+ đều là bội số của 4096

=> Cách tính kết hợp với VLAN

\- Xét VLAN là 1: ta có:  1.212 + 1.20 = 4097

\- Xét VLAN là 2: ta có:  1.212 + 1.21 = 4098

**5. Cấu hình STP:**

**a. Một số điểm cần lưu ý khi cấu hình Switch Cisco**

=> Mặc định Switch Cisco là bật mặc định STP. 

=> Mode default là PVST+ là mỗi VLAN chạy một cây STP

=> Switch Cisco không hỗ trợ SPT truyền thống là 802.1D mà phải PVST+ 

**b. Các lệnh hiệu chỉnh STP:** 

\+ Cấu hình Root SW: phải chỉ ra vì nó cần có cấu hình mạnh

=> Tùy chọn 1 trong 2 trường hợp: SW(config)#spanning-tree vlan  n  root [primary | secondary]

vd: SW(config)#spanning-tree vlan  3  root primary (chỉ ra Switch nào làm Root).

=> Chỉ cố định luôn: SW(config)#spanning-tree vlan  n  priority gt (giá trị priority mong muốn phải chia hết cho 4096)

vd: SW(config)#spanning-tree vlan  3  priority 8192 

\+ Cấu hình Port Fast:

=> SW(config)# int f0/10

=> SW(config-ip)# switchport mode access

=> SW(config-ip)# Spanning-tree portfast

**c. Các lệnh Show:** 

=> Show Spanning-tree  vlan  n

vd: Show Spanning-tree  vlan  3

**6. Lệnh chống bão Broadcast trên cổng cho STP:**

=> storm-control broadcast level pps 1500 1000 

\+ upper =1500 (gói giới hạn được đi qua)

\+ Low = 1000 (cảnh báo)

=> Configure terminal

interface <id>

` `storm-control {broadcast|multicast|unicast} level {level [level-low] | bps bps [bps-low] | pps pps [pps-low]}

` `for example:

` `block at 80% utilization, unblock at 50%

storm-control broadcast level 80 50

` `or

` `block at 100 pps, unblock at 70 pps

storm-control broadcast pps 100 70

` `storm-control action {shutdown | trap}

**7. Block Unicast và Multicast Flooding:** 

=> Switch# configure terminal

=> Switch(config)# interface gigabitethernet0/1

=> Switch(config-if)# switchport block multicast

=> Switch(config-if)# switchport block unicast

=> Switch(config-if)# end

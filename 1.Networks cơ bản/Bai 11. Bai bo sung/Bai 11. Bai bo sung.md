**Bài bổ sung: làm trên thiết bị thật**

**1. Load IOS Cisco 2600 bằng lệnh:**

\+ Trên Server:

=> Cài đặt TFTP Server 

=> Copy IOS c2600-is-mz.113-2.0.2.Q vào thư mục của TFTP 

\+ Trên Router:

=>  Khởi động lại Router và nhấn Ctrl + Break

=> Trong Rommon ta thiết lập như sau:

rommon 1 > set                                                               => Xem thông tin

rommon 2 > IP\_ADDRESS=10.10.3.100                      => Địa chỉ IP cho port

rommon 3 > IP\_SUBNET\_MASK=255.255.255.0       => Subnet mask

rommon 4 > DEFAULT\_GATEWAY=10.10.3.1          => Default gateway

rommon 5 > TFTP\_SERVER=10.10.3.1                       => Địa chỉ TFTP server

rommon 6 > TFTP\_FILE=c2600-is-mz.113-2.0.2.Q    => tên file cần nạp 

rommon 7 > sync                                                           => để lưu giá trị vào NVRAM 

rommon 8 > tftpdnld                                                     => Bắt đầu quá trình nạp

**2. Load IOS Cisco 2600 bằng Xmodem:**

**a. Giới thiệu:**

-IOS image được đặt trên PC, dùng giao thức truyền Xmodem hay Ymodem để truyền file IOS qua router qua cổng console. Trong thực tế ta có thể gặp tình huống này khi router bị mất IOS.

\- Có thể truyền IOS image từ máy tính ở xa bằng cách nối modem với cổng console của router nối qua mạng điện thoại thông thường (PSTN). Máy tính từ xa cũng nối modem với mạng điện thoại , từ máy tính này quay số và kết nối với router.

\- Để truyền IOS image từ một máy tính cục bộ, kết nối cổng console router với cổng serial của máy tính, dùng cáp null-modem (tức cáp rollover). Tốc độ cổng console cấu hình trên router phải phù hợp với tốc độ cổng serial (COM1 hoặc COM2) của PC.

**b. Các bước thực hiện:**

1.Nối router với máy tính qua cổng console, khởi động router.

2.Đặt tốc độ lại cho cổng console là 115200 bps.

3.Khởi động lại router .

4.Chỉnh lại thông số chương trình HyperTermial cho phù hợp.

5.Dùng lệnh xmodem để bắt đầu quá trình nhận file trên router.

6.Khởi động quá trình truyền file bằng xmodem từ chương trình HyperTermial.

7.Chờ tới khi quá trình truyền hoàn tất, router khởi động từ IOS mới.

8.Đặt lại tốc độ 9600 bps cho cổng console (tức đặt lại giá trị mặc định cho thanh ghi).

**c. Thực hiện**

**B1. Một router khi không có IOS image trong flash lúc khởi động sẽ vào tự động vào chế độ ROM monitor.** Dấu nhắc ROM monitor khác nhau ở các nhóm router 2600, 3600 và router 2500.

**Router 2600**

rommon 1>

**Đối với router 2500, dấu nhắc sẽ có dạng:**

\>

Đặt lại tốc độ cổng console là 115200 bps và khởi động lại router

Đối với Router 2600

Dùng lệnh confreg để đặt lại giá trị thanh ghi cấu hình, có thể thực hiện bằng hai cách:

rommon 2 > confreg 0x3822

You must reset or power cycle

rommon 3 > reset

hoặc chỉ đánh lệnh confreg sau đó trả lời các câu hỏi theo sau:

**rommon 2 > confreg**

Configuration Summary

enabled are:

load rom after netboot fails

console baud: 9600

boot: image specified by the boot system commands

or default to: cisco2-C2600

do you wish to change the configuration? y/n [n]: y

enable "diagnostic mode"? y/n [n]: n

enable "use net in IP bcast address"? y/n [n]: n

disable "load rom after netboot fails"? y/n [n]: n

enable "use all zero broadcast"? y/n [n]: n

enable "break/abort has effect"? y/n [n]: y

enable "ignore system config info"? y/n [n]: n

change console baud rate? y/n [n]: y

enter rate: 0 = 9600, 1 = 4800, 2 = 1200, 3 = 2400

4 = 19200, 5 = 38400, 6 = 57600, 7 = 115200 [0]: 7

change the boot characteristics? y/n [n]: n

Configuration Summary

enabled are:

load rom after netboot fails

break/abort has effect

console baud: 115200

boot: image specified by the boot system commands

or default to: cisco2-C2600

do you wish to change the configuration? y/n [n]: n

You must reset or power cycle for new config to take effect

rommon 3 > reset

Đối vói router 2500

\>o/r 0x3822 đặt lại giá trị thanh ghi

\>i khởi động lại router

**B2. Sau khi khởi động lại router, tốc độ bit đã thay đổi, phải thiết lập kết nối mới (File – New Connection ...)**

\- Chỉnh lại thông số HyperTermial cho phù hợp với tốc độ console mới là 115200 baud. Với tốc độ này sẽ giảm thời gian truyền IOS image."\_nR!1bŒ›R ký tự lạ xuất hiện do không phù hợp tốc độ phải chỉnh lại thông số COM1 như sau:

**B3. Thực hiện lệnh xmodem với thông số theo sau là file IOS image muốn nhận.**

rommon 1 > xmodem c2600-io3-mz.121-5.T

Do not start the sending program yet...

File size Checksum File name

4032136 bytes (0x3d8688) 0xaca4 2600.12.0.7.bin

WARNING: All existing data in bootflash will be lost!

Invoke this application only for disaster recovery.

Do you wish to continue? y/n [n]: y

Ready to receive file c2600- io3-mz.121-5.T ...

**B4. Khi màn hình hiện thông báo đã sẵn sàng nhận file, right click trên màn hình chọn Send File ... (hoặc chọn từ menu Transfer / Send File ...)**

Chọn Filename thích hợp và Protocol là Xmodem; nhấn Send

Thực hiện chỉnh các thông số như các hộp thoại sau:

**Giao thức gởi file Xmodem**

(tại HyperTeminal)

Erasing flash at 0x607c0000

program flash location 0x60510000

Download Complete! chờ tới khi thông báo hoàn tất quá trình kiểm tra, router tự khởi động lại

program load complete, entry point: 0x80008000, size: 0x517174

**B5. Router đã khởi động lại, đặt giá trị thanh ghi về mặc định**

Would you like to enter the initial configuration dialog? [yes/no]: No

Router#config t

Enter configuration commands, one per line. End with CNTL/Z.

Router(config)#config-register 0x2102 ¬ Thay đổi giá trị thanh ghi về mặc định

Router(config)#exit

**B6. Kiểm tra lại file mới đã được nạp**

Router#show flash

System flash directory:

File Length Name/status

1 5337744 c2600-io3-mz.121-5.T file mới đã lưu trong flash

[5337808 bytes used, 3050800 available, 8388608 total]

8192K bytes of processor board System flash (Read/Write)

Router#show version

Cisco Internetwork Operating System Software

IOS (tm) C2600 Software (C2600-IO3-M), Version 12.1(5)T, RELEASE SOFTWARE(fc1)

System image file is "flash:2600.12.0.7.bin"

Basic Rate ISDN software, Version 1.1.

1 FastEthernet/IEEE 802.3 interface(s)

1 Serial network interface(s)

1 ISDN Basic Rate interface(s)

32K bytes of non-volatile configuration memory.

8192K bytes of processor board System flash (Read/Write)

Configuration register is 0x3822 (will be 0x2102 at next reload)

Router#copy run start 

**3. Load IOS cho Switch:** 

\+ Do Switch load IOS thông qua cổng Console và theo giao thức Xmodem. Sử dụng phần mềm SecureCRT hoặc Hyper terminal

Bước 1: Kiểm tra Baud Rate mặc định là 9600 sẽ load rất lâu nên chuyển về 115200 

=> Switch: BAUD=115200

Bước 2: thực hiện quá trình load

=> Switch: copy xmodem: flash:bootfile => ấn Enter

=> Trên SecureCRT hoặc Hyper terminal ta vào: Tranfer => Send Xmodem => chọn IOS và nhấn Send

Bước 3: Set lại BAUD để không bị kí tự lạ:

=> Switch: BAUD=9600

Bước 4: Khởi động lại Switch bằng câu lệnh reset

**4. Phá mật khẩu Router 2600:**

\+ Chế độ không lấy thông tin từ NVRAM

=> Khởi động lại Router và nhấn Ctrl + Break

rommon 1 > confreg 0x2142  

rommon 1 > reset

=> Sau đó vào Router:

Router#copy startup-config running-config  (copy lại file cấu hình trong NVRAM)

Nhập lại mật khẩu mới và WR lại: 

R(config)#enable secret cisco

\+ Chuyển về chế độ bình thường:

=>  Khởi động lại Router và nhấn Ctrl + Break

confreg 0x2102

**5. Backup file cấu hình (startup-config) và IOS của Router về một PC đóng vai trò là TFTP Server ( Dùng phần mềm [TFTPD32](http://downloads.phpnuke.org/en/download-item-view-g-b-n-y-g/TFTPD32.htm) để cấu hình cho PC trở thành TFTP Server)**

**+ Restore ngược từ TFTP Server trở lại Router file cấu hình và IOS**

![C:\E8736B25\424F6740-4786-4088-ACB7-F4504922EE98\_files\image001.png](Aspose.Words.e988d113-ff01-4cd1-a9a8-c423c563464f.001.png "image001")

**+ Backup**

**Bước 1 : Đặt 1 địa chỉ IP cho card mạng trên PC đóng vai trò là TFTP Server**

**Bước 2 : Sử dụng cáp chéo đấu nối PC và Router theo sơ đồ trên**

**Bước 3 : Trên Router bật cổng kết nối với PC lên  và gán địa chĩ IP cho cổng đó**

![C:\E8736B25\424F6740-4786-4088-ACB7-F4504922EE98\_files\image002.png](Aspose.Words.e988d113-ff01-4cd1-a9a8-c423c563464f.002.png "image002")

**Bước 4 : Kiểm tra kết nối giữa PC và Router bằng lệnh “ping”**

![C:\E8736B25\424F6740-4786-4088-ACB7-F4504922EE98\_files\image003.png](Aspose.Words.e988d113-ff01-4cd1-a9a8-c423c563464f.003.png "image003")

**Bước 5 : Tiến hành copy file cấu hình (Startup-config) Router sang PC đóng vai trò TFTP Server**

![C:\E8736B25\424F6740-4786-4088-ACB7-F4504922EE98\_files\image004.png](Aspose.Words.e988d113-ff01-4cd1-a9a8-c423c563464f.004.png "image004")

**Bước 6 : Dùng lệnh “show version” trên Router để kiểm tra tên file IOS Router đang sử dụng**

![C:\E8736B25\424F6740-4786-4088-ACB7-F4504922EE98\_files\image005.png](Aspose.Words.e988d113-ff01-4cd1-a9a8-c423c563464f.005.png "image005")

**Bước 7 : Copy file IOS từ Router sang PC đóng vai trò TFTP Server**

![C:\E8736B25\424F6740-4786-4088-ACB7-F4504922EE98\_files\image006.png](Aspose.Words.e988d113-ff01-4cd1-a9a8-c423c563464f.006.png "image006")

**Như vậy là trong PC đóng vai trò TFTP Server bây giờ sẽ có 2 file. Một file là cấu hình (Startup-config) và một file IOS. Sau này, khi Router có sự cố hoặc thay đổi cấu hình cần phục hồi lại trạng thái cũ , ta chỉ cần upload ngược lại 2 file này từ TFTP Server sang Router**

**+ Restore**

**Bước 1 : Upload file cấu hình (startup-config) từ TFTP Server ngược lại Router**

![C:\E8736B25\424F6740-4786-4088-ACB7-F4504922EE98\_files\image007.png](Aspose.Words.e988d113-ff01-4cd1-a9a8-c423c563464f.007.png "image007")

**Bước 2 : Trên Router dùng lệnh “show flash” để kiểm tra nội dung bộ nhớ Flash**

**Bước 3 : Nạp IOS đã lưu trên TFTP Server vào Router sử dụng lệnh *“copy tftp: flash:”* tương tự upload file cấu hình** 

**Lúc này trong bộ nhớ Flash của Router sẽ có 2 file IOS. Ta cần phải khai báo cho Router biết dùng file nào khi khởi động bằng lệnh “boot system flash”**

**Bước 4 : khai báo file IOS cho Router dùng để khởi động**

![C:\E8736B25\424F6740-4786-4088-ACB7-F4504922EE98\_files\image008.png](Aspose.Words.e988d113-ff01-4cd1-a9a8-c423c563464f.008.png "image008")

**Khởi động lại Router để xem kết quả**

**6. Cấu hình Access Server:**

Router#
Router#conf t
Router(config)#hostname access−server
access−server(config)#ip host r1 2001 192.168.5.112
access−server(config)#ip host r2 2002 192.168.5.112
access−server(config)#ip host r3 2003 192.168.5.112
access−server(config)#ip host r4 2004 192.168.5.112
access−server(config)#ip host SW1 2005 192.168.5.112
access−server(config)#ip host SW2 2006 192.168.5.112

access−server(config)#ip host SW3 2007 192.168.5.112

access−server(config)#interface  f0/0
access−server(config−if)#ip address 192.168.5.112 255.255.255.0
access−server(config−if)#exit
access−server(config)#

access−server(config)#line 1 7
access−server(config−line)#transport input all
access−server(config−line)#no exec

**7. Khôi phục mật khẩu cho Catalyst switch 2950, 3550**

**a. Mô tả**

\- Quá trình khôi phục mật khẩu là cần thiết nếu như người admin quên password hay là password đã bị thay thế bởi người dùng khác. Quá trình này đòi hỏi người muốn khôi phục password phải có mặt tại nơi để Switch để bấm vào nút MODE của Switch. Ta thấy khôi phục password của 3550 và 2950 là giống nhau. Vì vậy trong bài viết này chỉ đề cập đến quá trình khôi phục password của 2950 .

**b. Thực hiện**

\1. Ban đầu ta cấu hình password cho switch 2950 .

Switch>enable

Switch#config terminal

Switch(config)#host SW1

SW1(config)#enable password bachkhoa-npower

SW1(config)#copy run start

\2. Bây giờ ta tắt bật switch và sau đó nhấn vào nút “MODE” , sau khi đèn start tắt , chúng ta quay trở lại với màn hình máy tính và xem switch khởi động .

SOFTWARE (fc1)

Compiled Mon 03-Apr-00 17:20 by swati

starting...

Base ethernet MAC Address: 00:02:b9:9a:85:80

Xmodem file system is available.

The system has been interrupted prior to initializing the

flash filesystem. The following commands will initialize

the flash filesystem, and finish loading the operating

system software:

flash\_init

load\_helper

boot

switch:

**switch: flash\_init**

Initializing Flash...

flashfs[0]: 5 files, 1 directories

flashfs[0]: 0 orphaned files, 0 orphaned directories

flashfs[0]: Total bytes: 7741440

flashfs[0]: Bytes used: 4686336

flashfs[0]: Bytes available: 3055104

flashfs[0]: flashfs fsck took 7 seconds.

...done initializing flash.

Boot Sector Filesystem (bs: ) installed, fsid: 3

Parameter Block Filesystem (pb: ) installed, fsid: 4

switch: load\_helper

switch: dir flash:

dir flash:

Directory of flash:/

2 -rwx 3036160 &lt;date> c2950-i6q4l2-mz.121-20.EA1.bin

3 -rwx 1142 &lt;date> config.text

4 -rwx 5 &lt;date> private-config.text

5 -rwx 856 &lt;date> vlan.dat

8 -rwx 1645810 &lt;date> c2900XL-c3h2s-mz-120.5.2-XU.bin

3055104 bytes available (4686336 bytes used)

\3. Bây giờ chúng ta sẽ đổi tập tin config.text thành config.old

switch: rename flash:config.text flash:config.old

\4. Sau đó chúng ta đánh lệnh boot để khởi động lại switch

Switch: boot

Sau khi switch khởi động lại chúng ta sẽ vào priviledge mode và chuyển file config.old thành file config.text để lấy lại cấu hình start-up. Ta tiếp tục copy những cấu hình từ config.text vào running-config.

Switch#copy flash:config.text system:running-config

Destination filename [running-config]? (Press Enter)

648 bytes copied in 1.206 secs (648 bytes/sec)

Bây giờ chúng ta cấu hình lại password mới và lưu lại cấu hình này

SW1(config)#enable password bknpower

SW1(config)#copy run start

Quá trình recovery password đã xong. Chỉ cần reload lại switch, ta có thể vào privilegde vào bằng password mới của mình.

Các đặc điểm Cat 3550

Hệ thống file:

-Các file dạng bin là file của IOS. Nếu bạn muốn sử dụng CLI để quản lý Switch, đây là file bạn cần phải quan tâm. Các file dạng .tar là những file thực thi từ cái mà cả IOS và CMS file được dịch ra trong tiến trình xử lý . Nếu bạn muốn quản lý switch hay là một nhóm các switch thông qua các giao diện web thì đây là các file cần cho bạn. Các file này chứa trong flash hoặc tftp-server. Ta có thể xem bằng lệnh show version .

Bộ nhớ của 3505:

-SDRAM của tất cả các Switch 3550 đều là 64M. Tất cả Switch 3550 đều có 16M flash internal . Phải chú ý những hệ điều hành của mình chép vào . Xem dung lượng flash còn trống bằng lệnh dir flash. Thanh ghi của 3550 không thể thay đổi được. 

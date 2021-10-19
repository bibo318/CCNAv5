
**CÁU HÌNH TỔNG HỢP 1 ĐƯỜNG**

![](Aspose.Words.4c71834a-6273-4c96-a87c-ef488357dd6c.001.png)

**1. Set IP cho 2 PC và Server**

|PC0|Server IP|
| :-: | :-: |
|IP Address: 192.168.1.10|IP Address: 8.8.8.8|
|Subnet Mask:255.255.255.0|Subnet Mask:255.255.255.0|
|Default Getway:192.168.1.1|Default Getway:8.8.8.1|
|DNS Server: 8.8.8.8|DNS Server: 8.8.8.8|
|PC1|Chỉnh DNS On|
|IP Address: 192.168.2.10|Name: google.com|
|Subnet Mask:255.255.255.0|Address: 8.8.8.8|
|Default Getway:192.168.2.1||
|DNS Server: 8.8.8.8||
**2. Set SW0**

**a. Cấu hình cơ bản Switch**

Switch>enable

Switch#configure terminal

Switch(config)#hostname SW0

SW0(config)#line console 0

SW0(config-line)#password dainam

SW0(config-line)#login

SW0(config-line)#exit

SW0(config)#line vty 0 4

SW0(config-line)#password dainam

SW0(config-line)#login

SW0(config-line)#exit

SW0(config)#ban motd "XINCHAO"

SW0(config)#enable secret dainam

SW0(config)#service password-encryption (mã hóa tất cả mật khẩu)

**b. Cấu hình VLAN**

SW0(config)#vlan 10

SW0(config-vlan)#name IT

SW0(config-vlan)#Vlan 20

SW0(config-vlan)#name Sale

SW0(config-vlan)#exit

SW0(config)#interface range f0/1-10

SW0(config-if-range)#switchport access vlan 10

SW0(config-if-range)#exit

SW0(config)#interface range f0/11-20

SW0(config-if-range)#switchport access vlan 20

SW0(config-if-range)#exit

SW0(config)#int g1/1

SW0(config-if)#switchport mode trunk 

SW0(config-if)#end

SW0#wr (lưu lại cấu hình)

**3. Set router R1(Chưa cần đưa cổng WIC-2T)**

**a. cấu hình cơ bản**

Continue with configuration dialog? [yes/no]: n

Router>enable

Router#configure terminal 

Router(config)#hostname R1

R1(config)#line console 0

R1(config-line)#password dainam

R1(config-line)#login

R1(config-line)#exit

R1(config)#line vty 0 4

R1(config-line)#password dainam

R1(config-line)#login

R1(config-line)#exit

R1(config)#banner motd "XINCHAO"

R1(config)#enable secret dainam

R1(config)#service password-encryption (mã hóa tất cả mật khẩu)

**b. Cấu hình Sub interface (cấu hình nhiều IP Gateway trên một cổng)**

R1(config)#int g0/0

R1(config-if)#no shutdown 

R1(config-if)#exit

R1(config)#interface g0/0.10

R1(config-subif)#encapsulation dot1Q 10

R1(config-subif)#ip address 192.168.1.1 255.255.255.0

R1(config-subif)#exit

R1(config)#interface g0/0.20

R1(config-subif)#encapsulation dot1Q 20

R1(config-subif)#ip address 192.168.2.1 255.255.255.0

R1(config-subif)#exit

**c. Cấu hình IP cho cổng bên ngoài**

R1(config)#interface g0/1

R1(config-if)#ip address 10.0.0.1 255.255.255.0

R1(config-if)#no shut

R1(config-if)#exit

**d. Cấu hình định tuyến động (RIPv2)**

R1(config)#router rip 

R1(config-router)#version 2

R1(config-router)#network 10.0.0.0

R1(config-router)#no auto-summary 

R1(config-router)#redistribute connected metric 1

R1(config-router)#end

R1#wr

**4.Cấu hình Router CORE(tắt công tắc đưa cổng WIC-2T vào sau đó bật công tắc lên)**

**a. cấu hình cơ bản**

Router>enable

Router(config)#hostname CORE

CORE(config)#line console 0

CORE(config-line)#password dainam

CORE(config-line)#login

CORE(config-line)#exit

CORE(config)#line vty 0 4

CORE(config-line)#password dainam

CORE(config-line)#login

CORE(config-line)#exit

CORE(config)#banner motd "XIN CHAO"

CORE(config)#enable secret dainam

CORE(config)#service password-encryption (mã hóa tất cả mật khẩu)

**b. cấu hình IP cho các cổng và bật NAT trong cổng**

CORE(config)#int g0/0

CORE(config-if)#no shutdown 

CORE(config-if)#ip address 10.0.0.2 255.255.255.0

CORE(config-if)#ip nat inside

CORE(config-if)#exit

CORE(config)#interface s0/0/0

CORE(config-if)#no shutdown 

CORE(config-if)#ip address 200.0.0.100 255.255.255.0

CORE(config-if)#clock rate 64000

CORE(config-if)#ip nat outside 

CORE(config-if)#exit

**c. Cấu hình đường định tuyến mặc định (Default Root)**

CORE(config)#ip route 0.0.0.0 0.0.0.0 s0/0/0

**d. Cấu hình định tuyến động (sử dụng RIPv2)**

CORE(config)#router rip 

CORE(config-router)#version 2

CORE(config-router)#network 10.0.0.0

CORE(config-router)#no auto-summary 

CORE(config-router)#default-information originate 

CORE(config-router)#exit

**e. Cấu hình Access list và NAT**

CORE(config)#access-list 10 permit any

CORE(config)#ip nat inside source list 10 interface s0/0/0 overload

CORE(config)#end

CORE#wr

**6,Set router ISP(tắt công tắc đưa cổng WIC-2T vào sau đó bật công tắc lên)**

**a. cấu hình cơ bản**

Router>enable

Router#configure terminal 

Router(config)#hostname ISP

ISP(config)#line console 0

ISP(config-line)#password dainam

ISP(config-line)#login

ISP(config-line)#exit

ISP(config)#line vty 0 4

ISP(config-line)#password dainam

ISP(config-line)#login

ISP(config-line)#exit

ISP(config)#banner motd "XIN CHAO"

ISP(config)#enable secret dainam

**b. đặt IP cho các cổng**

ISP(config)#interface g0/0

ISP(config-if)#ip address 8.8.8.1 255.255.255.0

ISP(config-if)#no shutdown 

ISP(config-if)#exit

ISP(config)#interface s0/0/0

ISP(config-if)#no shutdown 

ISP(config-if)#ip address 200.0.0.1 255.255.255.0

ISP(config-if)#end

ISP#wr

**7. Kiểm tra sau khi cấu hình (như hình là đường mạng đã thông)**

![](Aspose.Words.4c71834a-6273-4c96-a87c-ef488357dd6c.002.png)

Chú ý: 

- Dùng lệnh Show vlan để kiểm tra VLAN trên Switch
- Dùng lệnh Show run để xem những cấu hình sai trên cả Switch và Router

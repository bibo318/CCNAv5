![](Aspose.Words.f05a6889-1055-4331-b887-d5743f158b48.001.png)

**1. Set Ip cho 2 PC và Server:**

|**PC0**|**Server IP**|
| :-: | :-: |
|IP Address: 2000::A|IP Address: 2008::8|
|Subnet Mask:96|Subnet Mask:96|
|Default Getway:2000::1|Default Getway: 2008::1|
|DNS Server: 2008::8|DNS Server: 2008::8|
|**PC1**|Chỉnh DNS On|
|IP Address: 2001::B|Resource RecodeName: google.com|
|Subnet Mask:96|Address: 2008::8|
|Default Getway:2001::1|Chọn Add|
|DNS Server: 2008::8||
**2,Set SW0:**

**a. Cấu hình cơ bản Switch**

Switch>enable

Switch#configure terminal

Switch(config)#hostname (SW0) TenSwiches

SW0(config)#line console 0

SW0(config-line)#password hanu

SW0(config-line)#login

SW0(config-line)#exit

SW0(config)#line vty 0 4

SW0(config-line)#password hanu

SW0(config-line)#login

SW0(config-line)#exit

SW0(config)#ban motd "XINCHAO"

SW0(config)#enable secret hanu

**b. Cấu hình VLAN**

SW0(config)#vlan 10

SW0(config-vlan)#name IT

SW0(config-vlan)#Vlan 20

SW0(config-vlan)#name Sale

SW0(config-vlan)#exit

SW0(config)#interface range f0/1-10

SW0(config-if-range)#switchport access vlan 10

SW0(config)#interface range f0/11-20

SW0(config-if-range)#switchport access vlan 20

SW0(config-if-range)#exit

SW0(config)#int f1/1

SW0(config-if)#switchport mode trunk 

SW0(config-if)#end

SW0#wr (lưu lại cấu hình)

**3.Set router R1(Chưa cần đưa cổng WIC-2T)**

**a. cấu hình cơ bản**

Continue with configuration dialog? [yes/no]: n

Router>enable

Router#configure terminal 

Router(config)#hostname R1

R1(config)#line console 0

R1(config-line)#password hanu

R1(config-line)#login

R1(config-line)#exit

R1(config)#line vty 0 4

R1(config-line)#password hanu

R1(config-line)#login

R1(config-line)#exit

R1(config)#banner motd "XINCHAO"

R1(config)#enable secret hanu

**b. Cấu hình Sub interface (nhiều IP gateway trên một cổng)**

R1(config)#**ipv6 unicast-routing**

R1(config)#int f0/0

R1(config-if)#no shutdown 

R1(config-if)#exit

R1(config)#interface f0/0.10

R1(config-subif)#encapsulation dot1Q 10

R1(config-subif)#ip address 2000::1/96

R1(config-subif)#exit

R1(config)#interface f0/0.20

R1(config-subif)#encapsulation dot1Q 20

R1(config-subif)#ip address 2001::1/96

R1(config-subif)#exit

**c. Cấu hình định tuyến động (RIPng)**

R1(config)#ipv6 router rip R1

R1(config-rtr)#redistribute connected metric 1

R1(config-router)#end

R1#wr

**d. Cấu hình IP cho cổng bên ngoài**

R1(config)#interface f0/1

R1(config-if)#ip address 2002::1/96

R1(config-if)# ipv6 rip R1 enable

R1(config-if)#no shut

R1(config-if)#exit

**4.Cấu hình Router CORE**

**a. cấu hình cơ bản**

Continue with configuration dialog? [yes/no]: n

Router>enable

Router(config)#hostname CORE

CORE(config)#line console 0

CORE(config-line)#password hanu

CORE(config-line)#login

CORE(config-line)#exit

CORE(config)#line vty 0 4

CORE(config-line)#password hanu

CORE(config-line)#login

CORE(config-line)#exit

CORE(config)#banner motd "XIN CHAO"

CORE(config)#enable secret hanu

CORE(config)#**ipv6 unicast-routing**

**b. Cấu hình định tuyến động (RIPng)**

CORE (config)#ipv6 router rip CORE

CORE (config-router)#exit

CORE #wr

**c. cấu hình IP cho các cổng** 

CORE(config)#int f0/0

CORE(config-if)#no shutdown 

CORE(config-if)#ipv6 address 2002::2/96

CORE(config-if)#ipv6 rip CORE enable 

CORE(config-if)# ipv6 rip CORE default-information originate

CORE(config-if)#exit

CORE(config)#interface f0/1

CORE(config-if)#no shutdown 

CORE(config-if)#ipv6 address 2006::A/96

CORE(config-if)#exit

**d. Cấu hình đường định tuyến mặc định (Default Root)**

CORE(config)#ipv6 route ::/0 2006::1

**6,Set router ISP**

**a. cấu hình cơ bản**

Continue with configuration dialog? [yes/no]: n

Router>enable

Router#configure terminal 

Router(config)#hostname ISP

ISP(config)#line console 0

ISP(config-line)#password hanu

ISP(config-line)#login

ISP(config-line)#exit

ISP(config)#line vty 0 4

ISP(config-line)#password hanu

ISP(config-line)#login

ISP(config-line)#exit

ISP(config)#banner motd "XIN CHAO"

ISP(config)#enable secret hanu

**ISP(config)# ipv6 unicast-routing**

**b. đặt IP cho các cổng**

ISP(config)#interface f0/0

ISP(config-if)#ipv6 address 2006::1/96

ISP(config-if)#no shutdown 

ISP(config-if)#exit

ISP(config)#interface f0/1

ISP(config-if)#no shutdown 

ISP(config-if)# ipv6 address 2008::1/96

ISP(config-if)#exit

**c. Cấu hình đường định tuyến tĩnh**

ISP(config)#ipv6 route 2000::/96 2006::A

ISP(config)#ipv6 route 2001::/96 2006::A

ISP(config)#end

ISP#wr

- Dùng lệnh Show vlan để kiểm tra vlan trên Switch
- Dùng lệnh Show run để xem những cấu hình sai

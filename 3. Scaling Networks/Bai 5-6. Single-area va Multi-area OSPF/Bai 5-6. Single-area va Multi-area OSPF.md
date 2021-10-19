**Single-area và Multi-area OSPF**

**I. Nội dung chính**

\1. Cấu hình Single-area OSPF

\2. Cấu hình Multi-area OSPF

` `**II. Nội dung chi tiết**

**1. Cấu hình Single-area OSPF**

**a. Chạy OSPF**

\- R(config)# Router  OSPF  Process-id (1-65535) chỉ có ý nghĩa nội bộ. 

\- R(config-Router)# network 192.168.1.0  0.0.0.31  area  0  (Areal là cùng mạng thành phần này rất quan trọng)

\- R(config-Router)#default-information originate 

\- Router(config-router)#redistribute connected [metric cost] subnet.

**b. Hiệu chỉnh OSPF**

\- Router - ID: 

=> R(config)# Router  OSPF  10

=> R(config-router)# router-id  a.b.c.d (nhập ip vào, IP chính là ID)

=> Sau đó trở ra mode quản trị:

=> R(config)#  Clear ip ospf  process  thì nó mới có hiệu lực

\- Priority:

=> R(config)# int f0/0

=> R(config-if)# ip  ospf  priority 

\- Hello/Dead time:

=> R(config-if)# ip  ospf  hello-interval  thời gian (là giây)

=> R(config-if)# ip  ospf  dead-interval  thời gian (là giây) 

**c. Xác thực trên 2 router**

Vào trong cổng:

=> R(config-if)# ip   ospf   authentiacation  [MD5]

Nếu điền key:

=> R(config-if)# ip   ospf   authentiacation-key   aptech

**d. Các lệnh Show**

=> Show  ip  router  ospf

=> Show  ip  ospf  neighbor

=> Show  ip  ospf  database

=> Show  ip  ospf  interface

=> Show  ip  protocol 

**2. Cấu hình Multi-area OSPF**

**a. cấu hình Multi-area**

\- Router(config)#router ospf 5

\- Router(config-router)#redistribute ospf 10 [metric cost] subnet

**b. Redistribute vào OSPF**

**- RIP => OSPF:**

\+ Router(config)#router ospf process-id

\+ Router(config-router)#redistribute rip [metric cost] subnet.

**- EIGRP-OSPF:**

\+ Router(config-router)#redistribute eigrp as-number [metric cost] subnet.

**- Static route & Default route => OSPF:**

\+ Router(config-router)#redistribute static [metric cost] subnet.

**- Connected route => EIGRP:** 

\+ Router(config-router)#redistribute connected [metric cost] subnet.

**- Default route => OSPF:**

\+ Router(config-router)#default-information originate.

\+ Nếu chúng ta không đưa vào tham số metric thì mặc định metric sẽ được đặt cho tuyến được redistribute vào là 20.

**3. Chú ý:**  dùng lệnh Show  ip  router:

10.0.0.0/24 is subnetted, 1 subnets

O E2 10.0.0.0 [110/20] via 192.168.1.20, 00:00:53, Serial0/1/0 => tương ứng #redistribute connected [metric cost] subnet.

C 192.168.1.0/24 is directly connected, Serial0/1/0

C 192.168.2.0/24 is directly connected, FastEthernet0/0

O 192.168.3.0/24 [110/65] via 192.168.1.20, 00:00:53, Serial0/1/0

O\*E2 0.0.0.0/0 [110/1] via 192.168.1.20, 00:00:11, Serial0/1/0  => tương ứng: #default-information originate 

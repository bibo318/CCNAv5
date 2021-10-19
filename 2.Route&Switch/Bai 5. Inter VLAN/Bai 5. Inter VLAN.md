Giới thiệu về Inter-VLAN

**I. Nội dung chính:**

\1. giới thiệu về Inter-VLAN

\2. Cấu hình Inter-VLAN

**II. Nội dung chi tiết:**

**1. giới thiệu về Inter-VLAN**

\- Mỗi mạng có nhu cầu riêng của nó, tuy nhiên cho dù đó là một mạng lưới rộng lớn hay nhỏ, định tuyến nội bộ, trong hầu hết các trường hợp, là điều cần thiết. Khả năng để phân chia mạng bằng cách tạo ra VLANs, do đó giảm broadcasts mạng và tính bảo mật ngày càng tăng. Các thiết lập phổ biến bao gồm một broadcast domain riêng biệt cho các dịch vụ quan trọng ngày càng nhiều. 

\- Vấn đề ở đây là làm thế nào có thể từ một trong những người sử dụng VLAN ( thuộc về 1 broadcast domain), sử dụng được các dịch vụ được cung cấp bởi một VLAN khác? Do vậy giải pháp định tuyến trên VLAN đã được đề cập đến.
\- Inter-VLAN là phương pháp được thiết lập có hiệu quả nhất bằng cách cung cấp một liên kết trunk duy nhất giữa Switch và Router mà có thể mang lưu lượng truy cập của nhiều VLAN và trong đó các lưu lượng ấy lần lượt có thể được định tuyến bởi Router.
\- Với Inter-VLAN Routing, Router nhận frame từ Switch với gói tin xuất phát từ một VLAN đã được tag. Nó liên kết các frame với các subinterface thích hợp và sau đó giải mã nội dung của frame (phần IP packet). Router sau đó thực hiện chức năng của Layer 3 dựa trên địa chỉ mạng đích có trong gói tin IP để xác định subinterface cần chuyển tiếp gói IP. Các IP packet bây giờ được đóng gói thành frame theo chuẩn dot1Q (hoặc ISL) để nhận dạng VLAN của subinterface chuyển tiếp và truyền đi trên đường trunk vào Switch.

**2. Cấu hình Inter-VLAN**

**a. Trên Switch**

=>SW0(config)#vlan 10

=>SW0(config-vlan)#name IT

=>SW0(config-vlan)#vlan 20

=>SW0(config-vlan)#name sale

=>SW0(config-vlan)#exit

=>SW0(config)#interface range f0/1-10

=>SW0(config-if-range)#switchport access vlan 10

=>SW0(config-if-range)#exit

=>SW0(config)#interface range f0/11-20

=>SW0(config-if-range)#switchport access vlan 20

=>SW0(config-if-range)#exit

=>SW0(config)#interface range g1/1-2

=>SW0(config-if-range)#switchport mode trunk

=>SW0(config)#interface vlan 1

=>SW0(config)#no shutdown

=>SW0(config-if)#ip add 10.0.0.101 255.255.255.0

=>SW0(config-if)#end

=>SW0#write

**b. Cấu hình định tuyến VLAN trên Router**

=> R1(config)#int f0/0

=> R1(config-if)#no shut

=> R1(config)#int f0/0.10

=> R1(config-subif)#encapsulation dot1Q 10

=> R1(config-subif)#ip add 192.168.1.1 255.255.255.0

=> R1(config-subif)#exit

=> R1(config)#int f0/0.20

=> R1(config-subif)#encapsulation dot1Q 20

=> R1(config-subif)#ip add 192.168.2.1 255.255.255.0

=> R1(config-subif)#exit

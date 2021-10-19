**Tổng quan về định tuyến**

**I. Nội dung chính**

\1. giới thiệu về định tuyến

\2. Sơ đồ tổng quan về định tuyến

\3. Giới thiệu về định tuyến tĩnh và định tuyến động

**II. Nội dung chi tiết**

**1. giới thiệu về định tuyến**

\- Trong ngành mạng máy tính, định tuyến (tiếng Anh: routing) là quá trình chọn lựa các đường đi trên một mạng máy tính để gửi dữ liệu qua đó. Việc định tuyến được thực hiện cho nhiều loại mạng, trong đó có mạng điện thoại, liên mạng, Internet, mạng giao thông.

**-** Routing chỉ ra hướng, sự di chuyển của các gói (dữ liệu) được đánh địa chỉ từ mạng nguồn của chúng, hướng đến đích cuối thông qua các node trung gian; thiết bị phần cứng chuyên dùng được gọi là router (bộ định tuyến). Tiến trình định tuyến thường chỉ hướng đi dựa vào bảng định tuyến, đó là bảng chứa những lộ trình tốt nhất đến các đích khác nhau trên mạng. Vì vậy việc xây dựng bảng định tuyến, được tổ chức trong bộ nhớ của router, trở nên vô cùng quan trọng cho việc định tuyến hiệu quả.

\- Routing khác với bridging (bắc cầu) ở chỗ trong nhiệm vụ của nó thì các cấu trúc địa chỉ gợi nên sự gần gũi của các địa chỉ tương tự trong mạng, qua đó cho phép nhập liệu một bảng định tuyến đơn để mô tả lộ trình đến một nhóm các địa chỉ. Vì thế, routing làm việc tốt hơn bridging trong những mạng lớn, và nó trở thành dạng chiếm ưu thế của việc tìm đường trên mạng Internet.

**2. Sơ đồ tổng quan về định tuyến**

![Hinh-1-Tong-quan-ve-cac-giao-thuc-dinh-tuyen](http://www.ntps.edu.vn/images/blog/Hinh-1-Tong-quan-ve-cac-giao-thuc-dinh-tuyen.jpg "Hinh-1-Tong-quan-ve-cac-giao-thuc-dinh-tuyen")

**3. Giới thiệu về định tuyến tĩnh (static route) và định tuyến động** (dynamic route)

**a. Giới thiệu về định tuyến tĩnh**

\- Static route là kỹ thuật mà người quản trị phải tự tay khai báo các route trên các router. Kỹ thuật này đơn giản, dễ thực hiện, ít hao tốn tài nguyên mạng và CPU xử lý trên router (do không phải trao đổi thông tin định tuyến và không phải tính toán định tuyến). Tuy nhiên kỹ thuật này không hội tụ với các thay đổi diễn ra trên mạng và không thích hợp với những mạng có quy mô lớn (khi đó số lượng route quá lớn, không thể khai báo tay được) .

**b. Giới thiệu về định tuyến động**

\- Với dynamic route, các router sẽ trao đổi thông tin định tuyến với nhau. Từ thông tin nhận được, mỗi router sẽ thực hiện tính toán định tuyến từ đó xây dựng bảng định tuyến gồm các đường đi tối ưu nhất đến mọi điểm trong hệ thống mạng. Với Dynamic route, các router phải chạy các giao thức định tuyến (routing protocol).

\- Dynamic route lại tiếp tục chia thành hai trường phái: các giao thức định tuyến ngoài – Exterior Gateway Protocol (EGP) và các giao thức định tuyến trong - Interior Gateway Protocol (IGP).

\+ Các giao thức định tuyến ngoài (EGP) với giao thức tiêu biểu là BGP (Border Gateway Protocol) là loại giao thức được dùng để chạy giữa các router thuộc các AS khác nhau, phục vụ cho việc trao đổi thông tin định tuyến giữa các AS. AS – Autonomous System – tạm dịch là *Hệ tự trị* là tập hợp các router thuộc cùng một sự quản lý về kỹ thuật và sở hữu của một doanh nghiệp nào đó, cùng chịu chung một chính sách về định tuyến. Các AS thường là các ISP. Như vậy định tuyến ngoài thường được dùng cho mạng Internet toàn cầu, trao đổi số lượng thông tin định tuyến rất lớn giữa các ISP với nhau và hình thức định tuyến mang nặng hình thức chính sách (policy).

\- Các giao thức định tuyến trong (IGP) gồm các giao thức tiêu biểu như RIP, OSPF, EIGRP. Trong đó, RIP và OSPF là các giao thức chuẩn quốc tế, cong EIGRP là giao thức của Cisco, chỉ chạy trên thiết bị Cisco. IGP là loại giao thức định tuyến chạy giữa các router nằm bên trong một AS. Cả ba giao thức IGP mới kể trên đều được giới thiệu trong chương trình CCNA.



![Hinh-2-IGP-va-EGP](http://www.ntps.edu.vn/images/blog/Hinh-2-IGP-va-EGP.jpg "Hinh-2-IGP-va-EGP")

Với các IGP, chúng lại tiếp tục được chia thành nhiều nhánh khác nhau:

\- Nếu chia ba, các giao thức IGP có tổng cộng 03 loại: Distance – vector, Link – state và Hybrid.

\+ Distance – vector: mỗi router sẽ gửi cho láng giềng của nó toàn bộ bảng định tuyến theo định kỳ. Giao thức tiêu biểu của hình thức này là giao thức RIP. Đặc thù của loại hình định tuyến này là có khả năng bị loop nên cần một bộ các quy tắc chống loop khá phong phú. Các quy tắc chống loop có thể làm chậm tốc độ hội tụ của giao thức.

\+ Link – state: với loại giao thức này, môi router sẽ gửi bảng *cơ sở dữ liệu trạng thái đường link* (LSDB – Link State Database) cho mọi router cùng vùng (area). Việc tính toán định tuyến được thực hiện bằng giải thuật Dijkstra.

\+ Hybrid: tiêu biểu là giao thức EIGRP của Cisco. Loại giao thức này kết hợp các đặc điểm của hai loại trên. Tuy nhiên, thực chất thì EIGRP vẫn là giao thức loại Distance – vector nhưng đã được cải tiến thêm để tăng tốc độ hội tụ và quy mô hoạt động nên còn được gọi là Advanced distance vector.

\- Nếu chia hai, ta có thể chia các giao thức IGP thành hai loại:

\+ Các giao thức classful: router sẽ không gửi kèm theo subnet – mask trong bản tin định tuyến của mình. Từ đó các giao thức classful không hỗ trợ các sơ đồ VLSM và mạng gián đoạn (discontiguos network). Giao thức tiêu biểu là RIPv1 (trước đây còn có thêm cả IGRP nhưng hiện giờ giao thức này đã được gỡ bỏ trên các IOS mới của Cisco).

\+ Các giao thức classless: ngược với classful, router có gửi kèm theo subnet – mask trong bản tin định tuyến. Từ đó các giao thức classless có hỗ trợ các sơ đồ VLSM và mạng gián đoạn (discontiguos network). Các giao thức classless: RIPv2, OSPF, EIGRP.

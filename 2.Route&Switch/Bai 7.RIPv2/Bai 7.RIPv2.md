Giao thức định tuyến RIP phiên bản 2

**1. Đặc điểm:** Để tiếp cận RIPv2 một cách nhanh chóng và đầy đủ, những phần trong chương này sẽ đề cập tới sự khác nhau giữa RIPv1 và RIPv2:

|Đặc điểm|Mô tả|
| :- | :- |
|Dịch vụ tầng vận chuyển|Giao thức UDP, cổng 20|
|Chi phí|Số chặng tối đa là 15 Router, 16 Router được xem là vô cùng|
|Thời gian định kỳ gửi thông điệp Hello|Không sử dụng, RIP gửi định kỳ bảng định tuyến|
|Gửi cập nhật đến địa chỉ đích|Sử dụng địa chỉ Broadcast nội bộ (255.255.255.255) đối với RIPv1, RIPv2 sử dụng multicast là 224.0.0.9|
|Thời gian định kỳ gửi cập nhật|30s|
|Cập nhật đầy đủ hoặc không đầy đủ|Gửi toàn bộ bảng định tuyến sau thời gian cập nhật|
|Sử dụng cập nhật ngay lập tức|Sử dụng cập nhật ngay có sự thay đổi|
|Sử dụng nhiều đường đi tới cùng mạng con|Cho phép sử dụng từ 1 tới 6 tuyến có chi phí bằng nhau tới mạng con, mặc định là 4 tuyến|
|Xác thực\* (RIPv2)|Sử dụng chuổi ký tự không mã hóa hoặc MD5|
|Gửi mặt nạ mạng con trong cập nhật (RIPv2)|RIPv2 gửi Subnetmask theo từng tuyến, hỗ trợ VLSM và định tuyến không đúng lớp. Do đó RIPv2 có thể thực thi cho mô hình mạng không liên tục|
|Mặt nạ mạng có chiều dài thay đổi (VLSM)|RIPv2 gửi cập nhật kèm theo mặt nạ mạng con có chiều dài khác nhau ứng với mỗi mạng con|
|Thêm tuyến\* (RIPv2)|Cho phép thêm những tuyến khác vào bảng định tuyến bằng phân phối lại chúng vào RIP|
|Trường chặng kế tiếp|Xác định IP của cặng kế tiếp cho mỗi tuyến, Router quảng bá những tuyến trong bảng định tuyến của nó đi với địa chỉ chặng kế tiếp chính là địa chỉ IP của Router.|
=> Router chạy RIP gửi thông tin về tuyến đường trong các cập nhật RIP qua mỗi giao tiếp trong mỗi khoảng thời gian cập nhật. Một Router chạy RIP quảng bá những tuyến đường kết nối trực tiếp với nó, và những Router chạy RIP khác nhận quảng bá và cập nhật vào bảng định tuyến của mình. Chú ý rằng RIP không cất giữ bảng sơ đồ (topology) riêng biệt. Những Router chạy RIP không thiết lập quan hệ láng giềng, cũng không gửi thông điệp hello - mỗi router chỉ đơn giản là gửi cập nhật với địa chỉ đích là 224.0.0.9 với RIPv2 và 255.255.255.255 với RIPv1

=> RIPv2 và RIPv1 đều sử dụng số chặng làm chi phí, chi phí tối đa là 15, với chi phí bằng 16 được xem là vô cùng (infinity) và tuyến không thể đến được. Một Router chạy RIP không đặt chi phí của nó vào tuyến khi gửi cập nhật. Thay vào đó Router chạy RIP sẽ tăng chi phí lên một khi xây dựng gói tin cập nhật. Ví dụ: nếu Router A có một tuyến chi phí bằng 2, nó sẽ quảng bá tuyến đó đi với chi phí bằng 3.

=> Khi một Router chạy RIP học được nhiều tuyến đến cùng một mạng con thì tuyến có chi phí thấp nhất sẽ được chọn. Nếu như có nhiều tuyến có chi phí bằng nhau và nhỏ nhất, Router mặc định sẽ cập nhật 4 tuyến vào bảng định tuyến. Router cũng có thể cho phép cập nhật từ 1 tới 6 tuyến vào bảng định tuyến bằng cách sử dụng câu lệnh *ip maximum-paths  number*  trong chế độ Router RIP

**2. Hội tụ và chống vòng lặp:**

Phần quan trọng nhất và cũng phức tạp nhất của RIP nằm ở những phương thức chống vòng lặp. Giống như những giao thức định tuyến Distance vector, RIP sử dụng kết hợp những công cụ chống vòng lặp khác nhau, nhưng đáng tiếc rằng những công cụ này cũng làm tăng thời gian hội tụ (convergence) một cách đáng kể. Sự thật đó là một hạn chế rất lớn của RIP (kể cả RIPv2). Bảng sau đây sẽ tổng hợp những tính năng và phương thức liên quan đến hội tụ và chống vòng lặp của RIP

|Tính năng|Mô tả|
| :- | :- |
|Split Horizon|Thay vì quảng bá tất cả các tuyến ra một giao tiếp, RIP không quảng bá những tuyến mà Route học được từ giao tiếp này.|
|<p>Triggered</p><p>Update</p>|<p>Route sẽ gửi một cập nhật mới ngay khi thông tin định tuyến bị thay đổi, thay vì phải chờ hết thời gian gửi cập nhật. Trigger update còn có tên gọi khác là Flash update. Khi một giá trị chi phí thay đổi tốt hơn hoặc kém hơn, router ngay lập tức sẽ gửi một thông điệp cập nhật mà không cần chờ vào khoảng thời gian gửi cập nhật bị hết. Quá trình tái hội tụ diễn ra nhanh hơn so với trường hợp phải chờ những khoảng thời gian cập nhật định kỳ. Các thông điệp cập nhật định kỳ vẫn diễn ra cùng với các thông điệp Triggerup date. Như vậy một Router có thể nhận một thông tin kém về một tuyến từ một Router chưa hội tụ sau khi đã nhận một thông tin chính xác từ Trigger Update. Tình huống này xẩy ra dẫn đến các lỗi định tuyến vẫn có thể xẩy ra trong quá trình hội tụ.</p><p>Một sự hiệu chỉnh xa hơn nữa là trong thông điệp cập nhật, chỉ bao gồm các địa chỉ mạng làm cho việc kích hoạt xẩy ra. Kỹ thuật này làm giảm thời gian xử lý và giảm thời gian ảnh hưởng tới băng thông.</p>|
|Router poisoning|Khi tuyến bị lỗi, router sẽ gửi cập nhật nhật về định tuyến đó đi với giá trị chi phí là vô hạn (số chặng là 16)|
|Poison Reverse|Router nhận được quảng bá về một tuyến bị sự cố (chi phí là 16) trên một giao tiếp, router sẽ hồi đáp lại lại thông điệp poison reverse trên cùng giao tiếp đó. Thực chất đây là sự kết hợp của Split horizon và router poisoning. Trong điều kiện không nhận được quảng bá về một tuyến bị sự cố thì tính năng Split horizon được bật.|
|Update timer|Qua mỗi khoảng thời gian cập nhật định tuyến, router sẽ gửi cập nhật một lần qua một giao tiếp, mỗi giao tiếp có một khoảng thời gian cập nhật riêng, mặc định trên tất cả giao tiếp là 30s.|
|Holddown timer|<p>Đối với mỗi tuyến đến một mạng con trong bảng định tuyến, nếu như chi phí của tuyến thay đổi đến một giá trị lớn hơn, thời gian holddown timer sẽ bắt đầu. Trong khoảng thời gian này (mặc định là 180s) router sẽ không cập nhật định tuyến nào khác đến mạng con đó trong bảng định tuyến cho tới khi thời gian holddown timer kết thúc.</p><p>Trigger update sẽ là tăng khả năng đáp ứng một hệ thống mạng đang hội tụ. Holddown timers sẽ giúp kiểm soát các thông tin định tuyến xấu.</p><p>Nếu khoảng cách đến một mạng đích tăng (ví dụ: số chặng tăng từ 2 đến 4 router sẽ gán một giá trị thời gian cho tuyến đó. Cho tới khi nào thời gian hết hạn router sẽ không chấp nhận bất kỳ cập nhật nào cho tuyến đó.</p><p>Rõ ràng có một sự đánh đổi ở đây. Khả năng các thông tin định tuyến kém bị đưa vào bảng định tuyến là giảm nhưng bù lại thời gian hội tụ tăng lên. Nếu thời gian holddown là quá ngắn, nó sẽ không hiệu quả. Nếu khoảng thời gian là quá dài, quá trình định tuyến thông thường sẽ bị ảnh hưởng.</p>|
|Invalid timer|Đối với mỗi tuyến tồn tại trong bảng định tuyến, thời gian invalid timer sẽ tăng cho đến khi router nhận được đập nhật thông báo về các tuyến đó. Nếu nhận được cập nhật, thời gian invalid timer sẽ được chuyển về 0. Nếu như router không nhận được cập nhật, mà thời gian invalid timer đã hết (mặc định là 180s) tuyến đó được xem là không dùng được.|
|Flush (Garbage timer)|Thời gian flush timer mặc định là 240s, cũng giống như thời gian invalid timer, tuy nhiên thời gian flush timer mặc định sẽ tăng thêm 60s nữa, trong thời gian này Router sẽ gửi cho Router các Router khác nhằm báo rằng tuyến dó hiện tịa không thể truy cập được, nếu không nhận được bất cứ cập nhật về tuyến, Router sẽ loại tuyến đó khỏi bảng định tuyến.|




![C:\B17D46A5\646D2803-BA02-4773-B435-7F56CA176904\_files\image001.png](Aspose.Words.9ac62f67-70f5-4ad5-b2db-16b2af954823.001.png "image001")



***Khoảng thời gian Invalid**:* 

=> Nếu mạng 10.1.5.0 bị mất, Router R4 sẽ đánh dấu tuyến này như là không đến (unreachable) và truyền thông tin cho các Rouer khác. Nhưng nếu trong trường hợp chính Router R4 bị chết, Router R1,R2,R3 vẫn còn lưu giữ thông tin về mạng 10.1.5.0 trong bảng định tuyến. Thông tin về tuyến không còn hợp lệ nhưng không có Router nào thông báo cho R1,R2,R3 biết về việc này. Kết quả là R1,R2,R3 sẽ đẩy các gói tin đi về các địa chỉ mạng đích không còn tồn tại, mạng bị hiện tượng lỗ đen.

=> Vấn đề có thể giải quyết được bằng cách thiết lập một thông số gọi là khoảng thời gian không phù hợp (invalidation timer) cho từng hàng trong bảng định tuyến. Ví dụ: khi Router R3 nghe về mạng 10.1.5.0 lần đầu tiên và nhập thông tin vào bảng định tuyến. R3 sẽ thiết lập một đồng hồ cho tuyến đó. Ở mỗi chu kỳ cập nhật nhận được từ R4 thì R3 sẽ bỏ qua những cập nhật đã biết và khởi động lại thời gian tuyến đó. Nếu Router R4 bị chết thì R3 không còn nghe về mạng 10.1.5.0. Thời gian Invalid sẽ bị hết, C đánh giấu tuyến như không đến được và truyền thông tin này trong cập nhật kế tiếp.

=> Thời gian cho tuyến hết hạn thường là từ 3 cho tới 6 chu kỳ cập nhật. Một Router không muốn xem một tuyến là không hợp lệ chỉ sau một chu kỳ cập nhật bị mất vì điều này sẽ làm cho gói tin bị mất hay tăng độ trễ của mạng. Ngược lại, nếu thời gian là quá dài, quá trình hội tụ mạng sẽ rất chậm.

***Split horizon:***

Giả sử rằng mạng 10.1.5.0 bị sự cố, Router R4 sẽ phát hiện, đánh dấu tuyến này là không đến được và truyền thông tin đến R3 ở chu kỳ cập nhật kế tiếp. Tuy nhiên trước khi R4 kích hoạt một cập nhật, có một vấn đề xẩy ra. Cập nhật của R3 đến thông báo là nó có thể đến được mạng 10.1.5.0, chỉ cách R3 một chặng. R4 không có cách nào nhận ra R3 quảng bá sai. R4 sẽ tăng giá trị số chặng và đưa vào bảng định tuyến thông tin là mạng 10.1.5.0 có thể đến được thông qua R3 cách đó 2 chặng. 

=> Bây giờ có một gói tin có địa chỉ đích là 10.1.5.3 đến Router R3. R3 tra bảng định tuyến của nó và đẩy gói tin về R4. R4 tra bảng định tuyến và đẩy về R3. Một vòng lặp xẩy ra. 

=> Tính năng Split horizon sẽ ngăn ngừa khả năng vòng lặp xuất hiện. Có 2 nhóm Split horizon gồm Split horizon đơn giản và Split horizon kết hợp với Poison reverse.

=> Nguyên tắc cho Split horizon đơn giản là khi gửi một cập nhật ra một cổng, không được chứa những địa chỉ mạng được học trên chính cổng đó.

=> Các Router thực hiện tính năng Split horizon đơn giản. R3 sẽ gửi một cập nhật cho R4 về địa chỉ mạng 10.1.1.0 và 10.1.2.0, 10.1.3.0. Các mạng 10.1.4.0 không gửi vì nó là connected và 10.1.5.0 là từ R4. Tương tự gửi cập nhật tới R2 bao gồm địa chỉ 10.1.4.0, 10.1.5.0 và không có 10.1.1.0 và 10.1.2.0, 10.1.3.0. 

=> Luật Split horizon với poison reverse là một cải tiến, 





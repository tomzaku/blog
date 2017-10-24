---
title: Hiểu rõ nguyên nhân và phòng chống các thủ thuật tấn công wireless
thumbnail: https://camo.githubusercontent.com/527bf73d81ccb73d4f02899da1958f821a5c170a/68747470733a2f2f736f7068726f6e2e6769746875622e696f2f77696669706869736865722f6469616772616d2e6a7067
tags: CIH
---
![Introduce](https://camo.githubusercontent.com/527bf73d81ccb73d4f02899da1958f821a5c170a/68747470733a2f2f736f7068726f6e2e6769746875622e696f2f77696669706869736865722f6469616772616d2e6a7067)
# Nguyên nhân lập topic
-> Nhầm chia sẽ những thứ mình hiểu và nằm rõ trong quá trình vọc vạch.
-> Lưu trữ lại các quá trình, sau này có thể đọc lại.
# Các câu hỏi đặt ra
Nếu bạn đã trả lời hết những câu hỏi dưới đây. Bạn cũng không cần phải đọc topic mình đâu.
1.  Rogue AP là gì? Vì sao phải cần nó?
2.  Cơ chế ngắt mạng victim ra sao? Vì sao người ngoài ( người không cần kết nối wifi nhà bạn ) có thể phá network nhà bạn?
3.  Một ngày đẹp trời bạn thấy một cái AP( wifi thường gọi, nhưng không phải nhé ) giống mình, Vì sao thế?
4.  Pass facebook/gmail/.... bị mất? Nguyên nhân?
5.  Khắc phục những lỗi trên ra sao? Bạn có chắc đang dùng 1 network an toàn?
# Các khái niệm cơ bản trước khi trả lời câu hỏi
Các khái niệm mình được rút gọn, và được định nghĩa theo phong cách mình. Nếu các bạn chưa hiểu rõ có thể bình luận phía dưới nhà.

### 1. AP là gì? Station là gì?
  **a. AP (Access Point)**
  ![Access Point](https://support.zen.co.uk/kb/uploads/Images/Network/Windows7/Wireless/select_network.jpg)
  Như hình bạn có thể thấy có 5 AP Thomson....,Uhomsom...., ....

  AP như là cái `card wireless` có hổ trợ `phát wireless`.
  Điện thoại có hổ trợ phát Wifi => Nó là AP
  Laptop phát Wifi => Nó là AP
  Usb Wireless => Nó là AP
  **b. Station: Máy trạm**
  ![Station](/images/Station.png)
  Chúng ta đã hiểu AP là máy phát. Vậy AP cần các máy thu để trao đổi dữ liệu.
  Máy thu có thể hiểu là station.
  Vậy Station là các kết nối tới AP.

  Tóm lại: AP phát, Station thu.
### 2. Kênh (Channel) là gì?
  Các trạm liên kết với nhau sử dụng tần số vô tuyến (RF) giữa 2.4 - 2.5GHz.
  2 Mạng dây cùng chung các **kênh lân cận có thể can thiệp với nhau**

  >Nếu bạn muốn cải thiện Wifi nhà bạn, hãy chọn channel khác với các channel xung quanh nhà bạn



### 3. Bạn có tự hỏi khi chúng ta bật wifi từ thiết bị, Chúng ta thấy tất cả các Wi-Fi xung quanh? Và có những WiFi nội bộ bạn không thấy được, tại sao vậy?

  Trả lời câu hỏi này bạn phải biết Beacon Frame là gì?
  AP phát ra dựa vào sóng RF( Radio Frequency) hay bạn thường gọi là sóng radio đấy. Vậy AP phát cái gì?
  Nó phát các frame(gồm package). Từ đây bạn có thể đoán được, tại sao device nhận được WiFi xung quanh?.
  > AP nó phát frame giúp người khác biết nó là ai, và độ mạnh của AP

  **Frame đó là gì?**
  > Beacon Frame

  Vậy `Beacon Frame` là frame được phát ra từ AP giúp device(điện thoại, laptop ....) thấy được.

  **Beacon Frame có gì? Gồm có thông tin AP như tôi đã nói? Vậy thông tin chính xác nó là gì?**

  Thật thú vị nếu bạn tự tìm hiểu nó bằng tool `Wireshark`(google để download nó nhé). Phần mềm này có thể bắt tất cả các gói tin xung quanh bạn. Đòi hỏi quyền root vì nó dùng raw-socket.
  Mình sẽ gửi vài hình ảnh dưới đây nếu các bạn nhác (Khuyến cáo không nên :D)
  ![Beacon Frame](/images/Beacon-Frame.png)
  Ở đây các bạn chú ý:
  + **Signal Strength**( thể hiện độ mạnh yếu Wireless). Nghiên cứu tại [đây](https://support.metageek.com/hc/en-us/articles/201955754-Understanding-WiFi-Signal-Strength)
  + **Destination** : ở dạng MAC ff:ff:ff:ff:ff:ff => AP muốn tất cả các `device đều nhận`.             
  + **Source Address == BSSID** : 18:44:e6:e1:b2:c4 (Gồm 24 bit đầu Nhà sản xuất, 24 bit cuối là Serial của từng card mạng )
  Ngoài ra còn có SSID: Gồm tên của Wireless mà AP tạo ra cho các trạm biết được.(Nằm ở mục Wireless Lan Management)

### 4. Bạn đã nắm được Beacon frame. Bạn đã từng thắc mắc , bạn scan wifi và chợt ra wifi cũ(wifi bạn đã kết nối ở nơi khác) lại xuất hiện ở nơi mới?

  Trường hợp này có thể xuất hiện ở một số device, một số device thì không.
  Câu trả lời đây là **Probe Frame**. Mà chính xác ở đây là **Probe Frame Request**.
  **Probe Frame Request** được tạo ra từ máy trạm nhằm mong muốn kết nối tới AP cũ.
  Tùy thuộc vào `thuật toán nhận Wireless` trên từng thiết bị có thể  nó sẽ bắt lấy `Probe Request`. Và dĩ nhiên nó đã vô tình lấy Wifi cũ nhà bạn và lưu trong list Wifi hiện sẵn.

### 5. Bạn đã hiểu cơ chế nhận Wireless rồi. Vậy cơ chế xác thực(authentication) và kết họp (association) từ máy trạm đến AP là như thế nào?

  ![Cơ chế authentication và asociation](/images/auuthentication_wireless.png)
  Máy trạm muốn kết nối tới AP phải qua 2 frame : Authentication và association.
  Đầu tiên Máy trạm gửi `authentication request` cho AP. Mục đích của frame này giúp AP nhận ra máy trạm là ai.
  Sau khi lấy thông tin máy trạm, AP gửi lại authentication reponse, mục đích là giúp máy trạm biết được AP đã nhận.
  Sau bước này: Máy trạm đã authenticated, unassociate.
  TIếp tục máy trạm gửi association request frame. Bao gồm Password Wireless được mã hóa tùy thuộc vào AP được chia sẽ bởi Share Key.
  AP sẽ trả về association response frame về phía máy trạm. Có thể thành công hoặc thất bại

# Các cách tấn công của Attacker

### 1. Crack Wifi (củ chuối)
http://zakurobot.com/
  Nguyên tắc: Attacker dùng 1 list password( khoảng mấy GB, chứa các password thông dụng ) dò mật khẩu Wifi nhà bạn
  Độ nguy hiểm: Attacker có thể dò 3000-7000 passwords/s (tùy thuộc vào cấu hình máy)
  Cách thức: Sử dụng các tool(aircrack-ng, ....)
  Phòng chống: Đặt password hạn chế về nguyên tắt, ví dụ: "jUSLOMSBHSMBFKS2HM1" (>12 ký tự)

### 2. AP Rouge (nguy hiểm hơn)
  Nguyên tắc: Attacker cần 2 card wifi. 1 card dùng để ngắt quyền truy cập client bằng cách gửi deauthentication frame. Card còn lại dùng để tạo AP giả để dụ victim vào AP giả của mình.

  **Chi tiết:**
  ![Cơ chế tấn công từ Attacker](/images/ap-rouge-principle.png)
  **a. Card 1: Ngắt quyền truy cập**
    Attacker tạo một deauthentication giả gửi tới client, client cử tưởng đó là AP thật nên thoát hẳn Wifi.
    Deauthentication giả: gồm MAC nguồn(Giả từ MAC của AP thật), MAC đích(sẽ là một list MAC nhằm gửi tất cả).
    Khi phát hiện có victim trong list MAC bằng cách victim sẽ cố gửi lại deauthentication frame lại cho AP. thì Attacker liên tục gửi deauthentication frame cho victim
  **b. Card 2: Tạo AP giả**
    Ở đây có thể thiết lập website( nhằm lấy thông tin người dùng ) dụ victim truy cập khi truy cập AP giả.


  Độ nguy hiểm: Cao, có thể mất thông tin người dùng....., Không cho phép người dùng truy cập mạng, gây rất mạng liên tục









  <!-- [Link](https://mrncciew.com/2014/10/10/802-11-mgmt-authentication-frame/) -->

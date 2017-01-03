---
title: Hiểu rõ nguyên nhân và phòng chống các thủ thuật tấn công wireless
thumbnail: https://www.myworldofwork.co.uk/sites/default/files/images/cv-sized-no-pic.jpg
tags: CIH
---
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

1. AP là gì? Station là gì?

  AP : Access Point
  AP như là cái `card wireless` có hổ trợ `phát wireless`.
  Điện thoại có hổ trợ phát Wifi => Nó là AP
  Laptop phát Wifi => Nó là AP
  Usb Wireless => Nó là AP

  Station: Máy trạm
  Chúng ta đã hiểu AP là máy phát. Vậy AP cần các máy thu để trao đổi dữ liệu.
  Máy thu có thể hiểu là station.
  Vậy Station là các kết nối tới AP.

  Tóm lại: AP phát, Station thu.
2. Bạn có tự hỏi khi chúng ta bật wifi từ thiết bị, Chúng ta thấy tất cả các Wi-Fi xung quanh? Và có những WiFi nội bộ bạn không thấy được, tại sao vậy?

  Trả lời câu hỏi này bạn phải biết Beacon Frame là gì?
  Định nghĩa Wiki thì rẫy.

  Mình nói tóm tắt lại.
  AP phát ra dựa vào sóng RF( Radio Frequency) hay bạn thường gọi là sóng radio đấy. Vậy AP phát cái gì?
  Nó phát các frame(gồm package). Từ đây bạn có thể đoán được, tại sao device nhận được WiFi xung quanh?.
  > AP nó phát frame giúp người khác biết nó là ai, và nó ở đâu với

  Frame đó là gì?
  > Beacon Frame

  Vậy Beacon Frame là Frame được phát ra từ AP xung quanh AP giúp device nhận được.

  Beacon Frame có gì? Thông tin AP? Vậy thông tin chính xác nó là gì?

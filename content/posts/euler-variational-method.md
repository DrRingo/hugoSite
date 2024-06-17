---
title: "Một kỉ niệm khác với Euler"
author: ["Nguyễn Bình Thành"]
publishDate: 2024-06-17T10:08:00+07:00
tags: ["mathnotes"]
categories: ["math"]
draft: false
featured_image: "/assets/img/taj-mahah.jpeg"
---

Cách đây mấy năm, trong lúc đang tìm kiếm đề tài cho luận văn của mình, tôi đã thử tìm hiểu bộ môn giải tích biến phân. Đó là môn tôi chưa được học trong chương trình, nhưng mà nó hứa hẹn tôi về một phương pháp tối ưu, nên tôi đọc, thế thôi.

Mày mò một hồi, tôi tự nhiên nhận ra rằng mình đã cảm được tinh thần của phép tính biến phân ấy. Mà khởi nguồn đầu tiên nhất, lại một lần nữa bắt đầu từ một người quen, Euler. Phương pháp Euler đã sử dụng để khai sinh ra phép tính biến phân thật kì lạ, nó không giống như bất kỳ điều gì tôi thấy trước đây. Nói cho mọi người dễ hiểu, thông thường làm toán hay làm bất kì điều gì khác, ta thường soi xét vật ta đang nghiên cứu, rồi đưa nó vào những tình huống cực hạn để nó bộc lộ ra những bản chất mà ta nghiên cứu, nói chung là phải có một lực từ ngoài vào, đối tượng mới tự biến đổi và thể hiện mình được. Nhưng Euler thì khác, ông chỉ quan sát sự thay đổi của các hàm số, gần như không tác động gì cả, từ đó, thông qua một vài phép biến đổi vi phân, Euler đã có được hàm số tối ưu mà gần như chẳng mất công sức nào.

Điều đó không khác gì một sự giác ngộ, cứ như là nằm ở bên trong lõi của mọi sự vật trong tự nhiên, đã có sẵn một cấu trúc tối ưu, và mọi hành động của tự nhiên đều tuân theo một quy tắc tối ưu nào đó, và công việc của Euler đơn giản chỉ là gọi nó ra tờ giấy trắng mà thôi.

Đó là kĩ thuật toán học đã có tuổi đời hơn 200 năm (phương trình Euler - Lagrange), và tôi khá chắc rằng vật lý học trong thế kỷ 19 đã tận dụng nó triệt để để tính toán tối ưu cho các phát minh của họ trong thời gian này (ví dụ như các chi tiết máy cần tính toán tối ưu ngay từ đầu). Bởi vì kĩ thuật giải phương trình Euler - Lagrange rất phức tạp, nên phản xạ ngay lúc đó của tôi là muốn giải phương trình này một cách tự động hoá bằng máy tính, symbolic và có thể vẽ ra cả đồ thị của hàm tối ưu.

Đây không phải là một ước muốn viển vông, đạt được điều này có nghĩa là từ các điều kiện ban đầu, và các ràng buộc ban đầu, với năng lực tính toán vừa đủ, ta sẽ biết được ngay lập tức đâu là đường đi tối ưu nhất dưới những điều kiện đó. Nó giống như bạn và đối thủ chuẩn bị chơi một ván cờ, nhưng bạn đã biết được các nước đi tối ưu, trước khi cả đối thủ đi nước đầu tiên.

Đời không như là mơ, tôi thực sự đã mất cả năm để duy trì mối bận tâm suy nghĩ về cách giải symbolic cho phương trình Euler - Lagrange ấy, đọc qua cả chục thư viện CAS, nhưng rồi chỉ vì một vướng mắc kĩ thuật đã làm tôi phải dừng lại.

Thế rồi, thời đại AI đã đến, và chúng có vẻ ngày càng chính xác hơn, người ta thậm chí còn viết một số phiên bản AI dùng cho những mục đích chuyên biệt, như khám chữa bệnh, giải toán,... và câu đầu tiên tôi hỏi AI, sau những câu test về độ chính xác của nó, là cách giải phương trình Euler - Lagrange này bằng symbolic. Rồi, từ từ đã chú em, chú mày đang viết cái gì thế này. Từ từ, để tao đọc đã, bên cạnh những câu lệnh bình thường, để giải quyết những vấn đề nhỏ nhặt bình thường của bài toán, thì có một câu lệnh không hiểu AI đã copy từ đâu mà tôi tìm kiếm mấy năm nay rồi không tìm được, nó đã sử dụng một cách rất sáng tạo các tài nguyên có sẵn để vượt qua vướng mắc kĩ thuật mà tôi đã dừng lại từ trước.

Và rồi, bùm, Euler - Lagrange căn bản đã được giải xong một cách tổng quát về mặt symbolic.

Thực tế thì tôi đã không còn trẻ, những chuyện kì lạ trên đời tôi gặp cũng nhiều rồi, nhiều đến nỗi tôi thường nghĩ mình đã gần đến trạng thái "bất hoặc" - tức là không còn điều gì làm mình nghi ngờ nữa cả, bản chất cuộc sống nó sẽ vốn như thế thì sẽ diễn ra như thế. Những khoảnh khắc đốn ngộ về mặt nhận thức cũng đã rất xa, xa như từ thời phổ thông của tôi. Nhưng có lẽ Euler đã nói không, ông ấy vẫn cho tôi một cảm giác khai sáng mới mẻ về bản chất của thế giới này. Và tôi nghĩ mình đủ tư cách để thay lời Euler để nói thế này: bản chất thế giới này không giống như ta thấy hàng ngày, nó rất lạ, và nó thậm chí lạ hơn những gì một người có thể nghĩ ra.

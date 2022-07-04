# Giới thiệu về source code 
source code anh có thể xem thêm tại http://gitlab.fpt.net/HI-FPT/MICROSERVICE/HI-CHAT/hi-chat-api

## Giới thiệu 
* Để đơn giản hóa, em viết source code như sau:
    * Em sẽ tạo ra các model và các function sẽ được viết dưới các model đó
    * Những function nhỏ được sử dụng nhiều lần sẽ được viết trong thư mục utils (ví dụ như function log, tạo http request )
    * Thư mục database chứa các thông tin về database schema, connect đến database
    * Thư mục routes sẽ xử lí các đường dẫn api. 

* Sau này mở rộng ra anh có thể thực hiện các cách như sau:
    * Anh hãy đập code đi, xây lại theo cách lập trình của anh 
    * Nếu anh sử dụng code trên, thì anh có thể tạo thêm model, thêm function, thêm route, utils, database 

## Những api đã viết, những api chưa viết 
### Api đã viết  
* Get_extension, mặc dù đã viết nhưng code này chưa được kiểm duyệt là đã đạt yêu cầu hay chưa 
### Api chưa viết 
* get_channel_info
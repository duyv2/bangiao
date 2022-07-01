
# Sơ đồ network

Sơ đồ network thể hiện vị trí của ejabberd, chat-management-microservice trên mạng lưới. Lưu ý đây là sơ đồ mới nhất em nhận được tại ngày 28 tháng 6 năm 2022. Trong tương lai có thể thay đổi, vì vậy em chỉ dùng sơ đồ này để giải thích quá trình hoạt động.



![alt text](https://github.com/duyv2/bangiao/blob/main/public/so_do_net_work.png?raw=true)

## Giải thích 
* Các đối tượng anh cần quan tâm trong sơ đồ này: hi-chat-XMPP server (đây là ejabberd, nằm trong khu vực màu tím góc trái trên của sơ đồ), MYSQL (là database ở bìa phải), hi-chat-api (nằm trong cụm local service, đây là chat-management-microservice)
* XMPP server sẽ có 2 đường kết nối đến. Đường thứ nhất là đi từ public vào, thông qua port 5222, client kết nối với tls, client gọi tới xmpp server này để đăng nhập và chat với các client khác. Để đăng nhập được vào xmpp, client sẽ cần có một tài khoản (gồm tài khoản và password). Đường thứ 2 là dùng để cho chat-management-microservice gọi đến xmpp thông qua http, cho phép chat-management-microservice tạo tài khoản, tạo phòng chat trên xmpp server.
* chat-management-microservice có 1 đường kết nối đến,  client sẽ gọi các api để tạo tài khoản, tạo phòng chat,...
* database được dùng để lưu thông tin tài khoản đăng nhập lên xmpp, lưu user info (họ tên, avatar, thông tin phòng chat,...). Ejabberd sử dụng 1 database và chat-management-microservice sử dụng 1 database. 

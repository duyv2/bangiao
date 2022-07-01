# Cấu hình file ejabberd.yml 
## Giới thiệu file ejabberd.yml 
* Toàn bộ thông tin cấu hình về file ejabberd.yml đề cập tại trang https://docs.ejabberd.im/admin/configuration/
* ejabberd.yml là file cấu hình của ejabberd server, anh cần phải chỉnh sửa file này để ejabberd server hoạt động theo đúng luồng và yêu cầu đã đề ra.
* ejabberd.yml nếu không được cấu hình thì sẽ sử dụng với dạng mặc định của nó, chắc chắn rằng sẽ không đáp ứng được nhu cầu của anh. 
* Tên của file này là ejabberd.yml
* Trong file này sẽ có nhiều thành phần, nhưng em sẽ chỉ đề cập đến những thành phần mình sẽ thay đổi bên dưới.
## Host 
* Host nên đặt trùng với lại tên miền. Ejabberd cho phép cấu hình nhiều hosts nhưng nếu anh có thời gian anh có thể tìm hiểu (em chưa tìm hiểu dạng nhiều hosts sẽ hoạt động như thế nào)
* Vị trí host trong file ejabberd.yml 
![alt text](https://github.com/duyv2/bangiao/blob/main/public/vi_tri_hosts_trong_ejabberd_yml.png?raw=true)
## Port 
* Sẽ có 2 port chính: 1 port dành cho chat-management-microservice gọi API đến, port còn lại sẽ dành cho app client kết nối đến để đăng nhập và chat
![alt text](https://github.com/duyv2/bangiao/blob/main/public/vi_tri_ports_trong_ejabberd_yml.png?raw=true)
* Diễn giải 
    - port 5222, ip :: nghĩa là cho phép gọi vào port 5222 từ bất kì địa chỉ ip nào, module ejabberd_c2s tức là port này xử lí loại kết nối là client đến server, max_stanza_size là kích cỡ tối đã của một thông điệp XML, access định nghĩa loại kết nối tới port, starttls_required: true (Yêu cầu client kết nối đến phải dùng tls)
    - port 80, ip :: nghĩa là cho phép gọi vào port 80 từ bất kì địa chỉ ip nào, module ejabberd_http là xử lý các loại request liên quan về http, request handle: /admin là giao diện của admin nếu anh vào đường dẫn tênmiền:80/admin, tương tự cho các route khác, ở đây cần quan tâm nhất là /api vì tại đây anh sẽ cấu hình để chat-management-microservice gọi api đến, em sẽ trình bày phía dưới 
## Database 
* Anh cần cấu hình thông tin database để ejabberd kết nối đến, dưới đây là ví dụ 
![alt text](https://github.com/duyv2/bangiao/blob/main/public/vi_tri_database_trong_ejabberd_yml.png?raw=true)
* Diễn giải 
    - Nếu không cấu hình, ejabberd sẽ sử dụng database mặc định của nó (database mnesia, 2GB)
    - default_db: sql để khai báo là ejabberd sẽ sử dụng database loại sql 
    - sql_type: mysql để khai báo là ejabberd sử dụng mysql, các loại sql_type khác (mssql | mysql | odbc | pgsql | sqlite) có thể dùng xem thêm tại https://docs.ejabberd.im/admin/configuration/toplevel/#sql-type
    - sql_server: "stg.fconnect.com.vn" để khai báo sql server, có thể sử dụng địa chỉ ip https://docs.ejabberd.im/admin/configuration/toplevel/#sql-server
    - sql_database: "db_test_ejabberd" để khai báo tên database trong sql mà ejabberd sẽ kết nối đến, https://docs.ejabberd.im/admin/configuration/toplevel/#sql-database
    - sql_username: khai báo username 
    - sql_password: pass word để truy cập vào database
    - sql_port: port kết nối đến database 
    - sql_keepalive_interval: nghĩa là cứ một khoảng thời gian thì ejabberd sẽ ping đến database, vì nếu không ping thì kết nối có thể bị đứt quãng 
    - auth_password_format, auth_scram_hash được dùng để băm mật khẩu, tức là mật khẩu client dùng để login vào ejabberd sẽ được băm đi, trong trường hợp nếu database của mình được bảo mật thì có thể xóa 2 option này đi 
## Modules 
* Ngoài các thành phần cốt lõi của ejabberd, các tính năng mở rộng được viết dưới hình thức module, anh xem chi tiết tại https://docs.ejabberd.im/developer/extending-ejabberd/modules/#what-is-a-module
* Các module sẵn có trong ejabberd, để sử dụng các module này anh thêm vào file ejabberd.yml 
![alt text](https://github.com/duyv2/bangiao/blob/main/public/modules_trong_ejabberd_.png?raw=true)
* Em sẽ diễn giải một số module quan trọng, anh có thể tìm hiểu thêm tại trang https://docs.ejabberd.im/admin/configuration/modules/
    - mod_block_strangers được dùng để ngăn chặn các client tự nhắn tin với nhau, điều này có nghĩa là anh có thể dùng nó để chặn người lạ, hacker nhắn tin tùy tiện với khách hàng của mình trong trường hợp họ dò ra được địa chỉ JID bất kì 
    - mod_fail2ban: Được dùng để chặn ip của client nếu client gửi thông tin sai định dạng lên ejabberd server, lưu ý không dùng module này nếu ejabberd đặt ở sau proxy, loadbalancer vì ejabberd sẽ chặn proxy và loadbalancer 
    - mod_http_api: Module quản lý các cuộc gọi API, như đã cấu hình ở mục port, cần có module này
## Tls
* Loại kết nối đến port 5222 phải được mã hóa tls. Cài đặt vào file ejabberd.yml như hình bên dưới 
![alt text](https://github.com/duyv2/bangiao/blob/main/public/tls_ejabberd_yml.png?raw=true)
* Diễn giải:
    - Anh sẽ cần các loại file bên trên, cụ thể 2 file quan trọng nhất là fullchain.pem, privkey.pem, sau đó bật starttls_required là true tại mục port 5222 đã đề cập ảnh trên.
    - Lưu ý: có thể không cần bật tls tại ejabberd, vì nếu trên staging sử dụng nginx, nginx đã cài tls, và điều hướng request đến ejabberd, để biết thêm chi tiết anh có thể hỏi anh Phạm Văn Ngọc 
## API permisson 
* Ta cần cài đặt làm sao để chỉ có chat-management-microservice gọi được api đến ejabberd qua port 80 mà không để cho hacker gọi vào được, về lý thuyết ta có thể sử dụng cấu hình api_permissions, nhưng trên thực tế port 80 của ejabberd sẽ được bên system giới hạn sẽ chỉ để chat-management-microservice gọi api đến. Nên em đã không dùng tính năng này trong ejabberd, nhưng nếu anh muốn tìm hiểu có thể xem tại https://docs.ejabberd.im/developer/ejabberd-api/permissions và https://docs.ejabberd.im/developer/ejabberd-api/simple-configuration/#basic-authentication

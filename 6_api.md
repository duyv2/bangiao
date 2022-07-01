
# API
* Hiện tại em chỉ sử dụng 2 api để gọi từ chat-management-microservice đến ejabberd, sau này có ejabberd có thể cập nhật, ra tính năng mới hoặc anh cần thêm loại api nào thì anh có thể theo dõi ở địa chỉ https://docs.ejabberd.im/developer/ejabberd-api/admin-api/
* 2 API em sử dụng đó là:
    - Đăng ký một tài khoản mới https://docs.ejabberd.im/developer/ejabberd-api/admin-api/#register , ý nghĩa: khi client gọi api /hi-chat-api/get_extension đến chat-management-microservice để yêu cầu chat-management-microservice cung cấp một tài khoản đăng nhập vào ejabberd, thì chat-management-microservice sẽ tạo tài khoản đăng ký lên ejabberd server rồi gửi thông tin tài khoản về cho client 
    - Cho các user vào roster của nhau https://docs.ejabberd.im/developer/ejabberd-api/admin-api/#add-rosteritem . Ý nghĩa: nhằm tránh kẻ lạ, hacker nhắn tin với khách hàng, như đã đề cập ở cấu hình file ejabberd.yml ta sẽ sử dụng module mod_block_strangers. Để 2 client nhắn tin được với nhau ta cần đưa 2 client vào roster của nhau.


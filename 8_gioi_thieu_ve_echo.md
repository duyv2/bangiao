# Giới thiệu về echo, echo10s 
## Ý nghĩa 
* echo là tài khoản được ra đời nhằm đáp ứng để bên mobile test các chức năng, mobile sẽ đăng nhập một tài khoản khác và nhắn tin đến echo, sau đó echo sẽ phản hồi lại nội dung tin nhắn đó 
* echo10s là tài khoản ra đời với mục đích giống như echo, điểm khác biệt giữa echo10s và echo là echo sẽ phản hồi ngay tức khắc trong khi echo10s sẽ phản hồi lại tin nhắn sau 10 giây .
* Code được viết bằng golang và theo code sau https://github.com/FluuxIO/go-xmpp/blob/master/_examples/xmpp_echo/xmpp_echo.go

## Triển khai 
* Vì được viết bằng code golang nên anh có thể chạy câu lệnh sau 
```
    go run xmpp_echo.go
```
* Trong đó xmpp_echo.go là file chứa source code. Anh phải sửa lại thông tin đăng nhập trong file đó để con echo này có thể login vào ejabberd server của anh 
* Vì để thuận tiện anh có thể đóng gói code trên lại thành image để sử dụng docker và chạy. 

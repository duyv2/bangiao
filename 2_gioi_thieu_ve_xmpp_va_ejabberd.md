**Lưu ý:** Những gì em trình bày về ejabberd anh có thể lên document của nó và đọc tại https://www.ejabberd.im/ và https://datatracker.ietf.org/doc/rfc6120/, để hiểu thêm về lý thuyết anh có thể tham khảo https://www.youtube.com/watch?v=GqDkc4Az_XQ

## Một số nét về XMPP
* XMPP là viết tắt của từ Extensible Messaging and Presence Protocol
* XMPP ra đời năm 2002, tiền thân của XMPP là Jabber 
* XMPP sử dụng Extensible Markup Language (XML) làm định dạng để trao đổi thông tin giữa các thực thể 
* Thực thể gồm thực thể gửi tin nhắn, thực thể nhận tin nhắn. Client và server được xem là thực thể (chưa biết được thực thể nào là gửi, thực thể nào là nhận, ví dụ, server nhận tin nhắn từ client a thì server là thực thể nhận, nhưng server gửi tin nhắn của client a cho client b thì server lại là thực thể gửi)
* Địa chỉ của 1 client (còn gọi là JID) có dạng: localpart@domainpart, full định dạng là localpart@domainpart/resourcepart. Trong đó localpart là phần định danh client, domainpart lại là host (tên miền), resourcepart là tên thiết bị của client. 
* Để trao đổi tin nhắn chỉ cần JID có dạng localpart@domainpart, nếu tin nhắn gửi đến địa chỉ vuduy@example.com thì tất cả các thiết bị đang login với JID là vuduy@example.com sẽ nhận được tin nhắn.

**Tóm lại** những điều cần nhớ là địa chỉ JID có dạng localpart@domainpart, định dạng tin nhắn là XML 

## Một số nét về Ejabberd 
* Ejabberd là server. Để dễ hiểu XMPP chỉ là giao thức, Ejabberd là server sử dụng giao thức đó.
* Ejabberd được triển khai năm 2002, phiên bản đầu tiên 1.0 ra mắt năm 2005
* Ejabberd được viết bằng ngôn ngữ Erlang
* Ejabberd hỗ trợ các database sql: MySQL, Postgres SQLite, MS SQL
* Anh có thể cấu hình ejabberd server thông qua file ejabberd.yml 

**Tóm lại** những điều cần nhớ là Ejabberd hỗ trợ sql database, và quan trọng nhất là anh phải cấu hình được cho ejabberd thông qua file ejabberd.yml.

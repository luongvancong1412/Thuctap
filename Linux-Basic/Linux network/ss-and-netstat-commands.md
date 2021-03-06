# Lệnh ss và netstat

## netstat
- Lệnh netstat là một tiện ích mạng được sử dụng để hiển thị các kết nối mạng, thống kê giao thức hoặc giao diện, bảng định tuyến, thành viên đa hướng,v.v.
- Tuy nhiên, lệnh netstat đã không được sử dụng nữa và được thay thế bằng lệnh ss nhanh hơn và dễ đọc hơn từ bộ công cụ IPROUTE

## SS
- Lệnh ss là một công cụ mạnh mẽ được sử dụng để hiển thị thông tin thống kê ổ cắm.

## Cách sử dụng cơ bản
Lệnh ss mà không có tuỳ chọn nào, nó sẽ trả về 1 danh sách đầy đủ các sockets và trạng thái kết nối:

```
ss
```

Chúng ta có thể chuyển đầu ra thành **less** để có đầu ra có thể cuộn được. Như bạn thấy, đầu ra sẽ chứa tất cả các chi tiết kết nối tcp, udp và socket. Không thực sự có thể sử dụng được. Nhưng chúng ta sẽ thấy bên dưới các tuỳ chọn khác nhau để lọc đầu ra.

## TCP/UDP established connections (-t or -u)
Chỉ xem các kết nối TCP hoặc UDP, có thể sử dụng các option -t hoặc -u.

```
ss -t
```

## 

- Theo mặc định, option -t chỉ báo cáo các kết nối đã thiết lập. Để chỉ báo cáo các socket đang nghe, chúng ta có thể sử dụng option -l
- đây là 2 ví dụ, đầu tiên là UDP, sau đó là TCP:

```
ss -ul

ss -tl
```

##

Nếu muốn xem tất cả các cổng TCP hoặc UDP ở trạng thái listen và thiết lập, có thể sử dụng option -a.

```
ss -ua

ss -ta
```

##

- Option -n ngăn chặn việc phân giải tên máy chủ và số port:

```
ss -tan
```

##

Để xem id quy trình (PID) và tên bằng socket, có thể sử dụng option -p.

Đây là 1 ví dụ mà chúng ta có thể thấy Google Chrome, sử dụng PID 13596, duyệt 1 trang web HTTPS:

```
ss -tp
```

##

Với option -o, thông tin hẹn giờ được hiển thị, ví dụ:
```
ss -tpo
```

## 
- Với option -s, chúng ta có thể xem thống kê các giao thức:

```
ss -s
```

##
Dưới đây là 1 ví dụ để xem liệu dịch vụ IPv4 có đang lắng nghe hay không:
```
ss -tunlp4
```
Trong đó:
- -t Hiển thị các cổng TCP
- -u Hiển thị các cổng UDP
- -n Không phân giải tên máy chủ
- -l Chỉ hiển thị các cổng nghe.
- -p Hiển thị các quy trình đang sử dụng 1 socket cụ thể.
- -4 Chỉ hiển thị các socket IPv4

##

Một option rất hay khác có sẵn với lệnh ss là khả năng lọc bằng cách sử dụng các trạng thái ICP.

Cú pháp là:
```
ss [option] [filter]
```

Có thể sử dụng các bộ lọc sau:


Ngoài ra còn có 1 số kết hợp được xác định trước của các trạng thái:
- - Tất cả các trạng thái trên
- - Tất cả các trạng thái ngoại trừ lắng nghe và đóng cửa
- - Tất cả các trạng thái được kết nối ngoại trừ được gửi qua đồng bộ
- - Hiển thị các trạng thái, được duy trì dưới dạng minisockets, tức là thời gian chờ và syn-recv.
- - Đối lập vưới trạng thái xô.

Dưới đây là 1 ví dụ để xem các phiên TCP ở trạng thái đã thiết lập:
```
ss -t 
```
Hoặc, để xem tất cả các socket IPv4 ở trạng thái listen:
```
ss -4
```

##
Vì chúng tôi có thể lọc bằng cách sử dụng trạng thái, cũng có thể lcij theo địa chỉ hoặc số cổng.

Ví dụ đầu tiên: đầu tiên sẽ liệt kê tất cả các phiên đã thiết lập IPv4 (-4), sau đó sẽ lọc để xem phiên có đích 193.247.171.26:
```
ss -4

ss -4
```


Cũng có thể lọc địa chỉ nguồn, nếu máy chủ của bạn có nhiều interface, với bộ lọc src:
```
ss -4 src 10.0.2.15
```
Lưu ý, chúng ta cũng có thể sử dụng ký hiệu CIDR:
```
ss -4 state
```

##
Để lọc số cổng hoặc ứng dụng, cú pháp như sau:

```
ss -4
```
 là những bộ lọc khả thi.

Sau đó, có thể sử dụng tên ứng dụng (ssh, telnet, HTTP, HTTPS,...) hoặc số cổng (22, 23, 80, 443, ...).

Cũng có thể sử dụng phạm vi cổng. Ví dụ: để xem tất cả các socket sử dụng cổng nguồn lớn hơn 1023:

```
ss -nt sport \>:1023
```

Nếu sử dụng các ký tự đặc biệt phải thêm dấu gạch chéo ngược ở phía trước, như trên. Nếu không, hãy sử dụng "le", "ge", "eq", ....

Các option là:
- <= or le: Nhỏ hơn hoặc bằng cổng
- >= or ge: Lớn hơn hoặc bằng cổng
- == or eq: Bằng với cổng
- != or ne: Không bằng cổng
- < or lt: ít hơn cổng
- > or gt: Lớn hơn cổng

Ví dụ:
```
ss -nt sport gt: 1023
giống với:
ss -nt sport \>: 1023
```

Sau đó, có thể kết hợp mọi thứ:
```
ss '()'
```

##
Hiển thị tất cả các socket TCP:
```
ss -t -a
```

Hiển thị all các socket TCP với ngữ cảnh bảo mật SELinux quy trình:
```
ss -taZ
```

Hiển thị tất cả các ổ cắm UDP:
```
ss -ua
```

Hiển thị tất cả (vào và ra) các kết nối ssh đã thiết lập:
```
ss -o
```

Hiển thị tất cả các kết nối HTTP và HTTPS đã thiết lập gửi đi:
```
ss
```
Tìm tất cả các quy trình cục bộ được kết nối với máy chủ X:
```
ss -x
```

Liệt kê tất cả các ổ cắm TCP ở trạng thái FIN-WAIT-1 cho máy chủ web của chúng tôi, cho mạng 193.233.7 / 24 và xem bộ hẹn giờ của chúng:

```
ss -o
```

Liệt kê các ổ cắm ở tất cả các trạng thái từ tất cả các bảng ổ cắm trừ TCP:
```
ss -a
```

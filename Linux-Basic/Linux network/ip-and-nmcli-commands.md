# Lệnh ip và nmcli

## The ip commands: IP queries (the “show” commands)


### Link status

Lệnh **ip link show** sẽ hiển thị thông tin cho tất cả interface:
```
[root@haproxy ~]# ip link show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP mode DEFAULT group default qlen 1000
    link/ether 00:0c:29:88:9b:cb brd ff:ff:ff:ff:ff:ff
3: ens37: <BROADCAST,MULTICAST> mtu 1500 qdisc pfifo_fast state DOWN mode DEFAULT group default qlen 1000
    link/ether 00:0c:29:88:9b:d5 brd ff:ff:ff:ff:ff:ff

```

Trong ví dụ này, chúng ta có thể thấy 4 giao diện:

- lo: là giao diện lặp lại
- ens33: là một giao diện ethernet. Chúng ta có thể thấy trạng thái là "UP".
- ens37: là một giao diện ethernet khác. Ở đây trạng thái chúng ta "DOWN".

Đầu ra mà con người dễ đọc hơn là với tùy chọn -brief , có thể được rút ngắn thành -br :
(Đúng, như “show ip int brief”)
```
[root@haproxy ~]# ip -br link show
lo               UNKNOWN        00:00:00:00:00:00 <LOOPBACK,UP,LOWER_UP>
ens33            UP             00:0c:29:88:9b:cb <BROADCAST,MULTICAST,UP,LOWER_UP>
ens37            DOWN           00:0c:29:88:9b:d5 <BROADCAST,MULTICAST>
```
Thêm option -c[olor] để hiển thị màu cho UP,DOWN
```
ip -br -c link show
```

Xem một interface:
```
[root@haproxy ~]# ip -br link show ens33
ens33            UP             00:0c:29:88:9b:cb <BROADCAST,MULTICAST,UP,LOWER_UP>
```

### interfaces statistics
Sử dụng tuỳ chọn -s để xem interface statistics:



Xem 1 interface cụ thể:


### Display the MAC address table

Sử dụng lệnh **ip neigh** để xem bảng địa chỉ MAC:

### Display the IP information

Sử dụng lệnh ip addr để kiểm tra địa chỉ IP. Sử dụng option -br để có đầu ra dễ đọc hơn.

Trong trường hợp có nhiều interface, có thể hiển thị 1 interface cụ thể:

### Display the routing table

Lệnh ip route để hiển thị bảng định tuyến

### Display the route for an address

Lệnh **ip route get** để hiển thị tuyến đường mà 1 địa chỉ sẽ sử dụng

Ở đây, chúng ta có thể thấy đối với đích 8.8.8.8 bước tiếp theo sẽ là 10.0.2.2 (cổng mặc định trong ví dụ trước), thông qua giao diện cục bộ: enp0s3.

### Making changes

Sau đây là một số ví dụ về cách thực hiện thay đổi đối với cấu hình mạng.

**Lưu ý quan trọng: trước khi đi sâu vào các ví dụ, cần lưu ý rằng có nhiều khác biệt về cách phần mạng được quản lý trên RHEL / CentOS, giữa phiên bản trước và phiên bản hiện tại. Bài đăng này dựa trên CentOS 8.0 sử dụng NetworkManager (mặc định).**

**Ví dụ: theo mặc định với RHEL / CentOS 8, nếu bạn cố gắng sử dụng tệp đơn vị network.service kế thừa, tệp này sẽ không khả dụng và bạn sẽ gặp lỗi:**

```
# systemctl restart network
Failed to restart network.service: Unit network.service not found.
```

### Bring up/down an interface

#### Các lệnh với IP

- Để tắt interface 
```
ip link set enp0s3 down
```

- Xem lại trạng thái:
```
ip -br addr
```
- Bật lại và kiểm tra lại trạng thái:
```
# ip link set enp0s3 up
# ip -br addr
```

#### Các lệnh với nmcli


```
nmcli device connect enp0s3
```

```
nmcli device disconnect enp0s3
```

### Change the IP address
Một số ví dụ thay đổi địa chỉ IP, từ IP DHCP sang IP tĩnh.

Trạng thái ban đầu: 1 interface là enp0s3 được cấu hình DHCP
Mục tiêu: đặt địa chỉ IPv4 tĩnh: 10.0.2.200/24

#### Các lệnh với nmcli

- Gán IPv4 10.0.2.200 cho giao diện ens37

```
nmcli con mod ens37 ipv4.addresses 10.0.2.200/24
```

- Đặt gateway là 10.0.2.2:
```
nmcli con mod ens37 ipv4.gateway 10.0.2.2
```
- Thay đổi cấu hình từ dhcp sang static:

```
nmcli con mod ens37 ipv4.method manual
```
- Đặt DNS là 1.1.1.1:
```
nmcli con mod ens37 ipv4.dns "1.1.1.1"
```
- Lưu lại các thay đổi và reload lại interface:
```
nmcli con up ens37
```

Kiểm tra lại thay đổi bằng lệnh ip -br a
```
ip -br a
```

- Có thể xem lại những gì nmcli thay đổi từ file network-script:

```
cat /etc/sysconfig/network-scripts/ifcfg-ens37
```

#### Network-script

Có thể hoàn lại thay đổi bằng cách thay đổi file /etc/sysconfig/network-script/ifcfg-ens37:

```
# vi /etc/sysconfig/network-scripts/ifcfg-ens37
(...edit the file...)

# cat /etc/sysconfig/network-scripts/ifcfg-ens37 
```
- Khởi động lại dịch vụ, ta có lại IP dhcp:

```
systemctl restart NetworkManager.service 
```

#### Nmtui
Một phương pháp khác thay đổi địa chỉ IP là sử dụng công cụ NMTUI.

- Khởi động tool:
```
nmtui
```
hoặc
```
nmtui edit <interfacename>
```
- Sau đó xuất hiện giao diện đồ hoạ:

![](./../image/nmtui.png)

### Create 802.1q sub-interfaces and add an IP to it
More advanced networking.
Ví dụ: có 1 gioa diện ethernet vật lý và muốn sử dụng nó như 1 trunk với các giao diện con khác nhau (sub-interface)

#### Lệnh nmcli
- Tạo 2 sub-interface, VLAN gắn thẻ 10 và 20 với IP là 192.168.10.200/24 và 192.168.20.200/24:
```
nmcli con add type vlan con-name vlan-ens37.10 ifname ens37.10 dev ens37 id 10 ip4 192.168.10.200/24

nmcli con add type vlan con-name vlan-ens37.20 ifname ens37.20 dev ens37 id 20 ip4 192.168.20.200/24
```

- Dùng lệnh nmcli hoặc ip để xem interface vừa tạo:
```
nmcli connection

ip -br link show 

ip -br a
```
- Cũng có thể xem các interface được tạo trong thư mục /var/sysconfig/network-script.
```
ls -la /etc/sysconfig/network-scripts/
total 16
drwxr-xr-x. 2 root root   82 18 oct 12:38 .
drwxr-xr-x. 7 root root 4096 16 oct 14:44 ..
-rw-r--r--. 1 root root  267 18 oct 12:36 ifcfg-enp0s3
-rw-r--r--. 1 root root  388 18 oct 12:38 ifcfg-vlan-enp0s3.10
-rw-r--r--. 1 root root  388 18 oct 12:38 ifcfg-vlan-enp0s3.20
```
- Và xem nội dung của 1 interface:
```
# cat /etc/sysconfig/network-scripts/ifcfg-vlan-enp0s3.10
VLAN=yes
TYPE=Vlan
PHYSDEV=enp0s3
VLAN_ID=10
REORDER_HDR=yes
GVRP=no
MVRP=no
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=none
IPADDR=192.168.10.200
PREFIX=24
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=vlan-enp0s3.10
UUID=57d81e20-7777-44e9-92c2-bd3a8656f189
DEVICE=enp0s3.10
ONBOOT=yes
```

- Các interface được UP lên ngay lập tức và ta có thể ping chúng:

```
# ping 192.168.10.200
PING 192.168.10.200 (192.168.10.200) 56(84) bytes of data.
64 bytes from 192.168.10.200: icmp_seq=1 ttl=64 time=0.284 ms
64 bytes from 192.168.10.200: icmp_seq=2 ttl=64 time=0.090 ms
64 bytes from 192.168.10.200: icmp_seq=3 ttl=64 time=0.253 ms
^C
--- 192.168.10.200 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 76ms
rtt min/avg/max/mdev = 0.090/0.209/0.284/0.085 ms

# ping 192.168.20.200
PING 192.168.20.200 (192.168.20.200) 56(84) bytes of data.
64 bytes from 192.168.20.200: icmp_seq=1 ttl=64 time=0.153 ms
64 bytes from 192.168.20.200: icmp_seq=2 ttl=64 time=0.172 ms
64 bytes from 192.168.20.200: icmp_seq=3 ttl=64 time=0.131 ms
^C
--- 192.168.20.200 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 42ms
rtt min/avg/max/mdev = 0.131/0.152/0.172/0.016 ms
```

### Add/ Delete/ Replace an entry to the routing table

- Xem bảng định tuyến:

```
ip route
```
Như bạn thấy, bảng định tuyến của tôi bao gồm hai tuyến đường được kết nối: 192.168.10.0/24 và 192.168.20.0/24 tương ứng với hai giao diện con đã tạo ở trên. Nhưng, tôi không có tuyến đường mặc định nữa.

#### Lệnh IP:
- Tạo 1 via 192.168.10.1 trên ens37.10 và kiểm tra kết quả:

```
ip route add default via 192.168.10.1 dev ens37.10

ip route

ip route get 8.8.8.8
```

- Thêm 1 static route:

```
ip route add 10.0.0.0/16 via 192.168.20.1 dev ens37.20
ip route add 11.0.0.0/16 via 192.168.20.1 dev ens37.20

ip route
```
- Xoá 1 route:

```
ip route delete 11.0.0.0/16 via 192.168.20.1 dev ens37.20

ip route
```
Lưu ý: Những thay đổi sẽ bị mất sau khi khởi động lại máy.

#### Với lệnh nmcli
- Đầu tiên, liệt kê các thiết bị

```
nmcli conn
```

- Sau đó, thêm 2 static route mới. Ví dụ: thêm 192.168.222.0/24 tới 192.168.10.1

```
nmcli con modify vlan-ens37.10 +ipv4.routes "192.168.222.0/24 192.168.10.1"
```

- Đặt lại interface và kiểm tra lại bảng định tuyến:

```
nmcli con up vlan-ens37.10
ip route
```

- Cách thêm 1 default gateway trên interface VLAN20:
```
nmcli con mod vlan-ens37.20 ipv4.gateway "192.168.20.1"
nmcli con up vlan-ens37.20

ip route
```
Note: Những thay đổi này diễn ra persistent sau khi máy khởi động lại.



### IP Forwarding

Forwarding (routing) giữa các interface của máy linux bị tắt theo mặc định vì lý do bảo mật.

Để kích hoạt nó, phải thay đổi giá trị mặc định trong file /proc/sys/net/ipv4/ip_osystem từ 0 thành 1.


Điều này có thể thực hiện bằng cách chỉnh sửa tệp (sử dụng vi hoặc trình chỉnh sửa khác) hoặc sử dụng lệnh:

```
echo 1 > /proc/sys/net/ipv4/ip_forward
```
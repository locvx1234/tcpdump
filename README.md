# tcpdump
Tìm hiểu về cách sử dụng tcpdump

## 1. tcpdump là gì?
*tcpdump* là phần mềm dùng để bắt gói tin trên mạng, nhằm mục đích phân tích chúng.
	
## 2. Cài đặt tcpdump
Để cài tcpdump trên Linux, bạn sử dụng lệnh :

	$ apt-get install tcpdump

Hoặc có thể vào trang [tcpdump](http://www.tcpdump.org/#latest-release) để tải mã nguồn của công cụ này.

## 3. Làm việc với tcpdump
### 3.1. Chọn Interface để bắt tin

	$ tcpdump -i 'interface'
	
Ví dụ :
```
root@ubuntu:~# tcpdump -i eth0
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), capture size 65535 bytes
21:47:07.107560 IP 192.168.0.10.netbios-ns > 192.168.0.255.netbios-ns: NBT UDP PACKET(137): QUERY; REQUEST; BROADCAST
21:47:07.682760 IP 192.168.0.10.netbios-ns > 192.168.0.255.netbios-ns: NBT UDP PACKET(137): QUERY; REQUEST; BROADCAST
21:47:07.822665 IP 192.168.0.10.netbios-ns > 192.168.0.255.netbios-ns: NBT UDP PACKET(137): QUERY; REQUEST; BROADCAST
21:47:08.022032 IP 192.168.0.46.53984 > dns4.viettel.com.vn.domain: 48904+ PTR? 255.0.168.192.in-addr.arpa. (44)
21:47:08.027195 IP dns4.viettel.com.vn.domain > 192.168.0.46.53984: 48904* 0/0/0 (44)
21:47:08.027439 IP 192.168.0.46.38707 > dns4.viettel.com.vn.domain: 53789+ PTR? 10.0.168.192.in-addr.arpa. (43)

```

Lệnh sẽ liệt kê các gói tin lưu thông qua card mạng eth0.

### 3.2. Giới hạn số lượng gói tin 

	$ tcpdump -c 'number'

Ví dụ :
```
root@ubuntu:~# tcpdump -c 3 -i eth0
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), capture size 65535 bytes
21:59:12.925442 IP 192.168.0.10.netbios-ns > 192.168.0.255.netbios-ns: NBT UDP PACKET(137): QUERY; REQUEST; BROADCAST
21:59:13.744870 IP 192.168.0.10.netbios-ns > 192.168.0.255.netbios-ns: NBT UDP PACKET(137): QUERY; REQUEST; BROADCAST
21:59:13.861716 IP 192.168.0.46.59164 > dns4.viettel.com.vn.domain: 61420+ PTR? 255.0.168.192.in-addr.arpa. (44)
3 packets captured
11 packets received by filter
0 packets dropped by kernel
```

Số gói tin được giới hạn là 3. Sau khi bắt đủ 3 gói tin, chương trình kết thúc.

### 3.3. Hiển thị dạng ASCII của gói tin bắt được 

	$ tcpdump -A 
	
Ví dụ : 
```
root@ubuntu:~# tcpdump -A -i eth0
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), capture size 65535 bytes
22:08:53.053085 IP6 fe80::a12e:2592:be84:e696.57398 > ff02::c.1900: UDP, length 146
`.................%......................6.l..KLM-SEARCH * HTTP/1.1
Host:[FF02::C]:1900
ST:urn:Microsoft Windows Peer Name Resolution Protocol: V4:IPV6:LinkLocal
Man:"ssdp:discover"
MX:3


22:08:53.413647 IP 192.168.0.46.43303 > dns4.viettel.com.vn.domain: 48656+ PTR? c.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.2.0.f.f.ip6.arpa. (90)
E..v.g@.@........q...'.5.b...............c.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.2.0.f.f.ip6.arpa.....
```

Tùy chọn -A sẽ hiển thị dạng ASCII của dữ liệu bắt được. Nó tương đương phần này trong Wireshark : 

<img src="http://i.imgur.com/U8NTSvP.png">

### 3.4. Hiển thị dạng Hex và ASCII của gói tin bắt được 
	
	$ tcpdump -XX
	
Ví dụ : 
```
root@ubuntu:~# tcpdump -XX -i eth0
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), capture size 65535 bytes
22:10:37.710004 IP6 fe80::a12e:2592:be84:e696 > ff02::1:ffb9:6b87: ICMP6, neighbor solicitation, who has fe80::12b:b7a:e4b9:6b87, length 32
        0x0000:  3333 ffb9 6b87 70f1 a1ca a133 86dd 6000  33..k.p....3..`.
        0x0010:  0000 0020 3aff fe80 0000 0000 0000 a12e  ....:...........
        0x0020:  2592 be84 e696 ff02 0000 0000 0000 0000  %...............
        0x0030:  0001 ffb9 6b87 8700 93aa 0000 0000 fe80  ....k...........
        0x0040:  0000 0000 0000 012b 0b7a e4b9 6b87 0101  .......+.z..k...
        0x0050:  70f1 a1ca a133                           p....3
```

Tùy chọn -XX sẽ hiển thị dạng Hex và ASCII của dữ liệu bắt được. Nó tương đương phần này trong Wireshark : 

<img src="http://i.imgur.com/wPsYWuC.png">

### 3.5. Lưu các gói tin bắt được vào file 

	$ tcpdump -w filename.pcap
	
Ví dụ : 
```
root@ubuntu:~# tcpdump -w cap_tcpdump.pcap -i eth0
tcpdump: listening on eth0, link-type EN10MB (Ethernet), capture size 65535 bytes
7 packets captured
7 packets received by filter
0 packets dropped by kernel
```

Một file `cap_tcpdump.pcap` chứa các gói tin bắt được sẽ được lưu lại. Phần mở rộng là `.pcap` để phù hợp với các phần mềm phân tích.
 
### 3.6. Đọc file chứa các gói tin 

	$ tcpdump -r filename.pcap 

Ví dụ : 
```
root@ubuntu:~# tcpdump -r cap_tcpdump.pcap
reading from file cap_tcpdump.pcap, link-type EN10MB (Ethernet)
22:13:17.669209 IP6 fe80::a12e:2592:be84:e696.49300 > ff02::1:3.hostmon: UDP, length 22
22:13:17.669275 IP6 fe80::a12e:2592:be84:e696.55047 > ff02::1:3.hostmon: UDP, length 22
22:13:17.669544 IP 192.168.0.6.55047 > 224.0.0.252.hostmon: UDP, length 22
22:13:17.669575 IP 192.168.0.6.49300 > 224.0.0.252.hostmon: UDP, length 22
22:13:17.997440 IP6 fe80::a12e:2592:be84:e696.dhcpv6-client > ff02::1:2.dhcpv6-server: dhcp6 solicit
22:13:18.007332 IP 192.168.0.6.netbios-ns > 192.168.0.255.netbios-ns: NBT UDP PACKET(137): QUERY; REQUEST; BROADCAST
22:13:18.758076 IP 192.168.0.6.netbios-ns > 192.168.0.255.netbios-ns: NBT UDP PACKET(137): QUERY; REQUEST; BROADCAST
```

In ra file `cap_tcpdump.pcap` vừa lưu.
### 3.7. Đọc file chứa các gói tin lớn hơn 1 kích cỡ cho sẵn

	$ tcpdump -r filename.pcap greater 'size'
	
Ví dụ : 
```
root@ubuntu:~# tcpdump -r cap_tcpdump.pcap greater 128
reading from file cap_tcpdump.pcap, link-type EN10MB (Ethernet)
22:13:17.997440 IP6 fe80::a12e:2592:be84:e696.dhcpv6-client > ff02::1:2.dhcpv6-server: dhcp6 solicit
```

### 3.8. Đọc file chứa các gói tin nhỏ hơn 1 kích cỡ cho sẵn

	$ tcpdump -r filename.pcap less 'size'
	
Ví dụ : 
```
root@ubuntu:~# tcpdump -r cap_tcpdump.pcap less 128
reading from file cap_tcpdump.pcap, link-type EN10MB (Ethernet)
22:13:17.669209 IP6 fe80::a12e:2592:be84:e696.49300 > ff02::1:3.hostmon: UDP, length 22
22:13:17.669275 IP6 fe80::a12e:2592:be84:e696.55047 > ff02::1:3.hostmon: UDP, length 22
22:13:17.669544 IP 192.168.0.6.55047 > 224.0.0.252.hostmon: UDP, length 22
22:13:17.669575 IP 192.168.0.6.49300 > 224.0.0.252.hostmon: UDP, length 22
22:13:18.007332 IP 192.168.0.6.netbios-ns > 192.168.0.255.netbios-ns: NBT UDP PACKET(137): QUERY; REQUEST; BROADCAST
22:13:18.758076 IP 192.168.0.6.netbios-ns > 192.168.0.255.netbios-ns: NBT UDP PACKET(137): QUERY; REQUEST; BROADCAST
```

### 3.9. Lọc theo protocol 

	$ tcpdump 'protocol'
	
Ví dụ : 
```
root@ubuntu:~# tcpdump -i eth0 udp
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), capture size 65535 bytes
22:36:41.922745 IP 192.168.0.6.57400 > 239.255.255.250.1900: UDP, length 133
22:36:42.217853 IP 192.168.0.46.48100 > dns4.vietel.com.vn.domain: 51289+ PTR? 250.255.255.239.in-addr.arpa. (46)
22:36:42.222447 IP dns4.vietel.com.vn.domain > 192.168.0.46.48100: 51289 0/0/0 (46)
22:36:42.222911 IP 192.168.0.46.38280 > dns4.vietel.com.vn.domain: 41661+ PTR? 6.0.168.192.in-addr.arpa. (42)
```

Lọc các gói tin sử dụng một trong các phương thức : fddi, tr, wlan, ip, ip6, arp, rarp, decnet, tcp và udp.

### 3.10. Lọc theo IP nguồn và IP đích 

	$ tcpdump src 'IP nguồn' and dsc "IP đích"

Ví dụ : 
```
root@ubuntu:~# tcpdump -i eth0 src 192.168.0.6 and dst 239.255.255.250
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), capture size 65535 bytes
23:06:30.306087 IP 192.168.0.6 > 239.255.255.250: igmp v2 report 239.255.255.250
```
	
	
### 3.11. Các tùy chọn hiển thị thời gian 
- -t : Không hiển thị thời gian 
- -tt : Khoảng thời gian tính từ 00:00:00 1/1/1970
- -ttt : thời gian tính từ lúc bắt đầu bắt gói tin 
- -tttt : thời gian thực lúc bắt gói tin
	
Các tùy chọn được thêm vào các lệnh để ẩn hoặc hiện thị thời gian như mong muốn.

## 4. Tham khảo 

http://securitydaily.net/phan-tich-goi-tin-15-lenh-tcpdump-duoc-su-dung-trong-thuc-te/

http://www.tcpdump.org/manpages/tcpdump.1.html
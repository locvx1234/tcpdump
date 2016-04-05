# tcpdump
Tìm hiểu về cách sử dụng tcpdump

## 1. tcpdump là gì?
	*tcpdump*  là phần mềm bắt gói tin trên mạng nhằm mục đích phân tích chúng.
	
## 2. Cài đặt tcpdump
Sử dụng lệnh :

	$ apt-get install tcpdump

Hoặc có thể vào trang [tcpdump](http://www.tcpdump.org/#latest-release) để tải mã nguồn của công cụ này.

## 3. Chọn Interface để bắt tin

	$ tcpdump -i 'interface'
	
```
	tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
	listening on eth0, link-type EN10MB (Ethernet), capture size 65535 bytes
	21:47:07.107560 IP 192.168.0.10.netbios-ns > 192.168.0.255.netbios-ns: NBT UDP PACKET(137): QUERY; REQUEST; BROADCAST
	21:47:07.682760 IP 192.168.0.10.netbios-ns > 192.168.0.255.netbios-ns: NBT UDP PACKET(137): QUERY; REQUEST; BROADCAST
	21:47:07.822665 IP 192.168.0.10.netbios-ns > 192.168.0.255.netbios-ns: NBT UDP PACKET(137): QUERY; REQUEST; BROADCAST
	21:47:08.022032 IP 192.168.0.46.53984 > dns4.viettel.com.vn.domain: 48904+ PTR? 255.0.168.192.in-addr.arpa. (44)
	21:47:08.027195 IP dns4.viettel.com.vn.domain > 192.168.0.46.53984: 48904* 0/0/0 (44)
	21:47:08.027439 IP 192.168.0.46.38707 > dns4.viettel.com.vn.domain: 53789+ PTR? 10.0.168.192.in-addr.arpa. (43)
```

## 4. Giới hạn số lượng gói tin 

	$ tcpdump -c 'number'
	
	
[TOC]

# Overview

# Open Source Hardware
- [Talos Secure Workstation][3]

# Network Devide
From phone line -> Modem ADSL -> Router -> Switch -> Computer

Today, maybe one devide can be all of them (Modem + Router + Switch).

## Modem
Box from your ISP that connects to the internet. It actually connects to the phone line or the coaxial cable or whatever physical line you have. It normally has at least an ethernet connection, sometimes a USB as well.

- LAN: RJ45 jack (UTP cable + Ethernet port on modem)
- Phone line: RJ11 jack (DSL Cable + DSL port on modem)

## Router
Box that connects to the modem and allows multiple devices to use that internet connection at the same time. It also lets the devices talk to each other (so you can transfer files in your house or whatever). Can be wired, wireless, or both.

All input output is RJ45 (WAN and LAN)

## Wireless Access Point
Attaches to a router and allows wifi connections to the network.

## Switch

# WAN & LAN
1. Phân biệt việc kêt nối mạng cho wifi router vào port WAN hay port LAN
	- Gắn vào Port LAN thì sẽ phát cùng lớp mạng với nguồn cung cấp (vd: cùng lớp 192.168.1.0/24) cần phải tắt chế độ DHCP trên tất cả các con router wireless này
	- Gắn vào Port WAN: port WAN có 3 chế độ
		+ **Bridge Mode** (giống hệt như gắn vào port LAN ít router hỗ trợ)
		+ **DHCP client** chế độ này router wifi phải cấp DHCP lớp nào thì tùy bạn (vd: 192.168.12.0/24 cần phải khác với lớp được nhận từ WAN) tất cả user kết nối đến wifi router này đều đứng sau NAT tức là chỉ chia sẻ file với các user cùng kết nối chung SSID và router wireless nếu bạn không mở port , ( 192.168.12.3/24==>NAT==>192.168.1.6/24==>NAT==>180.148.4.6{Public IP})
		+ **Static IP** đặt IP cho WAN nếu bạn muốn quản lý nó dễ dàng hơn mọi thứ giống như DHCP client.

2. Lưu ý khi sử dụng nhiều router wireless để phủ sóng wifi
	- Cần phải xác định bạn có dùng phần mềm để quản lý băng thông hay phân quyền truy nhập gì không, có cần share file hay không. Có thì kết nối vào port LAN không cần thì kết nối vào WAN hay LAN gì cũng được. (nếu gắn vào LAN chú ý router chính cung cấp DHCP có đủ số lượng và ổn định không)
	- Router của bạn có tính năng WDS không. Nếu có có thể bật tính năng này lên và cấu hình cho các thiết bị cùng phát 1 SSID và Pass để di chuyển không phải gõ lại pass nhiều lần (nên tham khảo thêm tài liệu)
	- Quy hoạch sóng để tránh nhiễu ( 3 chanel không chồng lấn nhau là 1,6,11)


# References
[1]: https://en.wikipedia.org/wiki/List_of_open-source_hardware_projects "Wikipedia - List of open-source hardware projects"
[2]: https://en.wikipedia.org/wiki/Open-source_hardware "Wikipedia - Open source hardware"
[3]: https://www.crowdsupply.com/raptor-computing-systems/talos-secure-workstation "Talos Secure Workstation"

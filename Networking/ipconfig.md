# 🌐 Networking Fundamentals

## 📌 Giới thiệu về IP
Networking = kết nối nhiều thiết bị (host) với nhau để chia sẻ dữ liệu, dịch vụ, tài nguyên.
Mỗi thiết bị trong mạng cần địa chỉ IP để nhận dạng.
```
Wireless LAN adapter Wi-Fi:

    Connection-specific DNS Suffix  . : ➡️ Là hậu tố tên miền tự động thêm vào khi bạn truy vấn DNS.
        Ở đây để trống ⇒ mạng không cấu hình suffix.
    Description . . . . . . . . . . . : ➡️ Mô tả phần cứng — chính là tên card mạng Wi-Fi.
    Physical Address. . . . . . . . . : ➡️ Địa chỉ MAC của card mạng — duy nhất cho mỗi thiết bị.
        Dạng 6 cặp hex: XX-XX-XX-XX-XX-XX
        Dùng ở tầng Data Link (Layer 2).
        Trong pentest, MAC có thể spoof (giả mạo) để ẩn danh hoặc bypass filter.
    DHCP Enabled. . . . . . . . . . . : Yes ➡️ Yes → Máy nhận IP tự động từ DHCP Server (thường là router Wi-Fi).
        DHCP (Dynamic Host Configuration Protocol) là một giao thức mạng cho phép tự động cấp phát địa chỉ IP và các cấu hình mạng khác.
    Autoconfiguration Enabled . . . . : Yes ➡️ Yes → Cho phép Windows tự tạo IP tạm thời nếu DHCP không cấp được (APIPA).
        APIPA (Automatic Private IP Addressing) là một cơ chế cho phép các thiết bị trong mạng cục bộ tự động gán cho mình một địa chỉ IP trong khoảng từ 169.254.0.1 đến 169.254.255.254.
    IPv6 Address. . . . . . . . . . . : (Preferred)➡️ Địa chỉ IP phiên bản 6
        Được biểu diễn bằng 8 nhóm hex, cách nhau bằng dấu ":", hỗ trợ không gian địa chỉ lớn hơn IPv4.
        Các địa chỉ này gồm cả Global và Link-local:
            2401:d800:... → Global IPv6 (có thể định tuyến qua Internet)
            fe80::... → Link-local (chỉ dùng trong mạng LAN)
        (Preferred) nghĩa là địa chỉ hiện đang được dùng.
    Temporary IPv6 Address. . . . . . : (Preferred)
    IPv6 Address. . . . . . . . . . . : (Deprecated)
        (Deprecated) nghĩa là địa chỉ cũ, sắp hết hạn, không dùng nữa.
    Temporary IPv6 Address. . . . . . : (Deprecated)
    Link-local IPv6 Address . . . . . : (Preferred)
    IPv4 Address. . . . . . . . . . . : (Preferred) ➡️ Địa chỉ IP phiên bản 4, địa chỉ IP hiện tại của máy bạn trong mạng LAN.
        Được biểu diễn bằng 4 octet, cách nhau bằng dấu ".".
        Có 2 phần:
            Network ID: xác định mạng (ví dụ: 192.168.1.0)
            Host ID: xác định thiết bị trong mạng (ví dụ: .10)
        (Preferred) nghĩa là IP hợp lệ, đang hoạt động.
    Subnet Mask . . . . . . . . . . . : ➡️ Cho biết phần Network ID / Host ID của IP.
        255.255.255.0 = /24 nghĩa là 24 bit đầu là Network ID, còn lại 8 bit là Host ID.
        → Network ID = 192.168.110.0
        → Host range = .1 đến .254
    Lease Obtained. . . . . . . . . . : ➡️ Khoảng thời gian DHCP cấp IP cho bạn.
    Lease Expires . . . . . . . . . . : ➡️ Sau khi hết hạn, máy sẽ xin lại IP mới từ server DHCP.
    Default Gateway . . . . . . . . . : ➡️ Thường là địa chỉ IP của router mà máy bạn dùng để ra ngoài mạng LAN.
        Khi mỗi gói tin gửi ra ngoài mạng LAN, nó sẽ được chuyển đến Default Gateway trước.
    DHCP Server . . . . . . . . . . . : ➡️ Địa chỉ của server cấp IP tự động — trong mạng gia đình thường trùng với router (gateway).
        → Router có thể vừa làm Gateway, vừa làm DHCP Server.
    DHCPv6 IAID . . . . . . . . . . . : 170447082
    DHCPv6 Client DUID. . . . . . . . : 00-01-00-01-30-5D-45-01-8C-B0-E9-25-C3-B7
    DNS Servers . . . . . . . . . . . : ➡️ Máy chủ DNS được dùng để phân giải tên miền → IP.
    NetBIOS over Tcpip. . . . . . . . : ➡️ Enabled -> Cho phép chia sẻ file, printer, và đặt tên trong mạng Windows (qua SMB).
```
Ví dụ thực tế:
```
Wireless LAN adapter Wi-Fi:

    Connection-specific DNS Suffix  . : 
    Description . . . . . . . . . . . : Intel(R) Wireless-AC 9560 160MHz
    Physical Address. . . . . . . . . : 28-D0-EA-40-B2-DA
    DHCP Enabled. . . . . . . . . . . : Yes
    Autoconfiguration Enabled . . . . : Yes
    IPv6 Address. . . . . . . . . . . : 2401:d800:111:6b9c:5685:e459:570e:e2c9(Preferred)
    Temporary IPv6 Address. . . . . . : 2401:d800:111:6b9c:745c:e8b2:28af:50c8(Preferred)
    IPv6 Address. . . . . . . . . . . : 2401:d800:7090:2101:596b:16ea:feaa:fea4(Deprecated)
    Temporary IPv6 Address. . . . . . : 2401:d800:7090:2101:756b:5516:41b6:dfaf(Deprecated)
    Link-local IPv6 Address . . . . . : fe80::a149:51ff:65ff:ff1d%11(Preferred)
    IPv4 Address. . . . . . . . . . . : 192.168.110.174(Preferred)
    Subnet Mask . . . . . . . . . . . : 255.255.255.0
    Lease Obtained. . . . . . . . . . : Wednesday, October 22, 2025 9:04:51 AM
    Lease Expires . . . . . . . . . . : Wednesday, October 22, 2025 5:04:36 PM
    Default Gateway . . . . . . . . . : fe80::805:2bff:fe12:463e%11
                                        192.168.110.177
    DHCP Server . . . . . . . . . . . : 192.168.110.177
    DHCPv6 IAID . . . . . . . . . . . : 170447082
    DHCPv6 Client DUID. . . . . . . . : 00-01-00-01-30-5D-45-01-8C-B0-E9-25-C3-B7
    DNS Servers . . . . . . . . . . . : 192.168.110.177
    NetBIOS over Tcpip. . . . . . . . : Enabled
```

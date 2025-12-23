## 🧩 BẢNG TỔNG HỢP CÁC GIAO THỨC

| **Protocol**    | **Port**          | **Chức năng chính**                    | **Tầng OSI**     | **Ghi chú / Ứng dụng trong pentest**                          |
| --------------- | ----------------- | -------------------------------------- | ---------------- | ------------------------------------------------------------- |
| **ICMP**        | N/A               | Kiểm tra kết nối, phản hồi mạng (ping) | Network (L3)     | Dùng trong host discovery (`ping`, `nmap -sn`)                |
| **ARP**         | N/A               | Ánh xạ IP ↔ MAC                        | Data Link (L2)   | Dùng để quét cục bộ (`arp -a`, `netdiscover`, `arp-scan`)     |
| **DNS**         | 53 (UDP/TCP)      | Phân giải tên miền ↔ IP                | Application (L7) | Dùng để xác định subdomain, zone transfer (`dig`, `dnsrecon`) |
| **DHCP**        | 67, 68 (UDP)      | Cấp IP tự động                         | Application (L7) | Có thể tấn công DHCP spoofing / rogue DHCP                    |
| **HTTP**        | 80 (TCP)          | Giao thức web không mã hóa             | Application (L7) | Thu thập banner, tấn công web (`nmap -sV`, `nikto`, `burp`)   |
| **HTTPS**       | 443 (TCP)         | Web bảo mật (SSL/TLS)                  | Application (L7) | Có thể kiểm tra chứng chỉ, sniff SSL handshake                |
| **FTP**         | 21 (TCP)          | Truyền file                            | Application (L7) | Thường có anonymous login hoặc lộ thông tin version           |
| **FTPS**        | 990 (TCP)         | FTP qua SSL/TLS                        | Application (L7) | Mã hóa, ít gặp trong bài thi eJPT                             |
| **SFTP**        | 22 (TCP, SSH)**   | FTP qua SSH                            | Application (L7) | Cùng port SSH, dùng key hoặc password                         |
| **SSH**         | 22 (TCP)          | Đăng nhập từ xa an toàn                | Application (L7) | Thường test brute-force (`hydra`, `nmap --script ssh-brute`)  |
| **Telnet**      | 23 (TCP)          | Đăng nhập từ xa không mã hóa           | Application (L7) | Dễ sniff credentials, ít dùng hiện nay                        |
| **SMTP**        | 25 (TCP)          | Gửi email                              | Application (L7) | Dò thông tin người dùng (`VRFY`, `EXPN`)                      |
| **POP3**        | 110 (TCP)         | Nhận email (tải về)                    | Application (L7) | Có thể test login, kiểm tra leak                              |
| **IMAP**        | 143 (TCP)         | Truy cập email trên server             | Application (L7) | Brute-force user/password                                     |
| **SMB**         | 139, 445 (TCP)    | Chia sẻ file/máy in trong Windows      | Application (L7) | Dò NetBIOS name, liệt kê share, khai thác EternalBlue         |
| **NetBIOS**     | 137–139 (TCP/UDP) | Dịch vụ đặt tên / chia sẻ trong LAN    | Session (L5)     | Dò thông tin host Windows (`nbtstat`, `nmap -p139`)           |
| **RDP**         | 3389 (TCP)        | Remote Desktop (Windows)               | Application (L7) | Thường brute-force hoặc kiểm tra CVE                          |
| **SNMP**        | 161, 162 (UDP)    | Quản lý thiết bị mạng                  | Application (L7) | Có thể leak info (`public`/`private` community string)        |
| **LDAP**        | 389 (TCP)         | Directory service (Active Directory)   | Application (L7) | Dò user / domain info (`ldapsearch`)                          |
| **LDAPS**       | 636 (TCP)         | LDAP bảo mật (SSL)                     | Application (L7) | Mã hóa, nhưng vẫn có thể enumerate                            |
| **MySQL**       | 3306 (TCP)        | CSDL MySQL                             | Application (L7) | Test login, dump DB (`mysql -u root -p`, `hydra`)             |
| **PostgreSQL**  | 5432 (TCP)        | CSDL PostgreSQL                        | Application (L7) | Giống MySQL, có thể enumerate                                 |
| **MSSQL**       | 1433 (TCP)        | CSDL SQL Server                        | Application (L7) | Dò user, brute-force, SQLi test                               |
| **NTP**         | 123 (UDP)         | Đồng bộ thời gian                      | Application (L7) | Dò version, info leak                                         |
| **TFTP**        | 69 (UDP)          | Truyền file đơn giản (no auth)         | Application (L7) | Thường bị cấu hình sai, dễ khai thác                          |
| **HTTP Proxy**  | 8080, 3128        | Proxy server                           | Application (L7) | Có thể dùng bypass filter                                     |
| **HTTPS Proxy** | 8443              | Proxy SSL                              | Application (L7) | Dùng cho burp suite, test redirect                            |
| **RPC / MSRPC** | 135 (TCP)         | Gọi tiến trình từ xa (Windows)         | Session (L5)     | Dò thông tin Windows host (`rpcdump`, `enum4linux`)           |
| **Kerberos**    | 88 (TCP/UDP)      | Authentication cho AD                  | Application (L7) | Tấn công “Pass-the-Ticket”, “AS-REP Roast”                    |
| **NFS**         | 2049 (TCP/UDP)    | File share trên Linux/Unix             | Application (L7) | Dò mount point (`showmount -e`)                               |
| **Rsync**       | 873 (TCP)         | Đồng bộ file                           | Application (L7) | Dò thư mục ẩn (`rsync -av --list-only`)                       |

---

Tốt — mình rút gọn lại **chỉ những protocol thật sự cần thiết cho eJPT**, mỗi mục rất ngắn gọn, kèm port, vì sao quan trọng trong bài lab/thi, và vài lệnh / tool bạn hay dùng với protocol đó. In được, học nhanh được.

---

## ✅ Danh sách **cần biết** cho eJPT (ngắn, thực tế)

| Protocol                 |               Port (mặc định) | Tại sao quan trọng cho eJPT                                              | Tool / lệnh hay dùng                                              |
| ------------------------ | ----------------------------: | ------------------------------------------------------------------------ | ----------------------------------------------------------------- |
| **ICMP**                 |                           N/A | Host discovery, kiểm tra reachability (ping/traceroute).                 | `ping`, `tracert`/`traceroute`, `nmap -sn`                        |
| **ARP**                  |                           N/A | Quét mạng LAN, ánh xạ IP↔MAC, dùng để phát hiện host cục bộ.             | `arp -a`, `arp-scan`, `netdiscover`                               |
| **DNS**                  |                  53 (UDP/TCP) | Domain → IP, subdomain enumeration, zone transfer (thử `AXFR`).          | `nslookup`, `dig`, `dnsrecon`                                     |
| **DHCP**                 |                   67/68 (UDP) | Cấp IP; hiểu lease/gateway; có thể bị rogue DHCP trong lab.              | `dhclient`, kiểm tra thông tin `ipconfig`/`ifconfig`              |
| **TCP (concept)**        |                             — | Kết nối đáng tin cậy; hiểu 3-way handshake; port-based service mapping.  | `nmap -sS -sV`, `netstat`, `tcpdump`                              |
| **UDP (concept)**        |                             — | Dịch vụ không kết nối (DNS, SNMP, NTP); scan UDP khác với TCP.           | `nmap -sU`, `nc -u`, `tshark`                                     |
| **HTTP / HTTPS**         |                80 / 443 (TCP) | Web app enumeration, banner, directory bruteforce, vuln scanning.        | `curl`, browser + Burp, `nikto`, `gobuster`                       |
| **SSH**                  |                      22 (TCP) | Remote access; brute-force credential testing; key-based auth.           | `ssh`, `hydra`, `nmap --script ssh*`                              |
| **FTP / SFTP**           |  21 (FTP), SFTP uses SSH (22) | File transfer; check anonymous login or exposed files.                   | `ftp`, `sftp`, `nmap -sV -p21`                                    |
| **SMB / NetBIOS**        |           445 / 139 / 137–139 | Windows shares, enumeration of users/shares, common exploitation vector. | `smbclient`, `smbmap`, `enum4linux`, `nmap -p 445 --script smb-*` |
| **RDP**                  |                    3389 (TCP) | Remote Desktop; brute-force / check for exposed RDP.                     | `rdesktop`, `xfreerdp`, `nmap -p3389`                             |
| **SNMP**                 |                     161 (UDP) | Quản trị thiết bị; public string leak có thể lộ cấu hình.                | `snmpwalk -c public`, `nmap --script snmp-*`                      |
| **LDAP**                 |                     389 (TCP) | Dò thông tin Active Directory (users, groups).                           | `ldapsearch`, `enum4linux`                                        |
| **MySQL / DBs (cơ bản)** | 3306 (MySQL), 5432 (Postgres) | Kiểm tra DB mở, login default, dump dữ liệu.                             | `mysql -h`, `psql`, `nmap -sV -p3306`                             |

---

## 🔎 Học theo ưu tiên (eJPT)

1. **Bắt buộc thuộc**: ICMP, ARP, DNS, TCP/UDP (khái niệm), HTTP/HTTPS, SSH, SMB.
2. **Nên biết**: DHCP, NetBIOS, RDP, SNMP.
3. **Biết khái quát**: LDAP, MySQL/Postgres (nếu lab có dịch vụ DB).

---

## 🛠️ Mẹo dùng trong lab

* Khi thấy port mở → **suy nghĩ theo checklist**: port → dịch vụ → banner → enumeration → brute-force / vuln search.
* Luôn dùng `nmap -sV -sC -p- <target>` để nhanh nhận diện dịch vụ và chạy NSE script cơ bản.
* Với SMB: thử `smbclient -L //<ip>` và `enum4linux -a <ip>`.
* Với web: dùng `gobuster` hoặc `dirb` để tìm directories; `curl -I` xem header.

---


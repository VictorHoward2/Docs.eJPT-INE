Lệnh Nmap cơ bản để thu thập thông tin dịch vụ và phiên bản trên máy mục tiêu:
```bash
nmap target.ine.local -sC -sV 
```

---

Version Detection (-sV): với các port mở, Nmap gửi các probe đặc biệt để lấy banner và xác định service + version, thỉnh thoảng thử nhiều probe để đoán chính xác.
Ví dụ kết quả:
- Thực tế:
    ┌──(kali㉿kali)-[~/Downloads]
    └─$ nmap svg-2m.com -sV    
    Starting Nmap 7.95 ( https://nmap.org ) at 2025-10-17 03:27 EDT
    Nmap scan report for svg-2m.com (14.225.254.197)
    Host is up (0.0095s latency).
    Not shown: 674 filtered tcp ports (no-response), 321 closed tcp ports (reset)
    PORT     STATE SERVICE       VERSION
    80/tcp   open  http          Node.js Express framework
    135/tcp  open  msrpc         Microsoft Windows RPC
    443/tcp  open  ssl/http      Node.js Express framework
    3389/tcp open  ms-wbt-server Microsoft Terminal Services
    5985/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
    Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

    Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
    Nmap done: 1 IP address (1 host up) scanned in 49.69 seconds

- Trong Lab CTF1:
    ┌──(root㉿INE)-[~/CTF1/target.ine.local]
    └─# nmap target.ine.local -sV
    Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-10-17 13:11 IST
    Nmap scan report for target.ine.local (192.90.185.3)
    Host is up (0.000027s latency).
    Not shown: 999 closed tcp ports (reset)
    PORT   STATE SERVICE VERSION
    80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
    MAC Address: 02:42:C0:5A:B9:03 (Unknown)

    Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
    Nmap done: 1 IP address (1 host up) scanned in 6.69 seconds

---

NSE default scripts (-sC): chạy nhóm script mặc định (equivalent --script=default) trên các mục tiêu/port phù hợp để thu thập thêm thông tin (ví dụ: banner grabbing, HTTP title, ssl-cert, basic vuln check, smb-info, v.v.).

    🧩 NSE là gì? 
    NSE (Nmap Scripting Engine) là hệ thống cho phép Nmap tự động hóa các tác vụ quét và khai thác bằng cách sử dụng các script viết bằng ngôn ngữ Lua.

    Nói đơn giản:
    NSE là “bộ não mở rộng” của Nmap — giúp nó không chỉ quét port mà còn hiểu service, tìm lỗ hổng, thu thập thông tin chi tiết, thậm chí tấn công nhẹ (trong lab hợp pháp).

    🔍 Vai trò của NSE
    Khi không có NSE, Nmap chỉ làm được việc cơ bản:
        Phát hiện host đang hoạt động
        Quét port mở
        Nhận dạng service (-sV)

    Khi có NSE, Nmap có thể:
        Thu thập thông tin sâu hơn (version chi tiết, cấu hình, banner, title web)
        Kiểm tra lỗ hổng bảo mật (ví dụ CVE cụ thể)
        Thực hiện brute-force password trên một số dịch vụ (FTP, SSH…)
        Phân tích giao thức (SNMP, SMB, HTTP, MySQL, v.v.)
        Tự động khai thác (một số script “exploit” có thể gửi payload nhẹ)
Ví dụ kết quả:
- Thực tế:
    ┌──(kali㉿kali)-[~/Downloads]
    └─$ nmap svg-2m.com -sC
    Starting Nmap 7.95 ( https://nmap.org ) at 2025-10-17 03:32 EDT
    Nmap scan report for svg-2m.com (14.225.254.197)
    Host is up (0.00077s latency).
    Not shown: 752 filtered tcp ports (no-response), 243 closed tcp ports (reset)
    PORT     STATE SERVICE
    80/tcp   open  http
    |_http-title: Error
    135/tcp  open  msrpc
    443/tcp  open  https
    |_http-title: GeoData V2
    |_ssl-date: TLS randomness does not represent time
    | ssl-cert: Subject: commonName=svg-2m.com
    | Subject Alternative Name: DNS:svg-2m.com
    | Not valid before: 2025-08-30T04:44:53
    |_Not valid after:  2025-11-28T04:44:52
    | tls-alpn: 
    |_  http/1.1
    3389/tcp open  ms-wbt-server
    |_ssl-date: 2025-10-17T07:37:16+00:00; -1s from scanner time.
    | rdp-ntlm-info: 
    |   Target_Name: VPSSVG-2M2025-Q
    |   NetBIOS_Domain_Name: VPSSVG-2M2025-Q
    |   NetBIOS_Computer_Name: VPSSVG-2M2025-Q
    |   DNS_Domain_Name: vpssvg-2m2025-q
    |   DNS_Computer_Name: vpssvg-2m2025-q
    |   Product_Version: 10.0.19041
    |_  System_Time: 2025-10-17T07:37:16+00:00
    | ssl-cert: Subject: commonName=vpssvg-2m2025-q
    | Not valid before: 2025-07-11T07:32:04
    |_Not valid after:  2026-01-10T07:32:04
    5985/tcp open  wsman

    Host script results:
    |_clock-skew: mean: -1s, deviation: 0s, median: -1s

    Nmap done: 1 IP address (1 host up) scanned in 321.81 seconds
- Trong Lab CTF1:
    ┌──(root㉿INE)-[~]
    └─# nmap target.ine.local -sC
    Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-10-17 13:26 IST
    Nmap scan report for target.ine.local (192.90.185.3)
    Host is up (0.000029s latency).
    Not shown: 999 closed tcp ports (reset)
    PORT   STATE SERVICE
    80/tcp open  http
    | http-robots.txt: 1 disallowed entry 
    |_/wp-admin/
    |_http-title: INE
    |_http-generator: WordPress 6.5.3 - FL@G2{04401329a65d4d8d83af68267efcece0}
    MAC Address: 02:42:C0:5A:B9:03 (Unknown)

    Nmap done: 1 IP address (1 host up) scanned in 1.81 seconds

---

Kết hợp 2 lệnh: 

    ┌──(root㉿INE)-[~]
    └─# nmap target.ine.local -sC -sV
    Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-10-17 13:36 IST                                                                                                                                                                         
    Nmap scan report for target.ine.local (192.90.185.3)                                                                                                                                                                                       
    Host is up (0.000029s latency).                                                                                                                                                                                                            
    Not shown: 999 closed tcp ports (reset)                                                                                                                                                                                                    
    PORT   STATE SERVICE VERSION
    80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
    |_http-generator: WordPress 6.5.3 - FL@G2{04401329a65d4d8d83af68267efcece0}
    |_http-server-header: Apache/2.4.41 (Ubuntu)
    |_http-title: INE
    | http-robots.txt: 1 disallowed entry 
    |_/wp-admin/
    MAC Address: 02:42:C0:5A:B9:03 (Unknown)

    Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
    Nmap done: 1 IP address (1 host up) scanned in 8.18 seconds



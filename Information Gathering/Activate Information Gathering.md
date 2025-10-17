# 🎯 Active Information Gathering

> **Thu thập thông tin chủ động - Tương tác trực tiếp với mục tiêu để thu thập dữ liệu**

## 📋 Table of Contents
- [DNS Zone Transfers](#dns-zone-transfers)
- [Host Discovery With Nmap](#host-discovery-with-nmap)
- [Port Scanning With Nmap](#port-scanning-with-nmap)
- [Service Enumeration](#service-enumeration)
- [Vulnerability Scanning](#vulnerability-scanning)
- [Web Application Testing](#web-application-testing)

---

## 🌐 DNS Zone Transfers

### 📖 Tổng quan
Zone transfer (AXFR / IXFR) là cơ chế DNS cho phép sao chép toàn bộ zone (bản ghi DNS) từ một nameserver gốc sang một secondary nameserver. 

**🎯 Mục đích hợp pháp:** Đồng bộ hóa DNS giữa primary và secondary nameserver.

**⚠️ Rủi ro bảo mật:** Khi được mở cho công chúng (misconfiguration), attacker có thể yêu cầu AXFR và nhận toàn bộ bản ghi DNS — lộ subdomain, host nội bộ, IP, mail servers, TXT/SRV, v.v.

### 🔧 Các loại zone transfer
- **AXFR** — Full zone transfer (toàn bộ zone)
- **IXFR** — Incremental zone transfer (chỉ các thay đổi)

> **💡 Lưu ý:** Trong pentest, ta kiểm tra AXFR; nếu AXFR được phép thì attacker có đủ thông tin.

### 🛠️ Các lệnh kiểm tra phổ biến

#### 1. **Dig (thường dùng nhất)**
```bash
# Cú pháp cơ bản
dig @<nameserver> <domain> AXFR

# Ví dụ thực tế
dig @ns1.target.com target.com AXFR
dig @8.8.8.8 example.com AXFR

# Kiểm tra nhiều nameserver
dig @ns1.target.com target.com AXFR
dig @ns2.target.com target.com AXFR
dig @ns3.target.com target.com AXFR
```

#### 2. **Nslookup (interactive mode)**
```bash
# Chế độ interactive
nslookup
> server ns1.target.com
> set type=any
> ls -d target.com
> exit

# Hoặc dùng command line
nslookup -type=any target.com ns1.target.com
```

#### 3. **Host command**
```bash
# Cú pháp cơ bản
host -l target.com ns1.target.com

# Với verbose output
host -l -v target.com ns1.target.com
```

#### 4. **Sử dụng Fierce (automated tool)**
```bash
# Cài đặt fierce
sudo apt install fierce

# Chạy fierce
fierce -dns target.com
fierce -dns target.com -wordlist /usr/share/wordlists/dnsmap.txt
```

### 📊 Diễn giải kết quả

**✅ Zone transfer thành công:**
```
target.com.            3600    IN      A       192.168.1.10
mail.target.com.       3600    IN      A       192.168.1.20
admin.target.com.      3600    IN      A       192.168.1.30
db.target.com.         3600    IN      A       192.168.1.40
```

**❌ Zone transfer bị từ chối:**
```
; Transfer failed.
```

### 🎯 Ví dụ thực tế
```bash
# Kiểm tra zone transfer cho một domain
dig @ns1.google.com google.com AXFR
# Kết quả: Transfer failed (Google bảo mật tốt)

# Kiểm tra với domain test
dig @ns1.example.com example.com AXFR
# Có thể thành công với domain test
```

---

## 🔍 Host Discovery With Nmap

### 🎯 Mục tiêu
- Xác định host nào đang hoạt động (alive) trong một dải IP
- Giảm scope quét, tiết kiệm thời gian
- Tránh quét những host không tồn tại

### ⚙️ Các option quan trọng

| Option | Mô tả | Khi nào dùng |
|--------|--------|--------------|
| `-sn` | Ping scan (trước kia là -sP) | Scan cơ bản, nhanh |
| `-sL` | List scan (không gửi gói) | Chỉ liệt kê IP, không scan |
| `-Pn` | Tắt host discovery | Khi firewall block ping |
| `-PR` | ARP ping (chỉ LAN) | Scan mạng nội bộ |
| `-PE, -PP` | ICMP Echo / Timestamp ping | Khi cần ICMP |
| `-PS/-PA/-PU` | TCP SYN/ACK/UDP pings | Khi ICMP bị chặn |

### 🚀 Lệnh mẫu thực tế

#### 1. **Ping scan cơ bản**
```bash
# Scan một subnet
nmap -sn 10.10.10.0/24 -oA lab_hostdiscovery_basic

# Scan với timing template
nmap -sn -T4 10.10.10.0/24 -oA fast_scan

# Scan với verbose output
nmap -sn -v 10.10.10.0/24
```

#### 2. **ARP scan trên LAN**
```bash
# ARP scan cơ bản
sudo nmap -sn -PR 192.168.1.0/24 -oA lan_arp_scan

# ARP scan với timing
sudo nmap -sn -PR -T4 192.168.1.0/24
```

#### 3. **TCP SYN pings khi ICMP bị chặn**
```bash
# TCP SYN ping với port phổ biến
nmap -sn -PS80,443 10.10.10.0/24 -oA hostdiscovery_tcp

# TCP SYN ping với nhiều port
nmap -sn -PS22,80,443,8080 10.10.10.0/24

# TCP ACK ping
nmap -sn -PA80,443 10.10.10.0/24
```

#### 4. **Dùng danh sách targets từ file**
```bash
# Tạo file targets.txt
echo "10.10.10.1" > targets.txt
echo "10.10.10.2" >> targets.txt
echo "10.10.10.3" >> targets.txt

# Scan từ file
nmap -sn -iL targets.txt --host-timeout 30s -oA from_list
```

#### 5. **Khi muốn treat all as up**
```bash
# Bỏ discovery, scan tất cả
nmap -Pn -p 80,443 -iL targets.txt -oA all_assumed_up

# Chú ý: sẽ chạy port scan trên mọi host → lâu hơn
```

### 📈 Workflow thực tế
1. **Host discovery** → `live_hosts.txt`
2. **Quick scan** (top ports)
3. **Full scan** cho hosts quan trọng
4. **UDP scan** nếu cần
5. **NSE scripts** phù hợp
6. **Tổng hợp và phân tích** kết quả

---

## 🔌 Port Scanning With Nmap

### 🔧 Các kiểu scan cơ bản

| Kiểu Scan | Flag | Mô tả | Ưu điểm | Nhược điểm |
|-----------|------|--------|---------|------------|
| SYN scan | `-sS` | Stealth scan, nhanh | Nhanh, stealth | Cần root |
| TCP connect | `-sT` | Dùng TCP connect() của OS | Không cần root | Chậm hơn, dễ phát hiện |
| UDP scan | `-sU` | Phát hiện dịch vụ UDP | Phát hiện UDP services | Rất chậm |
| Version detection | `-sV` | Dò phiên bản dịch vụ | Chi tiết về service | Chậm hơn |
| Script scan | `-sC` | Chạy NSE default scripts | Tự động hóa | Có thể noisy |

### 🎯 Workflow thực tế
1. **Host discovery** → `live_hosts.txt`
2. **Quick scan** (top ports)
3. **Full scan** cho hosts quan trọng
4. **UDP scan** nếu cần
5. **NSE scripts** phù hợp
6. **Tổng hợp và phân tích** kết quả

### 📊 Diễn giải trạng thái port
- **open**: Port có service đang chạy
- **closed**: Port không có service
- **filtered**: Bị firewall chặn
- **open\|filtered**: Không xác định được (thường ở UDP)

### 🚀 Lệnh scan thực tế

#### 1. **Quick scan (top ports)**
```bash
# Scan top 1000 ports
nmap -sS -T4 target.com -oA quick_scan

# Scan top 100 ports
nmap -sS -T4 --top-ports 100 target.com
```

#### 2. **Full port scan**
```bash
# Scan tất cả 65535 ports
nmap -sS -T4 -p- target.com -oA full_scan

# Scan với version detection
nmap -sS -sV -T4 -p- target.com -oA full_version_scan
```

#### 3. **UDP scan**
```bash
# UDP scan top ports
nmap -sU -T4 --top-ports 1000 target.com -oA udp_scan

# UDP scan specific ports
nmap -sU -T4 -p 53,67,68,69,123,161,162,500,514 target.com
```

#### 4. **Script scan**
```bash
# Default scripts
nmap -sC -sV target.com -oA script_scan

# Specific script categories
nmap --script vuln target.com
nmap --script safe target.com
nmap --script discovery target.com
```

---

## 🔍 Service Enumeration

### 🛠️ Công cụ và kỹ thuật

#### 1. **Banner Grabbing**
```bash
# Telnet
telnet target.com 80
GET / HTTP/1.1
Host: target.com

# Netcat
nc target.com 80
GET / HTTP/1.1
Host: target.com

# Nmap
nmap -sV -sC target.com
```

#### 2. **Service-specific enumeration**
```bash
# SSH
ssh -V target.com
nmap --script ssh-hostkey target.com

# FTP
nmap --script ftp-anon target.com
nmap --script ftp-bounce target.com

# SMB
nmap --script smb-enum-shares target.com
nmap --script smb-vuln-* target.com
```

---

## 🛡️ Vulnerability Scanning

### 🔧 Công cụ vulnerability scanning

#### 1. **Nmap NSE Scripts**
```bash
# Vulnerability scripts
nmap --script vuln target.com

# Safe scripts only
nmap --script safe target.com

# Specific vulnerability
nmap --script smb-vuln-ms17-010 target.com
```

#### 2. **Nessus**
- Commercial vulnerability scanner
- Comprehensive vulnerability database
- Web-based interface

#### 3. **OpenVAS**
```bash
# Install OpenVAS
sudo apt install openvas

# Setup
sudo gvm-setup

# Access web interface
https://localhost:9392
```

---

## 🌐 Web Application Testing

### 🔍 Web reconnaissance
```bash
# Directory enumeration
gobuster dir -u http://target.com -w /usr/share/wordlists/dirb/common.txt

# Subdomain enumeration
gobuster vhost -u target.com -w /usr/share/wordlists/subdomains-top1million-5000.txt

# Technology detection
whatweb http://target.com
wappalyzer http://target.com
```

### 🛠️ Web vulnerability scanning
```bash
# Nikto
nikto -h http://target.com

# OWASP ZAP
zap.sh -cmd -quickurl http://target.com -quickprogress

# Burp Suite
# Manual testing với Burp Suite Professional
```

---

## 📝 Best Practices

### ✅ Do's
- **Luôn có authorization** trước khi scan
- **Sử dụng timing phù hợp** (-T4 cho scan nhanh, -T2 cho scan stealth)
- **Ghi chép đầy đủ** các lệnh và kết quả
- **Bắt đầu với scan nhẹ** trước khi scan sâu
- **Sử dụng output files** (-oA, -oN, -oG, -oX)

### ❌ Don'ts
- **Không scan** hệ thống không được phép
- **Không sử dụng** timing quá aggressive (-T5)
- **Không bỏ qua** việc phân tích kết quả
- **Không scan** production systems trong giờ cao điểm

### 📊 Output Formats
```bash
# All formats
nmap -sS target.com -oA scan_results

# Specific formats
nmap -sS target.com -oN normal_output.txt    # Normal
nmap -sS target.com -oG grepable_output.txt  # Grepable
nmap -sS target.com -oX xml_output.xml       # XML
```

---

## 🎯 Ví dụ thực tế hoàn chỉnh

### Scenario: Pentest một web server
```bash
# 1. Host discovery
nmap -sn 192.168.1.0/24 -oA host_discovery

# 2. Port scan
nmap -sS -T4 192.168.1.100 -oA port_scan

# 3. Service enumeration
nmap -sV -sC 192.168.1.100 -oA service_enum

# 4. Web reconnaissance
gobuster dir -u http://192.168.1.100 -w /usr/share/wordlists/dirb/common.txt

# 5. Vulnerability scan
nmap --script vuln 192.168.1.100 -oA vuln_scan
```

> **💡 Pro Tip:** Luôn ghi chép đầy đủ các lệnh scan và kết quả để tham khảo sau và tạo báo cáo pentest.
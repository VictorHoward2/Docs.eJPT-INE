# 🔍 Passive Information Gathering

> **Thu thập thông tin thụ động - Không tương tác trực tiếp với mục tiêu để tránh bị phát hiện**

## 📋 Table of Contents
- [Overview](#overview)
- [Recon vs Footprinting](#recon-vs-footprinting)
- [Web Discovery Tools](#web-discovery-tools)
- [DNS Tools & Techniques](#dns-tools--techniques)
- [OSINT Tools](#osint-tools)
- [Social Media Intelligence](#social-media-intelligence)
- [Search Engine Techniques](#search-engine-techniques)
- [Advanced Techniques](#advanced-techniques)
- [Automation Tools](#automation-tools)
- [Best Practices](#best-practices)

---

## 📖 Overview

Cả **Website Reconnaissance (Recon)** và **Footprinting** đều nằm trong **giai đoạn đầu tiên của tấn công (Information Gathering)**.
Mục tiêu chung: **thu thập thông tin về mục tiêu** trước khi tấn công.

Tuy nhiên:

* ⚙️ **Footprinting** là **bức tranh tổng thể** – thu thập mọi thông tin có thể về **tổ chức hoặc mục tiêu**.
* 🌐 **Website Recon** là **một phần nhỏ hơn** của Footprinting – tập trung vào **website cụ thể** (ứng dụng web).

### 🎯 Mục tiêu của Passive Reconnaissance
- **Thu thập thông tin** mà không để lại dấu vết
- **Xác định attack surface** của mục tiêu
- **Tìm hiểu về tổ chức** và cơ sở hạ tầng
- **Phát hiện lỗ hổng** từ thông tin công khai

---

## 🔄 Recon vs Footprinting

| Tiêu chí                    | **Footprinting**                                                          | **Website Reconnaissance**                                                |
| --------------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| **Mục tiêu**                | Tìm hiểu toàn bộ về tổ chức, mạng, domain, email, nhân sự, hạ tầng IT     | Tập trung vào website cụ thể của mục tiêu                                 |
| **Phạm vi**                 | Rộng (domain, subdomain, IP range, ASN, mạng nội bộ, nhân viên, DNS, MX…) | Hẹp hơn (trang web, cấu trúc thư mục, công nghệ, lỗ hổng web)             |
| **Ví dụ công cụ**           | Whois, nslookup, Maltego, recon-ng, theHarvester                          | Wappalyzer, Burp Suite, OWASP ZAP, Nikto, dirb, gobuster                  |
| **Kiểu thông tin thu thập** | Domain info, IP, DNS records, email servers, tên nhân viên, đối tác, v.v. | Framework, CMS, plugin, phiên bản server, file robots.txt, subdirectories |
| **Mục đích cuối cùng**      | Xác định toàn cảnh về mục tiêu để lên kế hoạch tấn công                   | Xác định lỗ hổng hoặc entry point trên web app                            |

---

## 🌐 Web Discovery Tools

### 🤖 robots.txt Analysis
Robots.txt là file cấu hình chỉ thị cho web crawlers.

**Điểm cần chú ý:**
- Thường chứa đường dẫn nhạy cảm (`/admin`, `/backup`)
- Không phải cơ chế bảo mật - chỉ là "hướng dẫn" cho bots
- Kiểm tra các path chứa:
  - Config files (`/config`, `/settings`)
  - Database dumps (`/backup`, `/dump`)
  - Admin consoles (`/admin`, `/administrator`)
  - Development endpoints (`/dev`, `/test`, `/staging`)

**Cách kiểm tra:**
```bash
# Truy cập trực tiếp
curl http://target.com/robots.txt

# Sử dụng wget
wget http://target.com/robots.txt

# Phân tích với grep
curl -s http://target.com/robots.txt | grep -E "(Disallow|Allow)"
```

### 🗺️ sitemap.xml Review
**Mục đích:** File XML liệt kê URLs để search engines index

**Các điểm quan trọng:**
- Chứa danh sách URLs đầy đủ
- Có thể tìm thấy endpoints ẩn
- Kiểm tra cả sitemap index và sub-sitemaps
- Tìm staging/test URLs

**Cách kiểm tra:**
```bash
# Truy cập sitemap
curl http://target.com/sitemap.xml

# Tìm tất cả sitemaps
curl -s http://target.com/sitemap.xml | grep -o 'https\?://[^<]*\.xml'

# Phân tích với xmllint
curl -s http://target.com/sitemap.xml | xmllint --format -
```

### 🔍 Directory Enumeration (Passive)
```bash
# Sử dụng công cụ online
# - dirb online
# - dirbuster online
# - gobuster online

# Hoặc sử dụng search engines
site:target.com inurl:admin
site:target.com inurl:backup
site:target.com inurl:config
```

---

## 🌐 DNS Tools & Techniques

### 📋 Whois Enumeration
| Thông tin | Mô tả | Ví dụ |
|-----------|--------|--------|
| Registrar | Nhà đăng ký tên miền | GoDaddy, Namecheap |
| Contacts | Email/phone liên hệ | admin@domain.com |
| Nameservers | DNS servers | ns1.example.com |
| Dates | Ngày tạo/hết hạn | Created: 2020-01-01 |
| Organization | Tổ chức sở hữu | Example Corp |

**Các lệnh Whois:**
```bash
# Whois cơ bản
whois target.com

# Whois với IP
whois 192.168.1.1

# Whois với ASN
whois -h whois.arin.net AS12345

# Sử dụng online tools
# - whois.net
# - whois.domaintools.com
# - whois.icann.org
```

### 🔎 DNS Reconnaissance 
**Các loại bản ghi quan trọng:**
```bash
# A/AAAA - IP mapping
dig target.com A
dig target.com AAAA

# MX - Mail servers
dig target.com MX

# TXT - SPF, DKIM records
dig target.com TXT

# NS - Nameservers
dig target.com NS

# CNAME - Canonical names
dig www.target.com CNAME

# PTR - Reverse DNS
dig -x 192.168.1.1

# SOA - Start of Authority
dig target.com SOA
```

**Công cụ DNS enumeration:**
```bash
# DNSenum
dnsenum target.com

# DNSrecon
dnsrecon -d target.com

# Fierce
fierce -dns target.com

# Sublist3r
sublist3r -d target.com
```

### 🔍 Subdomain Discovery
```bash
# Sublist3r
sublist3r -d target.com -t 10

# Amass
amass enum -d target.com

# Assetfinder
assetfinder target.com

# Subfinder
subfinder -d target.com

# Crt.sh (online)
# https://crt.sh/?q=target.com
```

---

## 🔍 OSINT Tools

### 🌐 Netcraft
**Thông tin thu thập:**
- Web server details
- Hosting history
- SSL certificates
- Technologies used
- Security reports

**Cách sử dụng:**
- Truy cập: https://netcraft.com
- Nhập domain vào search box
- Xem Site Report để có thông tin chi tiết

### 📧 theHarvester
```bash
# Cài đặt
sudo apt install theharvester

# Basic email scan
theHarvester -d target.com -b all

# Detailed scan with custom source
theHarvester -d target.com -b google,linkedin -l 500

# Scan với specific sources
theHarvester -d target.com -b bing,duckduckgo -l 1000

# Export kết quả
theHarvester -d target.com -b all -f results.html
```

### 🔑 Password Database Leaks
**Nguồn kiểm tra:**
- **HaveIBeenPwned**: https://haveibeenpwned.com
- **DeHashed**: https://dehashed.com
- **LeakCheck**: https://leakcheck.io
- **BreachDirectory**: https://breachdirectory.org

**Công cụ command line:**
```bash
# H8mail
pip install h8mail
h8mail -t target@domain.com

# LeakLookup
pip install leaklookup
leaklookup -e target@domain.com
```

### 🏢 Company Information
**Các nguồn thông tin:**
- **LinkedIn**: Thông tin nhân viên, cơ cấu tổ chức
- **Crunchbase**: Thông tin startup, funding
- **Glassdoor**: Thông tin công ty, đánh giá
- **SEC Filings**: Báo cáo tài chính (Mỹ)

---

## 📱 Social Media Intelligence

### 🔍 Social Media Reconnaissance
**Các platform quan trọng:**
- **LinkedIn**: Thông tin chuyên nghiệp
- **Twitter**: Thông tin real-time
- **Facebook**: Thông tin cá nhân
- **Instagram**: Hình ảnh, location
- **GitHub**: Code repositories

**Công cụ:**
```bash
# Social-Engineer Toolkit (SET)
setoolkit

# Maltego
# Commercial tool với free version

# Recon-ng
recon-ng
workspaces create target_company
modules load recon/contacts-contacts/linkedin_auth
```

### 👥 Employee Information
**Thông tin cần thu thập:**
- Tên nhân viên
- Chức vụ
- Email addresses
- Phone numbers
- Social media profiles
- Skills và certifications

---

## 🔍 Search Engine Techniques

### 🛡️ WAF Detection (wafw00f)
```bash
# Cài đặt
sudo apt install wafw00f

# Basic scan
wafw00f https://target.com

# Detailed analysis
wafw00f -a -v https://target.com

# Scan multiple URLs
wafw00f -i urls.txt
```

### 🔍 Google Dorking
| Operator | Usage | Example |
|----------|-------|---------|
| site: | Tìm trong domain | `site:target.com password` |
| filetype: | Tìm file type | `filetype:pdf site:target.com` |
| intitle: | Tìm trong title | `intitle:"admin login"` |
| inurl: | Tìm trong URL | `inurl:admin site:target.com` |
| intext: | Tìm trong nội dung | `intext:"error" site:target.com` |
| cache: | Xem cached version | `cache:target.com` |
| related: | Tìm site liên quan | `related:target.com` |

**Ví dụ Google Dorks:**
```bash
# Tìm admin panels
site:target.com inurl:admin
site:target.com intitle:"admin login"

# Tìm file config
site:target.com filetype:conf
site:target.com filetype:ini

# Tìm backup files
site:target.com filetype:bak
site:target.com filetype:sql

# Tìm error messages
site:target.com intext:"error"
site:target.com intext:"warning"
```

### 🔍 Shodan
**Thông tin thu thập:**
- Open ports và services
- SSL certificates
- Vulnerabilities
- Geographic location
- Historical data

**Cách sử dụng:**
- Truy cập: https://shodan.io
- Search với: `hostname:target.com`
- Sử dụng filters: `port:80,443`

### 🔍 Censys
**Tương tự Shodan:**
- Truy cập: https://censys.io
- Search với domain hoặc IP
- Xem certificates và services

---

## 🛠️ Advanced Techniques

### 🔍 Certificate Transparency Logs
**Các nguồn:**
- **Crt.sh**: https://crt.sh
- **Certificate Search**: https://censys.io/certificates
- **Google CT**: https://crt.sh

**Cách sử dụng:**
```bash
# Sử dụng crt.sh API
curl "https://crt.sh/?q=target.com&output=json"

# Sử dụng certspotter
certspotter -d target.com
```

### 🔍 Archive.org (Wayback Machine)
**Thông tin thu thập:**
- Historical versions của website
- Deleted pages
- Old configurations
- Previous technologies

**Cách sử dụng:**
- Truy cập: https://web.archive.org
- Nhập URL: `target.com`
- Xem timeline của changes

### 🔍 GitHub/GitLab Reconnaissance
**Tìm kiếm:**
- API keys
- Passwords
- Config files
- Source code
- Commits với sensitive data

**Công cụ:**
```bash
# GitLeaks
gitleaks detect --source . --verbose

# TruffleHog
trufflehog git https://github.com/target/repo

# GitDorker
gitdorker -tf targets.txt -d dorks.txt -o results.txt
```

---

## 🤖 Automation Tools

### 🔧 Recon-ng
```bash
# Cài đặt
sudo apt install recon-ng

# Khởi động
recon-ng

# Tạo workspace
workspaces create target_recon

# Load modules
modules load recon/domains-hosts/hackertarget
modules load recon/domains-hosts/shodan_hostname

# Chạy modules
run
```

### 🔧 Maltego
**Features:**
- Visual reconnaissance
- Data correlation
- Entity relationships
- Transform chains

**Cách sử dụng:**
- Download từ: https://maltego.com
- Tạo free account
- Sử dụng transforms để thu thập data

### 🔧 SpiderFoot
```bash
# Cài đặt
pip install spiderfoot

# Chạy web interface
spiderfoot -l 127.0.0.1:5001

# Command line
spiderfoot -s target.com -t all
```

---

## 📝 Best Practices

### ✅ Do's
- **Luôn bắt đầu với passive recon** trước khi active
- **Sử dụng nhiều nguồn** để cross-reference thông tin
- **Ghi chép đầy đủ** tất cả findings
- **Tổ chức thông tin** theo categories
- **Verify thông tin** từ multiple sources

### ❌ Don'ts
- **Không dựa vào một nguồn** duy nhất
- **Không bỏ qua** thông tin có vẻ không quan trọng
- **Không lưu trữ** sensitive data không cần thiết
- **Không chia sẻ** thông tin với unauthorized parties

### 📊 Information Organization
```bash
# Tạo cấu trúc thư mục
mkdir -p recon/{domains,ips,emails,employees,social,web}

# Lưu trữ findings
echo "Finding" >> recon/domains/target.com.txt
echo "IP: 192.168.1.1" >> recon/ips/target_ips.txt
```

### 🔄 Workflow
1. **Domain enumeration** → Subdomains, DNS records
2. **Company research** → Employees, structure, history
3. **Social media** → Profiles, posts, connections
4. **Technical info** → Technologies, infrastructure
5. **Vulnerability research** → Known issues, patches
6. **Documentation** → Organize và analyze findings

---

## 🎯 Ví dụ thực tế

### Scenario: Recon một startup
```bash
# 1. Domain research
whois startup.com
dig startup.com ANY
sublist3r -d startup.com

# 2. Company research
# LinkedIn, Crunchbase, Glassdoor

# 3. Employee enumeration
theHarvester -d startup.com -b linkedin
recon-ng modules load recon/contacts-contacts/linkedin_auth

# 4. Social media
# Twitter, Facebook, Instagram của company và employees

# 5. Technical reconnaissance
shodan hostname:startup.com
wafw00f https://startup.com
whatweb https://startup.com

# 6. GitHub reconnaissance
# Tìm repositories của company và employees
```

> **💡 Pro Tip:** Kết hợp nhiều tools và sources để có bức tranh toàn diện về mục tiêu. Luôn verify thông tin từ multiple sources.
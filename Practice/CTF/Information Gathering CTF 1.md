# 🎯 Information Gathering CTF Lab 1

## 📋 Lab Overview
Skill Check Labs là bài thực hành tương tác để kiểm tra kiến thức qua các tình huống thực tế. Không có solutions có sẵn, điểm số sẽ được chấm để theo dõi tiến độ học tập.

## 🎮 Lab Environment
Website mục tiêu: `http://target.ine.local`

### 🛠️ Tools Required
| Tool | Purpose |
|------|---------|
| Firefox | Web browsing và inspection |
| Curl | Request HTTP từ command line |
| HTTrack | Mirror Website |
| nmap | Network Scanning, Service Detection |
| dirsearch | Directory brute-forcing -> File Enumeration |
| dirb | Directory brute-forcing -> Path Enumeration |

### 🚩 Flags Overview
| Flag | Description |
|------|-------------|
| Flag 1 | Tìm file chỉ dẫn cho search engines |
| Flag 2 | Xác định website và version |
| Flag 3 | Tìm directory có thể browse |
| Flag 4 | Tìm file backup nhạy cảm |
| Flag 5 | Tìm thông tin trong mirror site |

## 💡 Hướng Dẫn Giải

### 🏁 Flag 1: Robots.txt
**Mục tiêu:** Tìm file chỉ dẫn cho search engines
```bash
# Đơn giản truy cập
curl http://target.ine.local/robots.txt
```

### 🏁 Flag 2: Website Version
**Mục tiêu:** Xác định loại website và phiên bản
```bash
# Sử dụng nmap với service detection
nmap target.ine.local -sC -sV
```

### 🏁 Flag 3: Directory Browsing
**Mục tiêu:** Tìm directory có thể browse
```bash
# Cách 1: Sử dụng dirsearch
dirsearch -u http://target.ine.local/

# Cách 2: Sử dụng dirb
dirb http://target.ine.local/
```
> 💡 **Kết quả:** `/wp-content/uploads/`

### 🏁 Flag 4: Backup Files
**Mục tiêu:** Tìm file backup trong webroot
```bash
# Bước 1: Tìm file với dirsearch
dirsearch -u http://target.ine.local/

# Bước 2: Đọc nội dung file wp-config.bak
curl http://target.ine.local/wp-config.bak
```

### 🏁 Flag 5: Website Mirroring
**Mục tiêu:** Tìm thông tin trong mirror site
```bash
# Bước 1: Mirror toàn bộ site
httrack http://target.ine.local/ -O mirror_site

# Bước 2: Đọc file chứa flag
cd mirror_site/target.ine.local
cat xmlrpc0db0.php
```

## 📝 Tips
- Luôn lưu lại output của các lệnh scan
- Kiểm tra kỹ các file được tìm thấy
- Directory browsing thường là dấu hiệu của misconfiguration
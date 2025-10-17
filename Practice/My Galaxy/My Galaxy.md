# 🌌 My Galaxy - Practice Targets

> **Danh sách các mục tiêu thực hành và ghi chú trong quá trình học eJPT**

## 📋 Table of Contents
- [Target Domains](#target-domains)
- [Practice Methodology](#practice-methodology)
- [Findings & Notes](#findings--notes)
- [Tools Used](#tools-used)
- [Lessons Learned](#lessons-learned)

---

## 🎯 Target Domains

### 1. Samsung LSS (samsung-lss.com)
**Mô tả:** Samsung Life Science Solutions - Cổng thông tin về các giải pháp khoa học đời sống của Samsung

**Thông tin cơ bản:**
- **Domain:** samsung-lss.com
- **Type:** Corporate website
- **Industry:** Life Sciences, Healthcare Technology
- **Status:** Active

**Reconnaissance Results:**
```bash
# DNS Information
dig samsung-lss.com A
# Result: [IP Address]

dig samsung-lss.com MX
# Result: [Mail servers]

# Subdomain Discovery
sublist3r -d samsung-lss.com
# Results: [Subdomains found]

# Technology Stack
whatweb https://samsung-lss.com
# Results: [Technologies detected]
```

**Key Findings:**
- [ ] Web server type and version
- [ ] CMS/Framework used
- [ ] SSL certificate details
- [ ] Subdomains discovered
- [ ] Email servers
- [ ] Social media presence

---

### 2. Samsung My Galaxy (samsung-mygalaxy.com)
**Mô tả:** Samsung My Galaxy - Cổng dịch vụ và hỗ trợ cho người dùng Samsung Galaxy

**Thông tin cơ bản:**
- **Domain:** samsung-mygalaxy.com
- **Type:** Customer support portal
- **Industry:** Consumer Electronics, Mobile Services
- **Status:** Active

**Reconnaissance Results:**
```bash
# DNS Information
dig samsung-mygalaxy.com A
# Result: [IP Address]

dig samsung-mygalaxy.com MX
# Result: [Mail servers]

# Subdomain Discovery
sublist3r -d samsung-mygalaxy.com
# Results: [Subdomains found]

# Technology Stack
whatweb https://samsung-mygalaxy.com
# Results: [Technologies detected]
```

**Key Findings:**
- [ ] Web server type and version
- [ ] CMS/Framework used
- [ ] SSL certificate details
- [ ] Subdomains discovered
- [ ] Email servers
- [ ] Social media presence

---

## 🔍 Practice Methodology

### Phase 1: Passive Information Gathering
1. **Domain Research**
   - Whois lookup
   - DNS enumeration
   - Subdomain discovery
   - Historical data analysis

2. **Company Intelligence**
   - Organization structure
   - Employee information
   - Social media presence
   - Business relationships

3. **Technical Reconnaissance**
   - Technology stack analysis
   - SSL certificate examination
   - Server fingerprinting
   - CDN and hosting information

### Phase 2: Active Information Gathering
1. **Network Discovery**
   - Host discovery
   - Port scanning
   - Service enumeration
   - OS fingerprinting

2. **Web Application Analysis**
   - Directory enumeration
   - Technology detection
   - Vulnerability scanning
   - Configuration analysis

3. **Service Enumeration**
   - Banner grabbing
   - Version detection
   - Default credentials testing
   - Service-specific vulnerabilities

---

## 📊 Findings & Notes

### Samsung LSS (samsung-lss.com)

#### DNS Records
```bash
# A Records
samsung-lss.com.        IN  A   [IP_ADDRESS]

# MX Records
samsung-lss.com.        IN  MX  10  [MAIL_SERVER]

# NS Records
samsung-lss.com.        IN  NS  [NAMESERVER_1]
samsung-lss.com.        IN  NS  [NAMESERVER_2]

# TXT Records
samsung-lss.com.        IN  TXT "v=spf1 [SPF_RECORD]"
```

#### Subdomains Discovered
- [ ] www.samsung-lss.com
- [ ] mail.samsung-lss.com
- [ ] [Additional subdomains]

#### Technology Stack
- **Web Server:** [Server type and version]
- **CMS/Framework:** [CMS detected]
- **SSL Certificate:** [Certificate details]
- **CDN:** [CDN provider if any]

#### Security Headers
```bash
# Check security headers
curl -I https://samsung-lss.com
# Results: [Security headers found]
```

#### Vulnerabilities Found
- [ ] [Vulnerability 1]
- [ ] [Vulnerability 2]
- [ ] [Additional findings]

---

### Samsung My Galaxy (samsung-mygalaxy.com)

#### DNS Records
```bash
# A Records
samsung-mygalaxy.com.   IN  A   [IP_ADDRESS]

# MX Records
samsung-mygalaxy.com.   IN  MX  10  [MAIL_SERVER]

# NS Records
samsung-mygalaxy.com.   IN  NS  [NAMESERVER_1]
samsung-mygalaxy.com.   IN  NS  [NAMESERVER_2]

# TXT Records
samsung-mygalaxy.com.   IN  TXT "v=spf1 [SPF_RECORD]"
```

#### Subdomains Discovered
- [ ] www.samsung-mygalaxy.com
- [ ] mail.samsung-mygalaxy.com
- [ ] [Additional subdomains]

#### Technology Stack
- **Web Server:** [Server type and version]
- **CMS/Framework:** [CMS detected]
- **SSL Certificate:** [Certificate details]
- **CDN:** [CDN provider if any]

#### Security Headers
```bash
# Check security headers
curl -I https://samsung-mygalaxy.com
# Results: [Security headers found]
```

#### Vulnerabilities Found
- [ ] [Vulnerability 1]
- [ ] [Vulnerability 2]
- [ ] [Additional findings]

---

## 🛠️ Tools Used

### Passive Reconnaissance
- **Whois:** Domain registration information
- **Dig:** DNS record enumeration
- **Sublist3r:** Subdomain discovery
- **theHarvester:** Email and employee enumeration
- **WhatWeb:** Technology stack detection
- **Shodan:** Internet-connected device search
- **Crt.sh:** Certificate transparency logs

### Active Reconnaissance
- **Nmap:** Network scanning and service enumeration
- **Gobuster:** Directory and file enumeration
- **Nikto:** Web vulnerability scanner
- **Wafw00f:** WAF detection
- **SSL Labs:** SSL configuration analysis

### Analysis Tools
- **Burp Suite:** Web application testing
- **OWASP ZAP:** Web application security scanner
- **Wireshark:** Network traffic analysis
- **Metasploit:** Exploitation framework

---

## 📚 Lessons Learned

### Technical Insights
1. **DNS Configuration**
   - Importance of proper DNS security
   - Zone transfer vulnerabilities
   - DNS enumeration techniques

2. **Web Application Security**
   - Common misconfigurations
   - Security header implementation
   - SSL/TLS best practices

3. **Information Disclosure**
   - Sensitive information in public records
   - Social media intelligence
   - Employee information gathering

### Methodology Improvements
1. **Systematic Approach**
   - Following structured methodology
   - Documenting all findings
   - Cross-referencing information

2. **Tool Selection**
   - Choosing appropriate tools for each phase
   - Combining multiple tools for comprehensive analysis
   - Understanding tool limitations

3. **Ethical Considerations**
   - Respecting target boundaries
   - Following responsible disclosure
   - Maintaining professional ethics

---

## 🎯 Next Steps

### Additional Targets
- [ ] Add more practice domains
- [ ] Include different types of targets (government, educational, commercial)
- [ ] Practice with different technology stacks

### Skill Development
- [ ] Advanced web application testing
- [ ] Network penetration testing
- [ ] Social engineering techniques
- [ ] Report writing and documentation

### Tool Mastery
- [ ] Advanced Nmap scripting
- [ ] Custom tool development
- [ ] Automation and scripting
- [ ] Cloud security assessment

---

## 📝 Notes Template

### Target: [DOMAIN_NAME]
**Date:** [DATE]
**Phase:** [PASSIVE/ACTIVE]
**Tools Used:** [TOOL_LIST]

#### Findings:
- [Finding 1]
- [Finding 2]
- [Finding 3]

#### Commands Used:
```bash
[COMMAND_1]
[COMMAND_2]
[COMMAND_3]
```

#### Screenshots/Evidence:
- [Screenshot 1]
- [Screenshot 2]
- [Screenshot 3]

#### Next Steps:
- [Action 1]
- [Action 2]
- [Action 3]

---

> **⚠️ Important:** Tất cả các hoạt động reconnaissance và testing được thực hiện chỉ với mục đích học tập và trên các mục tiêu được phép. Luôn tuân thủ các quy định pháp luật và đạo đức nghề nghiệp.
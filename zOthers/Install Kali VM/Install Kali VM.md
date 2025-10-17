# 🐧 Kali Linux VM Installation Guide

> **Hướng dẫn chi tiết cài đặt và cấu hình Kali Linux Virtual Machine cho môi trường học tập eJPT**

## 📋 Table of Contents
- [Prerequisites](#prerequisites)
- [Virtualization Software](#virtualization-software)
- [Download Kali Linux](#download-kali-linux)
- [VM Creation](#vm-creation)
- [Initial Configuration](#initial-configuration)
- [Post-Installation Setup](#post-installation-setup)
- [Troubleshooting](#troubleshooting)
- [Best Practices](#best-practices)
- [Security Considerations](#security-considerations)

---

## 🔧 Prerequisites

### System Requirements
- **RAM:** Tối thiểu 4GB (khuyến nghị 8GB+)
- **Storage:** Tối thiểu 20GB free space (khuyến nghị 50GB+)
- **CPU:** 64-bit processor với virtualization support
- **Network:** Internet connection để download và update

### Hardware Virtualization
Đảm bảo hardware virtualization được bật:
- **Intel:** Intel VT-x
- **AMD:** AMD-V
- **BIOS/UEFI:** Enable virtualization features

---

## 💻 Virtualization Software

### Option 1: VirtualBox (Free)
**Ưu điểm:**
- Miễn phí và open source
- Cross-platform (Windows, macOS, Linux)
- Dễ sử dụng cho người mới

**Download:** https://www.virtualbox.org/

### Option 2: VMware Workstation Player (Free)
**Ưu điểm:**
- Performance tốt hơn VirtualBox
- Integration tốt với host OS
- Professional features

**Download:** https://www.vmware.com/products/workstation-player.html

### Option 3: VMware Workstation Pro (Paid)
**Ưu điểm:**
- Advanced features
- Snapshot management
- Team collaboration tools

---

## 📥 Download Kali Linux

### Official Sources
1. **Kali Linux Website:** https://www.kali.org/get-kali/
2. **Pre-built VMs:** https://www.kali.org/get-kali/#kali-virtual-machines

### Available Formats
- **OVA (Open Virtual Appliance):** Cho VirtualBox
- **VMX:** Cho VMware
- **ISO:** Cho custom installation

### Recommended Downloads
```bash
# VirtualBox OVA
kali-linux-2023.4-virtualbox-amd64.ova

# VMware VMX
kali-linux-2023.4-vmware-amd64.vmx

# ISO Image
kali-linux-2023.4-installer-amd64.iso
```

---

## 🖥️ VM Creation

### Method 1: Import Pre-built VM (Recommended)

#### VirtualBox
1. **Open VirtualBox Manager**
2. **File → Import Appliance**
3. **Select OVA file** → Next
4. **Configure settings:**
   - RAM: 4-8GB
   - CPU: 2-4 cores
   - Storage: 50GB+
5. **Import** → Wait for completion

#### VMware
1. **Open VMware Player/Workstation**
2. **File → Open**
3. **Select VMX file**
4. **Configure settings** (same as VirtualBox)
5. **Power On**

### Method 2: Custom Installation from ISO

#### VirtualBox
1. **New VM** → Linux → Debian (64-bit)
2. **Allocate resources:**
   - RAM: 4-8GB
   - Hard disk: 50GB+ (VDI, Dynamic)
3. **Settings → Storage:**
   - Controller: IDE → Empty
   - Choose ISO file
4. **Start VM** → Follow installation wizard

#### VMware
1. **Create New Virtual Machine**
2. **Typical configuration**
3. **Install from ISO**
4. **Select Kali ISO**
5. **Configure resources** (same as VirtualBox)
6. **Complete installation**

---

## ⚙️ Initial Configuration

### First Boot Setup
```bash
# Default credentials (check documentation)
Username: kali
Password: kali

# Hoặc (một số bản mới)
Username: [user created during install]
Password: [password set during install]
```

### Network Configuration
```bash
# Check network connectivity
ping -c 4 google.com

# Check IP configuration
ip addr show
ip route show

# Test DNS resolution
nslookup google.com
```

### Update System
```bash
# Update package lists
sudo apt update

# Upgrade system
sudo apt full-upgrade -y

# Install essential tools
sudo apt install -y kali-tools-top10 git vim curl wget
```

---

## 🔧 Post-Installation Setup

### Essential Tools Installation
```bash
# Install top 10 Kali tools
sudo apt install -y kali-tools-top10

# Install additional useful tools
sudo apt install -y \
    nmap \
    gobuster \
    nikto \
    sqlmap \
    burpsuite \
    metasploit-framework \
    john \
    hashcat \
    hydra \
    aircrack-ng \
    wireshark \
    tcpdump \
    netcat \
    socat \
    netdiscover \
    enum4linux \
    smbclient \
    ldap-utils \
    dnsutils \
    whois \
    theharvester \
    recon-ng \
    maltego \
    setoolkit
```

### Development Environment
```bash
# Install Python development tools
sudo apt install -y python3 python3-pip python3-venv

# Install additional languages
sudo apt install -y nodejs npm golang-go

# Install text editors
sudo apt install -y vim nano emacs code
```

### Customization
```bash
# Set up aliases
echo "alias ll='ls -alF'" >> ~/.bashrc
echo "alias la='ls -A'" >> ~/.bashrc
echo "alias l='ls -CF'" >> ~/.bashrc
echo "alias ..='cd ..'" >> ~/.bashrc

# Reload bashrc
source ~/.bashrc
```

---

## 🔧 Troubleshooting

### Common Issues

#### 1. VM Won't Start
**Symptoms:** VM fails to boot or shows error messages

**Solutions:**
```bash
# Check virtualization support
# Windows: Check Task Manager → Performance → CPU
# Look for "Virtualization: Enabled"

# BIOS Settings:
# - Enable Intel VT-x or AMD-V
# - Enable Intel VT-d or AMD IOMMU
# - Disable Secure Boot (if needed)
```

#### 2. Network Issues
**Symptoms:** No internet connection, can't ping external hosts

**Solutions:**
```bash
# Check VM network settings
# VirtualBox: Settings → Network → Adapter 1 → NAT
# VMware: VM Settings → Network Adapter → NAT

# Restart network service
sudo systemctl restart NetworkManager

# Check network configuration
sudo ip link show
sudo ip addr show
```

#### 3. Performance Issues
**Symptoms:** VM runs slowly, laggy interface

**Solutions:**
```bash
# Increase VM resources:
# - RAM: 8GB+
# - CPU: 4+ cores
# - Enable hardware acceleration

# Install VMware Tools or VirtualBox Guest Additions
sudo apt install -y open-vm-tools  # For VMware
sudo apt install -y virtualbox-guest-utils  # For VirtualBox
```

#### 4. Display Issues
**Symptoms:** Poor resolution, display problems

**Solutions:**
```bash
# Install display drivers
sudo apt install -y xserver-xorg-video-all

# Configure display
sudo dpkg-reconfigure xserver-xorg

# Install guest additions
sudo apt install -y virtualbox-guest-x11  # For VirtualBox
```

#### 5. Audio Issues
**Symptoms:** No sound, audio not working

**Solutions:**
```bash
# Check audio devices
aplay -l

# Install audio packages
sudo apt install -y alsa-utils pulseaudio

# Test audio
speaker-test -c 2
```

### Advanced Troubleshooting

#### Log Analysis
```bash
# Check system logs
sudo journalctl -f

# Check boot logs
sudo dmesg | tail -50

# Check service status
sudo systemctl status NetworkManager
sudo systemctl status ssh
```

#### Network Troubleshooting
```bash
# Test network connectivity
ping -c 4 8.8.8.8
ping -c 4 google.com

# Check DNS resolution
nslookup google.com
dig google.com

# Check network interfaces
ip addr show
ip route show
```

---

## 📋 Best Practices

### Security
1. **Change default passwords**
2. **Enable firewall**
3. **Regular updates**
4. **Use snapshots for testing**
5. **Isolate VM from host network**

### Performance
1. **Allocate sufficient resources**
2. **Use SSD storage if possible**
3. **Enable hardware acceleration**
4. **Close unnecessary services**
5. **Use snapshots wisely**

### Organization
1. **Create separate VMs for different purposes**
2. **Use descriptive VM names**
3. **Document configurations**
4. **Keep snapshots organized**
5. **Regular cleanup**

### Backup Strategy
```bash
# Create VM snapshots before major changes
# VirtualBox: Right-click VM → Snapshots → Take Snapshot
# VMware: VM → Snapshot → Take Snapshot

# Export VM for backup
# VirtualBox: File → Export Appliance
# VMware: File → Export
```

---

## 🔒 Security Considerations

### VM Isolation
```bash
# Use NAT networking for isolation
# Create separate network segments
# Use host-only networking for lab environments
```

### Host Security
```bash
# Keep host OS updated
# Use antivirus on host
# Regular backups
# Strong passwords
```

### VM Security
```bash
# Enable firewall
sudo ufw enable

# Disable unnecessary services
sudo systemctl disable bluetooth
sudo systemctl disable cups

# Regular updates
sudo apt update && sudo apt upgrade -y
```

---

## 🎯 Lab Environment Setup

### Network Configuration
```bash
# Create lab network
# VirtualBox: File → Preferences → Network → Host-only Networks
# VMware: Edit → Virtual Network Editor

# Configure multiple network adapters:
# Adapter 1: NAT (Internet access)
# Adapter 2: Host-only (Lab network)
# Adapter 3: Internal (VM-to-VM communication)
```

### Target VMs
```bash
# Download vulnerable VMs:
# - Metasploitable
# - DVWA
# - WebGoat
# - VulnHub VMs
# - HackTheBox VMs
```

### Tools Configuration
```bash
# Configure Burp Suite
# - Set up proxy settings
# - Install extensions
# - Configure scope

# Configure Metasploit
sudo systemctl start postgresql
sudo msfdb init
```

---

## 📚 Additional Resources

### Documentation
- **Kali Linux Documentation:** https://www.kali.org/docs/
- **VirtualBox Manual:** https://www.virtualbox.org/manual/
- **VMware Documentation:** https://docs.vmware.com/

### Learning Resources
- **Kali Linux Training:** https://kali.training/
- **eJPT Course:** https://ine.com/
- **Cybrary:** https://www.cybrary.it/

### Community
- **Kali Linux Forums:** https://forums.kali.org/
- **Reddit r/Kalilinux:** https://reddit.com/r/Kalilinux
- **Discord Communities**

---

## 🎯 Quick Setup Checklist

### Pre-Installation
- [ ] Download virtualization software
- [ ] Download Kali Linux VM
- [ ] Check system requirements
- [ ] Enable hardware virtualization

### Installation
- [ ] Import/create VM
- [ ] Configure resources (RAM, CPU, Storage)
- [ ] Set up networking
- [ ] Boot VM successfully

### Post-Installation
- [ ] Change default passwords
- [ ] Update system packages
- [ ] Install essential tools
- [ ] Configure network settings
- [ ] Test connectivity

### Security
- [ ] Enable firewall
- [ ] Disable unnecessary services
- [ ] Create snapshots
- [ ] Document configuration

---

> **💡 Pro Tip:** Luôn tạo snapshot trước khi thực hiện các thay đổi lớn để có thể rollback nếu cần thiết. Điều này đặc biệt quan trọng khi test các tools và techniques mới.
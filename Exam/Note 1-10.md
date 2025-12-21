root@kali:~# nmap -sn 192.168.100.0/24
Starting Nmap 7.92 ( https://nmap.org ) at 2025-12-21 22:18 IST
Nmap scan report for ip-192-168-100-1.ap-southeast-1.compute.internal (192.168.100.1)
Host is up (0.00018s latency).
MAC Address: 02:E9:8B:DA:A1:63 (Unknown)
Nmap scan report for ip-192-168-100-50.ap-southeast-1.compute.internal (192.168.100.50)
Host is up (0.00032s latency).
MAC Address: 02:B5:ED:A1:42:6F (Unknown)
Nmap scan report for ip-192-168-100-51.ap-southeast-1.compute.internal (192.168.100.51)
Host is up (0.00032s latency).
MAC Address: 02:BA:D7:A6:44:59 (Unknown)
Nmap scan report for ip-192-168-100-52.ap-southeast-1.compute.internal (192.168.100.52)
Host is up (0.00037s latency).
MAC Address: 02:D4:37:F7:98:01 (Unknown)
Nmap scan report for ip-192-168-100-55.ap-southeast-1.compute.internal (192.168.100.55)
Host is up (0.00043s latency).
MAC Address: 02:75:26:1E:4E:E1 (Unknown)
Nmap scan report for ip-192-168-100-63.ap-southeast-1.compute.internal (192.168.100.63)
Host is up (0.00055s latency).
MAC Address: 02:88:66:A2:62:7B (Unknown)
Nmap scan report for ip-192-168-100-67.ap-southeast-1.compute.internal (192.168.100.67)
Host is up (0.00052s latency).
MAC Address: 02:73:22:C1:45:35 (Unknown)
Nmap scan report for ip-192-168-100-5.ap-southeast-1.compute.internal (192.168.100.5)
Host is up.
Nmap done: 256 IP addresses (8 hosts up) scanned in 1.84 seconds

======================================================



root@kali:~# nmap -sV -O -sC -p 80,139,445,3306,443 192.168.100.50,51,52,55
Starting Nmap 7.92 ( https://nmap.org ) at 2025-12-21 22:24 IST
Nmap scan report for ip-192-168-100-50.ap-southeast-1.compute.internal (192.168.100.50)
Host is up (0.00035s latency).

PORT     STATE  SERVICE      VERSION
80/tcp   open   http         Apache httpd 2.4.51 ((Win64) PHP/7.4.26)
|_http-title: WAMPSERVER Homepage
|_http-server-header: Apache/2.4.51 (Win64) PHP/7.4.26
139/tcp  open   netbios-ssn  Microsoft Windows netbios-ssn
443/tcp  closed https
445/tcp  open   microsoft-ds Windows Server 2012 R2 Standard 9600 microsoft-ds
3306/tcp closed mysql
MAC Address: 02:B5:ED:A1:42:6F (Unknown)
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.92%E=4%D=12/21%OT=80%CT=443%CU=34934%PV=Y%DS=1%DC=D%G=Y%M=02B5E
OS:D%TM=6948267C%P=x86_64-pc-linux-gnu)SEQ(SP=FE%GCD=1%ISR=10E%TI=I%CI=I%II
OS:=I%SS=S%TS=7)OPS(O1=M2301NW8ST11%O2=M2301NW8ST11%O3=M2301NW8NNT11%O4=M23
OS:01NW8ST11%O5=M2301NW8ST11%O6=M2301ST11)WIN(W1=2000%W2=2000%W3=2000%W4=20
OS:00%W5=2000%W6=2000)ECN(R=Y%DF=Y%T=80%W=2000%O=M2301NW8NNS%CC=Y%Q=)T1(R=Y
OS:%DF=Y%T=80%S=O%A=S+%F=AS%RD=0%Q=)T2(R=Y%DF=Y%T=80%W=0%S=Z%A=S%F=AR%O=%RD
OS:=0%Q=)T3(R=Y%DF=Y%T=80%W=0%S=Z%A=O%F=AR%O=%RD=0%Q=)T4(R=Y%DF=Y%T=80%W=0%
OS:S=A%A=O%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=80%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(
OS:R=Y%DF=Y%T=80%W=0%S=A%A=O%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=80%W=0%S=Z%A=S+%F
OS:=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=80%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G
OS:%RUD=G)IE(R=Y%DFI=N%T=80%CD=Z)

Network Distance: 1 hop
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Host script results:
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-time: 
|   date: 2025-12-21T16:55:18
|_  start_date: 2025-12-21T16:41:40
|_nbstat: NetBIOS name: WINSERVER-01, NetBIOS user: <unknown>, NetBIOS MAC: 02:b5:ed:a1:42:6f (unknown)
| smb2-security-mode: 
|   3.0.2: 
|_    Message signing enabled but not required
| smb-os-discovery: 
|   OS: Windows Server 2012 R2 Standard 9600 (Windows Server 2012 R2 Standard 6.3)
|   OS CPE: cpe:/o:microsoft:windows_server_2012::-
|   Computer name: WINSERVER-01
|   NetBIOS computer name: WINSERVER-01\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2025-12-21T16:55:18+00:00
|_clock-skew: mean: 0s, deviation: 1s, median: 0s

Nmap scan report for ip-192-168-100-51.ap-southeast-1.compute.internal (192.168.100.51)
Host is up (0.00031s latency).

PORT     STATE  SERVICE      VERSION
80/tcp   open   http         Microsoft IIS httpd 8.5
| http-webdav-scan: 
|   WebDAV type: Unknown
|   Allowed Methods: OPTIONS, TRACE, GET, HEAD, POST, COPY, PROPFIND, DELETE, MOVE, PROPPATCH, MKCOL, LOCK, UNLOCK
|   Server Date: Sun, 21 Dec 2025 16:55:17 GMT
|   Server Type: Microsoft-IIS/8.5
|   Public Options: OPTIONS, TRACE, GET, HEAD, POST, PROPFIND, PROPPATCH, MKCOL, PUT, DELETE, COPY, MOVE, LOCK, UNLOCK
|   Directory Listing: 
|     http://ip-192-168-100-51.ap-southeast-1.compute.internal/
|     http://ip-192-168-100-51.ap-southeast-1.compute.internal/aspnet_client/
|     http://ip-192-168-100-51.ap-southeast-1.compute.internal/cmdasp.aspx
|     http://ip-192-168-100-51.ap-southeast-1.compute.internal/iis-85.png
|     http://ip-192-168-100-51.ap-southeast-1.compute.internal/iisstart.htm
|_    http://ip-192-168-100-51.ap-southeast-1.compute.internal/robots.txt.txt
|_http-svn-info: ERROR: Script execution failed (use -d to debug)
|_http-title: IIS Windows Server
| http-methods: 
|_  Potentially risky methods: TRACE COPY PROPFIND DELETE MOVE PROPPATCH MKCOL LOCK UNLOCK PUT
|_http-server-header: Microsoft-IIS/8.5
139/tcp  open   netbios-ssn  Microsoft Windows netbios-ssn
443/tcp  closed https
445/tcp  open   microsoft-ds Microsoft Windows Server 2008 R2 - 2012 microsoft-ds
3306/tcp closed mysql
MAC Address: 02:BA:D7:A6:44:59 (Unknown)
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.92%E=4%D=12/21%OT=80%CT=443%CU=41470%PV=Y%DS=1%DC=D%G=Y%M=02BAD
OS:7%TM=6948267C%P=x86_64-pc-linux-gnu)SEQ(SP=FD%GCD=1%ISR=10B%TI=I%CI=I%II
OS:=I%SS=S%TS=7)OPS(O1=M2301NW8ST11%O2=M2301NW8ST11%O3=M2301NW8NNT11%O4=M23
OS:01NW8ST11%O5=M2301NW8ST11%O6=M2301ST11)WIN(W1=2000%W2=2000%W3=2000%W4=20
OS:00%W5=2000%W6=2000)ECN(R=Y%DF=Y%T=80%W=2000%O=M2301NW8NNS%CC=Y%Q=)T1(R=Y
OS:%DF=Y%T=80%S=O%A=S+%F=AS%RD=0%Q=)T2(R=Y%DF=Y%T=80%W=0%S=Z%A=S%F=AR%O=%RD
OS:=0%Q=)T3(R=Y%DF=Y%T=80%W=0%S=Z%A=O%F=AR%O=%RD=0%Q=)T4(R=Y%DF=Y%T=80%W=0%
OS:S=A%A=O%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=80%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(
OS:R=Y%DF=Y%T=80%W=0%S=A%A=O%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=80%W=0%S=Z%A=S+%F
OS:=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=80%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G
OS:%RUD=G)IE(R=Y%DFI=N%T=80%CD=Z)

Network Distance: 1 hop
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2025-12-21T16:55:17
|_  start_date: 2025-12-21T16:41:35
| smb-security-mode: 
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_nbstat: NetBIOS name: WINSERVER-02, NetBIOS user: <unknown>, NetBIOS MAC: 02:ba:d7:a6:44:59 (unknown)
| smb2-security-mode: 
|   3.0.2: 
|_    Message signing enabled but not required
|_clock-skew: mean: -1s, deviation: 0s, median: -1s

Nmap scan report for ip-192-168-100-52.ap-southeast-1.compute.internal (192.168.100.52)
Host is up (0.0011s latency).

PORT     STATE  SERVICE     VERSION
80/tcp   open   http        Apache httpd 2.4.41
|_http-title: Index of /
| http-ls: Volume /
| SIZE  TIME              FILENAME
| -     2018-02-21 17:28  drupal/
|_
|_http-server-header: Apache/2.4.41 (Ubuntu)
139/tcp  open   netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
443/tcp  closed https
445/tcp  open   netbios-ssn Samba smbd 4.13.17-Ubuntu (workgroup: WORKGROUP)
3306/tcp open   mysql       MySQL 5.5.5-10.3.34-MariaDB-0ubuntu0.20.04.1
| mysql-info: 
|   Protocol: 10
|   Version: 5.5.5-10.3.34-MariaDB-0ubuntu0.20.04.1
|   Thread ID: 37
|   Capabilities flags: 63486
|   Some Capabilities: Support41Auth, Speaks41ProtocolOld, ODBCClient, IgnoreSpaceBeforeParenthesis, FoundRows, InteractiveClient, SupportsTransactions, Speaks41ProtocolNew, IgnoreSigpipes, DontAllowDatabaseTableColumn, SupportsLoadDataLocal, SupportsCompression, ConnectWithDatabase, LongColumnFlag, SupportsMultipleStatments, SupportsMultipleResults, SupportsAuthPlugins
|   Status: Autocommit
|   Salt: y45L]p>#2qd!vOg:+e=@
|_  Auth Plugin Name: mysql_native_password
MAC Address: 02:D4:37:F7:98:01 (Unknown)
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.92%E=4%D=12/21%OT=80%CT=443%CU=35321%PV=Y%DS=1%DC=D%G=Y%M=02D43
OS:7%TM=6948267C%P=x86_64-pc-linux-gnu)SEQ(SP=108%GCD=1%ISR=10C%TI=Z%CI=Z%I
OS:I=I%TS=A)OPS(O1=M2301ST11NW7%O2=M2301ST11NW7%O3=M2301NNT11NW7%O4=M2301ST
OS:11NW7%O5=M2301ST11NW7%O6=M2301ST11)WIN(W1=F4B3%W2=F4B3%W3=F4B3%W4=F4B3%W
OS:5=F4B3%W6=F4B3)ECN(R=Y%DF=Y%T=40%W=F507%O=M2301NNSNW7%CC=Y%Q=)T1(R=Y%DF=
OS:Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%
OS:F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y
OS:%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%R
OS:D=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)I
OS:E(R=Y%DFI=N%T=40%CD=S)

Network Distance: 1 hop
Service Info: Host: IP-192-168-100-52

Host script results:
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.13.17-Ubuntu)
|   Computer name: ip-192-168-100-52
|   NetBIOS computer name: IP-192-168-100-52\x00
|   Domain name: ap-southeast-1.compute.internal
|   FQDN: ip-192-168-100-52.ap-southeast-1.compute.internal
|_  System time: 2025-12-21T16:55:17+00:00
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled but not required
|_nbstat: NetBIOS name: IP-192-168-100-, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb2-time: 
|   date: 2025-12-21T16:55:18
|_  start_date: N/A
|_clock-skew: mean: 0s, deviation: 1s, median: 0s

Nmap scan report for ip-192-168-100-55.ap-southeast-1.compute.internal (192.168.100.55)
Host is up (0.00038s latency).

PORT     STATE  SERVICE      VERSION
80/tcp   open   http         Microsoft IIS httpd 10.0
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-title: IIS Windows Server
|_http-server-header: Microsoft-IIS/10.0
139/tcp  open   netbios-ssn  Microsoft Windows netbios-ssn
443/tcp  closed https
445/tcp  open   microsoft-ds Windows Server 2019 Datacenter 17763 microsoft-ds
3306/tcp closed mysql
MAC Address: 02:75:26:1E:4E:E1 (Unknown)
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.92%E=4%D=12/21%OT=80%CT=443%CU=43630%PV=Y%DS=1%DC=D%G=Y%M=02752
OS:6%TM=6948267C%P=x86_64-pc-linux-gnu)SEQ(SP=FD%GCD=1%ISR=103%TI=I%CI=I%II
OS:=I%SS=S%TS=U)OPS(O1=M2301NW8NNS%O2=M2301NW8NNS%O3=M2301NW8%O4=M2301NW8NN
OS:S%O5=M2301NW8NNS%O6=M2301NNS)WIN(W1=FFFF%W2=FFFF%W3=FFFF%W4=FFFF%W5=FFFF
OS:%W6=FF70)ECN(R=Y%DF=Y%T=80%W=FFFF%O=M2301NW8NNS%CC=Y%Q=)T1(R=Y%DF=Y%T=80
OS:%S=O%A=S+%F=AS%RD=0%Q=)T2(R=Y%DF=Y%T=80%W=0%S=Z%A=S%F=AR%O=%RD=0%Q=)T3(R
OS:=Y%DF=Y%T=80%W=0%S=Z%A=O%F=AR%O=%RD=0%Q=)T4(R=Y%DF=Y%T=80%W=0%S=A%A=O%F=
OS:R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=80%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T
OS:=80%W=0%S=A%A=O%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=80%W=0%S=Z%A=S+%F=AR%O=%RD=
OS:0%Q=)U1(R=Y%DF=N%T=80%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(
OS:R=Y%DFI=N%T=80%CD=Z)

Network Distance: 1 hop
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Host script results:
| smb-os-discovery: 
|   OS: Windows Server 2019 Datacenter 17763 (Windows Server 2019 Datacenter 6.3)
|   Computer name: WINSERVER-03
|   NetBIOS computer name: WINSERVER-03\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2025-12-21T16:55:18+00:00
|_nbstat: NetBIOS name: WINSERVER-03, NetBIOS user: <unknown>, NetBIOS MAC: 02:75:26:1e:4e:e1 (unknown)
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2025-12-21T16:55:18
|_  start_date: N/A
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_clock-skew: mean: 0s, deviation: 1s, median: 0s

Post-scan script results:
| clock-skew: 
|   0s: 
|     192.168.100.50 (ip-192-168-100-50.ap-southeast-1.compute.internal)
|     192.168.100.55 (ip-192-168-100-55.ap-southeast-1.compute.internal)
|_    192.168.100.52 (ip-192-168-100-52.ap-southeast-1.compute.internal)
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 4 IP addresses (4 hosts up) scanned in 37.06 seconds


=========================================================

root@kali:~# nmap -sV -O -sC -p 80,139,445,3306,443 192.168.100.1,5,63,67
root@kali:~# nmap -sV -O -sC -p 80,139,445,3306,443 192.168.100.1,5,63,67
Starting Nmap 7.92 ( https://nmap.org ) at 2025-12-21 22:38 IST
Nmap scan report for ip-192-168-100-1.ap-southeast-1.compute.internal (192.168.100.1)
Host is up (0.00024s latency).

PORT     STATE    SERVICE      VERSION
80/tcp   filtered http
139/tcp  filtered netbios-ssn
443/tcp  filtered https
445/tcp  filtered microsoft-ds
3306/tcp filtered mysql
MAC Address: 02:E9:8B:DA:A1:63 (Unknown)
Too many fingerprints match this host to give specific OS details
Network Distance: 1 hop

Nmap scan report for ip-192-168-100-63.ap-southeast-1.compute.internal (192.168.100.63)
Host is up (0.00019s latency).

PORT     STATE    SERVICE      VERSION
80/tcp   filtered http
139/tcp  filtered netbios-ssn
443/tcp  filtered https
445/tcp  filtered microsoft-ds
3306/tcp filtered mysql
MAC Address: 02:88:66:A2:62:7B (Unknown)
Too many fingerprints match this host to give specific OS details
Network Distance: 1 hop

Nmap scan report for ip-192-168-100-67.ap-southeast-1.compute.internal (192.168.100.67)
Host is up (0.00041s latency).

PORT     STATE  SERVICE      VERSION
80/tcp   closed http
139/tcp  closed netbios-ssn
443/tcp  closed https
445/tcp  closed microsoft-ds
3306/tcp closed mysql
MAC Address: 02:73:22:C1:45:35 (Unknown)
Too many fingerprints match this host to give specific OS details
Network Distance: 1 hop

Nmap scan report for ip-192-168-100-5.ap-southeast-1.compute.internal (192.168.100.5)
Host is up (0.000021s latency).

PORT     STATE  SERVICE      VERSION
80/tcp   closed http
139/tcp  closed netbios-ssn
443/tcp  closed https
445/tcp  closed microsoft-ds
3306/tcp closed mysql
Too many fingerprints match this host to give specific OS details
Network Distance: 0 hops

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 4 IP addresses (4 hosts up) scanned in 5.97 seconds


======================================================

root@kali:~# curl -s http://192.168.100.50 | grep -i wordpress
                        <li>wordpress</li><li class='projectsdir'>These are your folders in c:/wamp64/www<br />To use them as an http link, you must declare them as VirtualHost</li>
                        <li><a href="http://localhost">localhost</a></li><li><a href="http://wordpress.local">wordpress.local</a></li>

======================================================

http://192.168.100.52/drupal/

======================================================

root@kali:~# curl -s -L http://192.168.100.50/wordpress/ | grep "wp-content/themes"
<link rel='stylesheet' id='bootstrap-min-css'  href='http://wordpress.local/wp-content/themes/spintech/assets/css/bootstrap.min.css?ver=5.9.3' type='text/css' media='all' />
<link rel='stylesheet' id='owl-carousel-min-css'  href='http://wordpress.local/wp-content/themes/spintech/assets/css/owl.carousel.min.css?ver=5.9.3' type='text/css' media='all' />
<link rel='stylesheet' id='font-awesome-css'  href='http://wordpress.local/wp-content/themes/spintech/assets/css/fonts/font-awesome/css/font-awesome.min.css?ver=5.9.3' type='text/css' media='all' />
<link rel='stylesheet' id='animate-css'  href='http://wordpress.local/wp-content/themes/spintech/assets/css/animate.min.css?ver=5.9.3' type='text/css' media='all' />
<link rel='stylesheet' id='spintech-editor-style-css'  href='http://wordpress.local/wp-content/themes/spintech/assets/css/editor-style.css?ver=5.9.3' type='text/css' media='all' />
<link rel='stylesheet' id='spintech-menus-css'  href='http://wordpress.local/wp-content/themes/spintech/assets/css/classic-menu.css?ver=5.9.3' type='text/css' media='all' />
<link rel='stylesheet' id='spintech-widgets-css'  href='http://wordpress.local/wp-content/themes/spintech/assets/css/widgets.css?ver=5.9.3' type='text/css' media='all' />
<link rel='stylesheet' id='spintech-main-css'  href='http://wordpress.local/wp-content/themes/spintech/assets/css/main.css?ver=5.9.3' type='text/css' media='all' />
<link rel='stylesheet' id='spintech-media-query-css'  href='http://wordpress.local/wp-content/themes/spintech/assets/css/responsive.css?ver=5.9.3' type='text/css' media='all' />
<link rel='stylesheet' id='spintech-style-css'  href='http://wordpress.local/wp-content/themes/spintech/style.css?ver=5.9.3' type='text/css' media='all' />
                                        background-image: url(http://wordpress.local/wp-content/themes/spintech/assets/images/bg/breadcrumbg.jpg);
<script type='text/javascript' src='http://wordpress.local/wp-content/themes/spintech/assets/js/owl.carousel.min.js?ver=1' id='owl-carousel-js'></script>
<script type='text/javascript' src='http://wordpress.local/wp-content/themes/spintech/assets/js/bootstrap.min.js?ver=1.0' id='bootstrap-js'></script>
<script type='text/javascript' src='http://wordpress.local/wp-content/themes/spintech/assets/js/wow.min.js?ver=5.9.3' id='wow-min-js'></script>
<script type='text/javascript' src='http://wordpress.local/wp-content/themes/spintech/assets/js/custom.js?ver=5.9.3' id='spintech-custom-js-js'></script>
<script type='text/javascript' src='http://wordpress.local/wp-content/themes/spintech/assets/js/theme.min.js?ver=5.9.3' id='spintech-theme-js-js'></script>


========================================

root@kali:~# enum4linux -a 192.168.100.52
Starting enum4linux v0.8.9 ( http://labs.portcullis.co.uk/application/enum4linux/ ) on Sun Dec 21 23:25:02 2025

 ========================== 
|    Target Information    |
 ========================== 
Target ........... 192.168.100.52
RID Range ........ 500-550,1000-1050
Username ......... ''
Password ......... ''
Known Usernames .. administrator, guest, krbtgt, domain admins, root, bin, none


 ====================================================== 
|    Enumerating Workgroup/Domain on 192.168.100.52    |
 ====================================================== 
[+] Got domain/workgroup name: WORKGROUP

 ============================================== 
|    Nbtstat Information for 192.168.100.52    |
 ============================================== 
Looking up status of 192.168.100.52
        IP-192-168-100- <00> -         B <ACTIVE>  Workstation Service
        IP-192-168-100- <03> -         B <ACTIVE>  Messenger Service
        IP-192-168-100- <20> -         B <ACTIVE>  File Server Service
        WORKGROUP       <00> - <GROUP> B <ACTIVE>  Domain/Workgroup Name
        WORKGROUP       <1e> - <GROUP> B <ACTIVE>  Browser Service Elections

        MAC Address = 00-00-00-00-00-00

 ======================================= 
|    Session Check on 192.168.100.52    |
 ======================================= 
[+] Server 192.168.100.52 allows sessions using username '', password ''

 ============================================= 
|    Getting domain SID for 192.168.100.52    |
 ============================================= 
Domain Name: WORKGROUP
Domain Sid: (NULL SID)
[+] Can't determine if host is part of domain or part of a workgroup

 ======================================== 
|    OS information on 192.168.100.52    |
 ======================================== 
Use of uninitialized value $os_info in concatenation (.) or string at ./enum4linux.pl line 464.
[+] Got OS info for 192.168.100.52 from smbclient: 
[+] Got OS info for 192.168.100.52 from srvinfo:
        IP-192-168-100-Wk Sv PrQ Unx NT SNT ip-192-168-100-52 server (Samba, Ubuntu)
        platform_id     :       500
        os version      :       6.1
        server type     :       0x809a03

 =============================== 
|    Users on 192.168.100.52    |
 =============================== 
Use of uninitialized value $users in print at ./enum4linux.pl line 874.
Use of uninitialized value $users in pattern match (m//) at ./enum4linux.pl line 877.

Use of uninitialized value $users in print at ./enum4linux.pl line 888.
Use of uninitialized value $users in pattern match (m//) at ./enum4linux.pl line 890.

 =========================================== 
|    Share Enumeration on 192.168.100.52    |
 =========================================== 

        Sharename       Type      Comment
        ---------       ----      -------
        print$          Disk      Printer Drivers
        shared          Disk      shared
        IPC$            IPC       IPC Service (ip-192-168-100-52 server (Samba, Ubuntu))
Reconnecting with SMB1 for workgroup listing.

        Server               Comment
        ---------            -------

        Workgroup            Master
        ---------            -------
        WORKGROUP            

[+] Attempting to map shares on 192.168.100.52
//192.168.100.52/print$ Mapping: DENIED, Listing: N/A
//192.168.100.52/shared Mapping: OK, Listing: OK
//192.168.100.52/IPC$   [E] Can't understand response:
NT_STATUS_OBJECT_NAME_NOT_FOUND listing \*

 ====================================================== 
|    Password Policy Information for 192.168.100.52    |
 ====================================================== 


[+] Attaching to 192.168.100.52 using a NULL share

[+] Trying protocol 139/SMB...

[+] Found domain(s):

        [+] IP-192-168-100-52
        [+] Builtin

[+] Password Info for Domain: IP-192-168-100-52

        [+] Minimum password length: 5
        [+] Password history length: None
        [+] Maximum password age: 37 days 6 hours 21 minutes 
        [+] Password Complexity Flags: 000000

                [+] Domain Refuse Password Change: 0
                [+] Domain Password Store Cleartext: 0
                [+] Domain Password Lockout Admins: 0
                [+] Domain Password No Clear Change: 0
                [+] Domain Password No Anon Change: 0
                [+] Domain Password Complex: 0

        [+] Minimum password age: None
        [+] Reset Account Lockout Counter: 30 minutes 
        [+] Locked Account Duration: 30 minutes 
        [+] Account Lockout Threshold: None
        [+] Forced Log off Time: 37 days 6 hours 21 minutes 


[+] Retieved partial password policy with rpcclient:

Password Complexity: Disabled
Minimum Password Length: 5


 ================================ 
|    Groups on 192.168.100.52    |
 ================================ 

[+] Getting builtin groups:

[+] Getting builtin group memberships:

[+] Getting local groups:

[+] Getting local group memberships:

[+] Getting domain groups:

[+] Getting domain group memberships:

 ========================================================================= 
|    Users on 192.168.100.52 via RID cycling (RIDS: 500-550,1000-1050)    |
 ========================================================================= 
[I] Found new SID: S-1-22-1
[I] Found new SID: S-1-5-21-3430311043-2551269930-1198545645
[I] Found new SID: S-1-5-32
[+] Enumerating users using SID S-1-22-1 and logon username '', password ''
S-1-22-1-1000 Unix User\ubuntu (Local User)
S-1-22-1-1001 Unix User\auditor (Local User)
S-1-22-1-1002 Unix User\dbadmin (Local User)
[+] Enumerating users using SID S-1-5-21-3430311043-2551269930-1198545645 and logon username '', password ''
S-1-5-21-3430311043-2551269930-1198545645-500 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-501 IP-192-168-100-52\nobody (Local User)
S-1-5-21-3430311043-2551269930-1198545645-502 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-503 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-504 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-505 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-506 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-507 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-508 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-509 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-510 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-511 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-512 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-513 IP-192-168-100-52\None (Domain Group)
S-1-5-21-3430311043-2551269930-1198545645-514 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-515 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-516 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-517 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-518 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-519 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-520 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-521 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-522 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-523 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-524 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-525 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-526 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-527 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-528 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-529 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-530 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-531 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-532 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-533 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-534 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-535 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-536 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-537 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-538 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-539 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-540 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-541 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-542 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-543 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-544 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-545 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-546 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-547 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-548 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-549 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-550 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1000 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1001 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1002 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1003 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1004 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1005 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1006 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1007 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1008 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1009 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1010 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1011 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1012 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1013 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1014 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1015 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1016 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1017 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1018 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1019 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1020 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1021 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1022 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1023 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1024 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1025 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1026 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1027 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1028 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1029 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1030 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1031 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1032 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1033 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1034 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1035 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1036 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1037 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1038 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1039 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1040 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1041 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1042 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1043 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1044 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1045 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1046 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1047 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1048 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1049 *unknown*\*unknown* (8)
S-1-5-21-3430311043-2551269930-1198545645-1050 *unknown*\*unknown* (8)
[+] Enumerating users using SID S-1-5-32 and logon username '', password ''
S-1-5-32-500 *unknown*\*unknown* (8)
S-1-5-32-501 *unknown*\*unknown* (8)
S-1-5-32-502 *unknown*\*unknown* (8)
S-1-5-32-503 *unknown*\*unknown* (8)
S-1-5-32-504 *unknown*\*unknown* (8)
S-1-5-32-505 *unknown*\*unknown* (8)
S-1-5-32-506 *unknown*\*unknown* (8)
S-1-5-32-507 *unknown*\*unknown* (8)
S-1-5-32-508 *unknown*\*unknown* (8)
S-1-5-32-509 *unknown*\*unknown* (8)
S-1-5-32-510 *unknown*\*unknown* (8)
S-1-5-32-511 *unknown*\*unknown* (8)
S-1-5-32-512 *unknown*\*unknown* (8)
S-1-5-32-513 *unknown*\*unknown* (8)
S-1-5-32-514 *unknown*\*unknown* (8)
S-1-5-32-515 *unknown*\*unknown* (8)
S-1-5-32-516 *unknown*\*unknown* (8)
S-1-5-32-517 *unknown*\*unknown* (8)
S-1-5-32-518 *unknown*\*unknown* (8)
S-1-5-32-519 *unknown*\*unknown* (8)
S-1-5-32-520 *unknown*\*unknown* (8)
S-1-5-32-521 *unknown*\*unknown* (8)
S-1-5-32-522 *unknown*\*unknown* (8)
S-1-5-32-523 *unknown*\*unknown* (8)
S-1-5-32-524 *unknown*\*unknown* (8)
S-1-5-32-525 *unknown*\*unknown* (8)
S-1-5-32-526 *unknown*\*unknown* (8)
S-1-5-32-527 *unknown*\*unknown* (8)
S-1-5-32-528 *unknown*\*unknown* (8)
S-1-5-32-529 *unknown*\*unknown* (8)
S-1-5-32-530 *unknown*\*unknown* (8)
S-1-5-32-531 *unknown*\*unknown* (8)
S-1-5-32-532 *unknown*\*unknown* (8)
S-1-5-32-533 *unknown*\*unknown* (8)
S-1-5-32-534 *unknown*\*unknown* (8)
S-1-5-32-535 *unknown*\*unknown* (8)
S-1-5-32-536 *unknown*\*unknown* (8)
S-1-5-32-537 *unknown*\*unknown* (8)
S-1-5-32-538 *unknown*\*unknown* (8)
S-1-5-32-539 *unknown*\*unknown* (8)
S-1-5-32-540 *unknown*\*unknown* (8)
S-1-5-32-541 *unknown*\*unknown* (8)
S-1-5-32-542 *unknown*\*unknown* (8)
S-1-5-32-543 *unknown*\*unknown* (8)
S-1-5-32-544 BUILTIN\Administrators (Local Group)
S-1-5-32-545 BUILTIN\Users (Local Group)
S-1-5-32-546 BUILTIN\Guests (Local Group)
S-1-5-32-547 BUILTIN\Power Users (Local Group)
S-1-5-32-548 BUILTIN\Account Operators (Local Group)
S-1-5-32-549 BUILTIN\Server Operators (Local Group)
S-1-5-32-550 BUILTIN\Print Operators (Local Group)
S-1-5-32-1000 *unknown*\*unknown* (8)
S-1-5-32-1001 *unknown*\*unknown* (8)
S-1-5-32-1002 *unknown*\*unknown* (8)
S-1-5-32-1003 *unknown*\*unknown* (8)
S-1-5-32-1004 *unknown*\*unknown* (8)
S-1-5-32-1005 *unknown*\*unknown* (8)
S-1-5-32-1006 *unknown*\*unknown* (8)
S-1-5-32-1007 *unknown*\*unknown* (8)
S-1-5-32-1008 *unknown*\*unknown* (8)
S-1-5-32-1009 *unknown*\*unknown* (8)
S-1-5-32-1010 *unknown*\*unknown* (8)
S-1-5-32-1011 *unknown*\*unknown* (8)
S-1-5-32-1012 *unknown*\*unknown* (8)
S-1-5-32-1013 *unknown*\*unknown* (8)
S-1-5-32-1014 *unknown*\*unknown* (8)
S-1-5-32-1015 *unknown*\*unknown* (8)
S-1-5-32-1016 *unknown*\*unknown* (8)
S-1-5-32-1017 *unknown*\*unknown* (8)
S-1-5-32-1018 *unknown*\*unknown* (8)
S-1-5-32-1019 *unknown*\*unknown* (8)
S-1-5-32-1020 *unknown*\*unknown* (8)
S-1-5-32-1021 *unknown*\*unknown* (8)
S-1-5-32-1022 *unknown*\*unknown* (8)
S-1-5-32-1023 *unknown*\*unknown* (8)
S-1-5-32-1024 *unknown*\*unknown* (8)
S-1-5-32-1025 *unknown*\*unknown* (8)
S-1-5-32-1026 *unknown*\*unknown* (8)
S-1-5-32-1027 *unknown*\*unknown* (8)
S-1-5-32-1028 *unknown*\*unknown* (8)
S-1-5-32-1029 *unknown*\*unknown* (8)
S-1-5-32-1030 *unknown*\*unknown* (8)
S-1-5-32-1031 *unknown*\*unknown* (8)
S-1-5-32-1032 *unknown*\*unknown* (8)
S-1-5-32-1033 *unknown*\*unknown* (8)
S-1-5-32-1034 *unknown*\*unknown* (8)
S-1-5-32-1035 *unknown*\*unknown* (8)
S-1-5-32-1036 *unknown*\*unknown* (8)
S-1-5-32-1037 *unknown*\*unknown* (8)
S-1-5-32-1038 *unknown*\*unknown* (8)
S-1-5-32-1039 *unknown*\*unknown* (8)
S-1-5-32-1040 *unknown*\*unknown* (8)
S-1-5-32-1041 *unknown*\*unknown* (8)
S-1-5-32-1042 *unknown*\*unknown* (8)
S-1-5-32-1043 *unknown*\*unknown* (8)
S-1-5-32-1044 *unknown*\*unknown* (8)
S-1-5-32-1045 *unknown*\*unknown* (8)
S-1-5-32-1046 *unknown*\*unknown* (8)
S-1-5-32-1047 *unknown*\*unknown* (8)
S-1-5-32-1048 *unknown*\*unknown* (8)
S-1-5-32-1049 *unknown*\*unknown* (8)
S-1-5-32-1050 *unknown*\*unknown* (8)

 =============================================== 
|    Getting printer info for 192.168.100.52    |
 =============================================== 
No printers returned.


enum4linux complete on Sun Dec 21 23:25:22 2025

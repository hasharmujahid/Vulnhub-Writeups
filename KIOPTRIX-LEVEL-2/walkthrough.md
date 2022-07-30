KIOPTRIX LEVEL NO 2
==================

HOST DISCOVERY
==============

```
┌──(kali㉿kali)-[~/Desktop/THM/VULNHUB/KIOPTRIX-LEVEL-1]
└─$ sudo nmap -sP 192.168.100.1/24
Starting Nmap 7.92 ( https://nmap.org ) at 2022-05-20 14:17 EDT
Nmap scan report for 192.168.100.1
Host is up (0.0017s latency).
MAC Address: 24:44:27:2A:9C:C0 (Huawei Technologies)
Nmap scan report for 192.168.100.4
Host is up (0.014s latency).
MAC Address: 04:79:70:F0:45:B7 (Huawei Technologies)
Nmap scan report for 192.168.100.6
Host is up (0.00042s latency).
MAC Address: 60:F6:77:8B:13:7F (Intel Corporate)
Nmap scan report for 192.168.100.54
Host is up (0.00066s latency).
MAC Address: 08:00:27:8D:4C:52 (Oracle VirtualBox virtual NIC)
Nmap scan report for 192.168.100.39
Host is up.
Nmap done: 256 IP addresses (5 hosts up) scanned in 2.19 seconds


HOST = Nmap scan report for 192.168.100.54


```

ENUMERATION
===========


NMAP
```bash
┌──(kali㉿kali)-[~/Desktop/THM/VULNHUB/KIOPTRIX-LEVEL-1]
└─$ sudo nmap -sS -sV -p- --min-rate 2000 192.168.100.54 -oN nmap.md 
Starting Nmap 7.92 ( https://nmap.org ) at 2022-05-20 14:18 EDT
Nmap scan report for 192.168.100.54
Host is up (0.00029s latency).
Not shown: 65528 closed tcp ports (reset)
PORT     STATE SERVICE  VERSION
22/tcp   open  ssh      OpenSSH 3.9p1 (protocol 1.99)
80/tcp   open  http     Apache httpd 2.0.52 ((CentOS))
111/tcp  open  rpcbind  2 (RPC #100000)
443/tcp  open  ssl/http Apache httpd 2.0.52 ((CentOS))
631/tcp  open  ipp      CUPS 1.1
927/tcp  open  status   1 (RPC #100024)
3306/tcp open  mysql    MySQL (unauthorized)
MAC Address: 08:00:27:8D:4C:52 (Oracle VirtualBox virtual NIC)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 18.30 seconds




```

PORT 80  and 443:
========

```

http://192.168.100.54/

LOGIN PORTAL BYPASSED IT BY ' or 1=1 -- -


REDIRECTED TO ===> http://192.168.100.54/index.php





```

NIKTO
=====

```bash

┌──(kali㉿kali)-[~/Desktop/THM/VULNHUB/KIOPTRIX-LEVEL-1]
└─$ nikto --host  https://192.168.100.54/ | tee nikto8011.md
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          192.168.100.54
+ Target Hostname:    192.168.100.54
+ Target Port:        443
---------------------------------------------------------------------------
+ SSL Info:        Subject:  /C=--/ST=SomeState/L=SomeCity/O=SomeOrganization/OU=SomeOrganizationalUnit/CN=localhost.localdomain/emailAddress=root@localhost.localdomain
                   Ciphers:  DHE-RSA-AES256-SHA
                   Issuer:   /C=--/ST=SomeState/L=SomeCity/O=SomeOrganization/OU=SomeOrganizationalUnit/CN=localhost.localdomain/emailAddress=root@localhost.localdomain
+ Start Time:         2022-05-20 14:36:05 (GMT-4)
---------------------------------------------------------------------------
+ Server: Apache/2.0.52 (CentOS)
+ Retrieved x-powered-by header: PHP/4.3.9
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The site uses SSL and the Strict-Transport-Security HTTP header is not defined.
+ The site uses SSL and Expect-CT header is not present.
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ Apache/2.0.52 appears to be outdated (current is at least Apache/2.4.37). Apache 2.2.34 is the EOL for the 2.x branch.
+ Hostname '192.168.100.54' does not match certificate's names: localhost.localdomain
+ Allowed HTTP Methods: GET, HEAD, POST, OPTIONS, TRACE 
+ Web Server returns a valid response with junk HTTP methods, this may cause false positives.
+ OSVDB-877: HTTP TRACE method is active, suggesting the host is vulnerable to XST
+ OSVDB-12184: /?=PHPB8B5F2A0-3C92-11d3-A3A9-4C7B08C10000: PHP reveals potentially sensitive information via certain HTTP requests that contain specific QUERY strings.
+ OSVDB-12184: /?=PHPE9568F34-D428-11d2-A769-00AA001ACF42: PHP reveals potentially sensitive information via certain HTTP requests that contain specific QUERY strings.
+ OSVDB-12184: /?=PHPE9568F35-D428-11d2-A769-00AA001ACF42: PHP reveals potentially sensitive information via certain HTTP requests that contain specific QUERY strings.
+ Uncommon header 'tcn' found, with contents: choice
+ OSVDB-3092: /manual/: Web server manual found.
+ OSVDB-3268: /icons/: Directory indexing found.
+ OSVDB-3268: /manual/images/: Directory indexing found.
+ Server may leak inodes via ETags, header found with file /icons/README, inode: 357810, size: 4872, mtime: Sat Mar 29 13:41:04 1980
+ OSVDB-3233: /icons/README: Apache default file found.
+ 8725 requests: 1 error(s) and 20 item(s) reported on remote host
+ End Time:           2022-05-20 14:43:21 (GMT-4) (436 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested



```
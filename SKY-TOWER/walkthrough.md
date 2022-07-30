SKY-TOWER
=========


DATE 19-05-2022 TIME = 8:15
===========================

HOST DISCOVERY
==============

```

 Currently scanning: 172.16.5.0/16   |   Screen View: Unique Hosts                                                                                                    
                                                                                                                                                                      
 5 Captured ARP Req/Rep packets, from 3 hosts.   Total size: 300                                                                                                      
 _____________________________________________________________________________
   IP            At MAC Address     Count     Len  MAC Vendor / Hostname      
 -----------------------------------------------------------------------------
 192.168.100.6   60:f6:77:8b:13:7f      1      60  Intel Corporate                                                                                                    
 192.168.100.52  08:00:27:54:4a:37      2     120  PCS Systemtechnik GmbH                                                                                             
 192.168.100.1   24:44:27:2a:9c:c0      2     120  HUAWEI TECHNOLOGIES CO.,LTD   


```

NMAP
====

```

┌──(kali㉿kali)-[~/Desktop/THM/VULNHUB/SKY-TOWER]
└─$ sudo nmap -sC -sV -p- --min-rate 1500 192.168.100.52 | tee nmapall.md
Starting Nmap 7.92 ( https://nmap.org ) at 2022-05-19 11:11 EDT
Nmap scan report for 192.168.100.52
Host is up (0.00059s latency).
Not shown: 65532 closed tcp ports (reset)
PORT     STATE    SERVICE    VERSION
22/tcp   filtered ssh
80/tcp   open     http       Apache httpd 2.2.22 ((Debian))
|_http-title: Site doesn't have a title (text/html).
|_http-server-header: Apache/2.2.22 (Debian)
3128/tcp open     http-proxy Squid http proxy 3.1.20
|_http-title: ERROR: The requested URL could not be retrieved
| http-open-proxy: Potentially OPEN proxy.
|_Methods supported: GET HEAD
|_http-server-header: squid/3.1.20
MAC Address: 08:00:27:54:4A:37 (Oracle VirtualBox virtual NIC)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 19.11 seconds



```

PORT 22;
========

```

SSH ===> NOTHING JIUICY

```

PORT 80 :
=========

```


┌──(kali㉿kali)-[~/Desktop/THM/VULNHUB/SKY-TOWER]
└─$ gobuster dir -u http://192.168.100.52/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt --no-error  -t 100 -x php,txt,html
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.100.52/
[+] Method:                  GET
[+] Threads:                 100
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Extensions:              php,txt,html
[+] Timeout:                 10s
===============================================================
2022/05/19 11:13:17 Starting gobuster in directory enumeration mode
===============================================================
/index.html           (Status: 200) [Size: 1136]
/index                (Status: 200) [Size: 1136]
/background           (Status: 200) [Size: 2572609]
/login.php            (Status: 200) [Size: 21]     
/background2          (Status: 200) [Size: 2831446]
/server-status        (Status: 403) [Size: 295]    
                                                   
===============================================================
2022/05/19 11:23:00 Finished
===============================================================

```

NIKTO
=====

```

┌──(kali㉿kali)-[~/Desktop/THM/VULNHUB/SKY-TOWER]
└─$ nikto --host  http://192.168.100.52/ | tee nikto8011.md
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          192.168.100.52
+ Target Hostname:    192.168.100.52
+ Target Port:        80
+ Start Time:         2022-05-19 11:23:57 (GMT-4)
---------------------------------------------------------------------------
+ Server: Apache/2.2.22 (Debian)
+ Server may leak inodes via ETags, header found with file /, inode: 87, size: 1136, mtime: Fri Jun 20 07:23:36 2014
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ Apache/2.2.22 appears to be outdated (current is at least Apache/2.4.37). Apache 2.2.34 is the EOL for the 2.x branch.
+ Uncommon header 'tcn' found, with contents: list
+ Apache mod_negotiation is enabled with MultiViews, which allows attackers to easily brute force file names. See http://www.wisec.it/sectou.php?id=4698ebdc59d15. The following alternatives for 'index' were found: index.html
+ Allowed HTTP Methods: GET, HEAD, POST, OPTIONS 
+ Retrieved x-powered-by header: PHP/5.4.4-14+deb7u9
+ OSVDB-3233: /icons/README: Apache default file found.
+ /login.php: Admin login page/section found.
+ 8725 requests: 0 error(s) and 11 item(s) reported on remote host
+ End Time:           2022-05-19 11:24:31 (GMT-4) (34 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested


```

/LOGIN
=======

```
CONTAINS SQL INJECTION VULNERABILITY 

TRIED TO BYPASS WITH THE ' or 1=1 -- - BUT FAILED 

TOOK A HINT BYPASSWED WITH => " '|| 1=1 # "

informations ==> 

Welcome john@skytech.com

As you may know, SkyTech has ceased all international operations.

To all our long term employees, we wish to convey our thanks for your dedication and hard work.

Unfortunately, all international contracts, including yours have been terminated.

The remainder of your contract and retirement fund, $2 ,has been payed out in full to a secure account. For security reasons, you must login to the SkyTech server via SSH to access the account details.

Username: john
Password: hereisjohn

We wish you the best of luck in your future 


```

NEXT STEPS :

```

WE GOT CREDS ```Username: john Password: hereisjohn```  WE SHOULD TRY SSH FTER I WILL LOOK INTO PORT 3128 

```

SSH
===

```




```
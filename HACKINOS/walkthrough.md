HACKINOS
========

HOST DISCOVERY
==============

```
 Currently scanning: 192.168.135.0/16   |   Screen View: Unique Hosts                                                                                                 
                                                                                                                                                                      
 3 Captured ARP Req/Rep packets, from 3 hosts.   Total size: 180                                                                                                      
 _____________________________________________________________________________
   IP            At MAC Address     Count     Len  MAC Vendor / Hostname      
 -----------------------------------------------------------------------------
 192.168.100.3   3e:6a:61:7f:a0:b9      1      60  Unknown vendor                                                                                                     
 192.168.100.6   60:f6:77:8b:13:7f      1      60  Intel Corporate                                                                                                    
 192.168.100.53  08:00:27:20:a9:bc      1      60  PCS Systemtechnik GmbH   

```

NMAP
====

```


┌──(kali㉿kali)-[~/Desktop/THM/VULNHUB/HACKINOS]
└─$ sudo nmap -sC -sV -p- --min-rate 1500 192.168.100.53 | tee nmapall.md
Starting Nmap 7.92 ( https://nmap.org ) at 2022-05-19 15:24 EDT
Nmap scan report for 192.168.100.53
Host is up (0.00026s latency).
Not shown: 65533 closed tcp ports (reset)
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 d9:c1:5c:20:9a:77:54:f8:a3:41:18:92:1b:1e:e5:35 (RSA)
|   256 df:d4:f2:61:89:61:ac:e0:ee:3b:5d:07:0d:3f:0c:87 (ECDSA)
|_  256 8b:e4:45:ab:af:c8:0e:7e:2a:e4:47:e7:52:f9:bc:71 (ED25519)
8000/tcp open  http    Apache httpd 2.4.25 ((Debian))
|_http-generator: WordPress 5.0.3
| http-robots.txt: 2 disallowed entries 
|_/upload.php /uploads
|_http-title: Blog &#8211; Just another WordPress site
|_http-open-proxy: Proxy might be redirecting requests
|_http-server-header: Apache/2.4.25 (Debian)
MAC Address: 08:00:27:20:A9:BC (Oracle VirtualBox virtual NIC)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 24.23 seconds


```

====================================================================================================================
====================================================================================================================

PORT 8000
=========


DIRECTORY SCAN
--------------
```

┌──(kali㉿kali)-[~/Desktop/THM/VULNHUB/HACKINOS]
└─$ gobuster dir -u http://192.168.100.53:8000/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt --no-error  -t 100 -x php,txt,html
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.100.53:8000/
[+] Method:                  GET
[+] Threads:                 100
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Extensions:              php,txt,html
[+] Timeout:                 10s
===============================================================
2022/05/19 15:27:51 Starting gobuster in directory enumeration mode
===============================================================
/uploads              (Status: 301) [Size: 325] [--> http://192.168.100.53:8000/uploads/]
/wp-content           (Status: 301) [Size: 328] [--> http://192.168.100.53:8000/wp-content/]
/upload.php           (Status: 200) [Size: 418]                                             
/index.php            (Status: 301) [Size: 0] [--> http://192.168.100.53:8000/]             
/wp-login.php         (Status: 200) [Size: 3179]                                            
/license.txt          (Status: 200) [Size: 19935]                                           
/wp-includes          (Status: 301) [Size: 329] [--> http://192.168.100.53:8000/wp-includes/]
/robots.txt           (Status: 200) [Size: 52]                                               
/readme.html          (Status: 200) [Size: 7415]                                             
/wp-admin             (Status: 301) [Size: 326] [--> http://192.168.100.53:8000/wp-admin/]   
/server-status        (Status: 403) [Size: 304]                                              
Progress: 537252 / 882244 (60.90%)                                                          ^C
[!] Keyboard interrupt detected, terminating.
                                                                                             
===============================================================
2022/05/19 15:36:32 Finished
===============================================================


```


====================================================================================================================
====================================================================================================================


WP-SCAN
=======

```


┌──(kali㉿kali)-[~/Desktop/THM/VULNHUB/HACKINOS]
└─$ wpscan --url http://192.168.100.53:8000/ -e vp,vt,u,dbe
_______________________________________________________________
         __          _______   _____
         \ \        / /  __ \ / ____|
          \ \  /\  / /| |__) | (___   ___  __ _ _ __ ®
           \ \/  \/ / |  ___/ \___ \ / __|/ _` | '_ \
            \  /\  /  | |     ____) | (__| (_| | | | |
             \/  \/   |_|    |_____/ \___|\__,_|_| |_|

         WordPress Security Scanner by the WPScan Team
                         Version 3.8.20
       Sponsored by Automattic - https://automattic.com/
       @_WPScan_, @ethicalhack3r, @erwan_lr, @firefart
_______________________________________________________________

[i] It seems like you have not updated the database for some time.
[?] Do you want to update now? [Y]es [N]o, default: [N]Y
[i] Updating the Database ...
[i] Update completed.

[+] URL: http://192.168.100.53:8000/ [192.168.100.53]
[+] Started: Thu May 19 15:40:37 2022

Interesting Finding(s):

[+] Headers
 | Interesting Entries:
 |  - Server: Apache/2.4.25 (Debian)
 |  - X-Powered-By: PHP/7.2.15
 | Found By: Headers (Passive Detection)
 | Confidence: 100%

[+] robots.txt found: http://192.168.100.53:8000/robots.txt
 | Found By: Robots Txt (Aggressive Detection)
 | Confidence: 100%

[+] XML-RPC seems to be enabled: http://192.168.100.53:8000/xmlrpc.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%
 | References:
 |  - http://codex.wordpress.org/XML-RPC_Pingback_API
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner/
 |  - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access/

[+] WordPress readme found: http://192.168.100.53:8000/readme.html
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] The external WP-Cron seems to be enabled: http://192.168.100.53:8000/wp-cron.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 60%
 | References:
 |  - https://www.iplocation.net/defend-wordpress-from-ddos
 |  - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 5.0.3 identified (Insecure, released on 2019-01-09).
 | Found By: Emoji Settings (Passive Detection)
 |  - http://192.168.100.53:8000/, Match: 'wp-includes\/js\/wp-emoji-release.min.js?ver=5.0.3'
 | Confirmed By: Meta Generator (Passive Detection)
 |  - http://192.168.100.53:8000/, Match: 'WordPress 5.0.3'

[i] The main theme could not be detected.

[+] Enumerating Vulnerable Plugins (via Passive Methods)

[i] No plugins Found.

[+] Enumerating Vulnerable Themes (via Passive and Aggressive Methods)
 Checking Known Locations - Time: 00:00:03 <=======================================================================================> (472 / 472) 100.00% Time: 00:00:03

[i] No themes Found.

[+] Enumerating DB Exports (via Passive and Aggressive Methods)
 Checking DB Exports - Time: 00:00:00 <==============================================================================================> (71 / 71) 100.00% Time: 00:00:00

[i] No DB Exports Found.

[+] Enumerating Users (via Passive and Aggressive Methods)
 Brute Forcing Author IDs - Time: 00:00:00 <=========================================================================================> (10 / 10) 100.00% Time: 00:00:00

[i] User(s) Identified:

[+] handsome_container
 | Found By: Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 | Confirmed By: Login Error Messages (Aggressive Detection)

[!] No WPScan API Token given, as a result vulnerability data has not been output.
[!] You can get a free API token with 25 daily requests by registering at https://wpscan.com/register

[+] Finished: Thu May 19 15:40:53 2022
[+] Requests Done: 603
[+] Cached Requests: 5
[+] Data Sent: 161.457 KB
[+] Data Received: 18.275 MB
[+] Memory used: 218.836 MB
[+] Elapsed time: 00:00:16


```
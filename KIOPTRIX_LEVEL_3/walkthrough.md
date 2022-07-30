KIOPTRIX LEVEL 3
================

NETWORK-DISCOVERY
=================

```

 Currently scanning: 192.168.143.0/16   |   Screen View: Unique Hosts                                                                                                
                                                                                                                                                                     
 13 Captured ARP Req/Rep packets, from 4 hosts.   Total size: 780                                                                                                    
 _____________________________________________________________________________
   IP            At MAC Address     Count     Len  MAC Vendor / Hostname      
 -----------------------------------------------------------------------------
 192.168.100.1   24:44:27:2a:9c:c0      1      60  HUAWEI TECHNOLOGIES CO.,LTD                                                                                       
 192.168.100.6   60:f6:77:8b:13:7f      1      60  Intel Corporate                                                                                                   
 192.168.100.55  08:00:27:c3:a4:d6     10     600  PCS Systemtechnik GmbH                                                                                            
 192.168.100.3   3e:6a:61:7f:a0:b9      1      60  Unknown vendor                                                                                                    




```

NAMP
====
```


┌──(kali㉿kali)-[~/Desktop/THM/VULNHUB/KIOPTRIX_LEVEL_3]
└─$ sudo nmap -sS -sV -p- --min-rate 2000 192.168.100.55 -oN nmap.md
Starting Nmap 7.92 ( https://nmap.org ) at 2022-05-27 11:30 EDT
Stats: 0:00:02 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 61.30% done; ETC: 11:30 (0:00:01 remaining)
Nmap scan report for 192.168.100.55
Host is up (0.00032s latency).
Not shown: 65533 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 4.7p1 Debian 8ubuntu1.2 (protocol 2.0)
80/tcp open  http    Apache httpd 2.2.8 ((Ubuntu) PHP/5.2.4-2ubuntu5.6 with Suhosin-Patch)
MAC Address: 08:00:27:C3:A4:D6 (Oracle VirtualBox virtual NIC)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 10.59 seconds


```

WEB-RECON
=========

```
POWRED BY =  LotusCMS s{


┌──(kali㉿kali)-[~/Desktop/THM/VULNHUB/KIOPTRIX_LEVEL_3]
└─$ searchsploit  LotusCMS                                          
------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                                                                       |  Path
------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
LotusCMS 3.0 - 'eval()' Remote Command Execution Metasploit)                                                                        | php/remote/18565.rb
LotusCMS 3.0.3 - Multiple Vulnerabilities                                                                                            | php/webapps/16982.txt
------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results



}

LOGIN PAGE = http://192.168.100.55/index.php?system=Admin

X-Powered-By = PHP/5.2.4-2ubuntu5.6



```

WEB-DIRECTORIES
===============

```bash

┌──(kali㉿kali)-[~/Desktop/THM/VULNHUB/KIOPTRIX_LEVEL_3]
└─$ gobuster dir -u http://192.168.100.55/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt --no-error  -t 100 -x php,txt,html
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.100.55/
[+] Method:                  GET
[+] Threads:                 100
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Extensions:              php,txt,html
[+] Timeout:                 10s
===============================================================
2022/05/27 11:35:01 Starting gobuster in directory enumeration mode
===============================================================
/index.php            (Status: 200) [Size: 1819]
/modules              (Status: 301) [Size: 357] [--> http://192.168.100.55/modules/]
/gallery              (Status: 301) [Size: 357] [--> http://192.168.100.55/gallery/]
/data                 (Status: 403) [Size: 325]                                     
/core                 (Status: 301) [Size: 354] [--> http://192.168.100.55/core/]   
/update.php           (Status: 200) [Size: 18]                                      
/style                (Status: 301) [Size: 355] [--> http://192.168.100.55/style/]  
/cache                (Status: 301) [Size: 355] [--> http://192.168.100.55/cache/]  
/phpmyadmin           (Status: 301) [Size: 360] [--> http://192.168.100.55/phpmyadmin/]
/server-status        (Status: 403) [Size: 334]                                        
                                                                                       
===============================================================
2022/05/27 11:40:26 Finished
===============================================================




```
PHP-MY-ADMIN
============

```bash

Welcome to phpMyAdmin 2.11.3deb1ubuntu1.3


LOGIN CAN BE BYPASSED BY INJECTING ====> 'root-- -'


WILL BE BACK TO ENUMERATE SOME MORE

```

LOGIN IN LOTUS 
==============

```

RUN SQLMAP ===> FAILED

TRY DEFAULT GREDENTIALS

IF DOESNOT WORK BACK TO EXPLOIT PHPMYADMIN OR LOTUSCMS



```
EXPLOITING LOTUS
================

```

TRIED EVAL()  EXPLOIT DOESNOT NOT WORK


```

EXPLOITING PHPMYADMIN
=====================

```
TRYING
------
phpMyAdmin - '/scripts/setup.php' PHP Code Injection 

http://192.168.100.55/phpmyadmin
```
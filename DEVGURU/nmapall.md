Starting Nmap 7.92 ( https://nmap.org ) at 2022-07-19 02:25 EDT
Nmap scan report for 192.168.100.72
Host is up (0.00023s latency).
Not shown: 65532 closed tcp ports (reset)
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.6p1 Ubuntu 4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 2a:46:e8:2b:01:ff:57:58:7a:5f:25:a4:d6:f2:89:8e (RSA)
|   256 08:79:93:9c:e3:b4:a4:be:80:ad:61:9d:d3:88:d2:84 (ECDSA)
|_  256 9c:f9:88:d4:33:77:06:4e:d9:7c:39:17:3e:07:9c:bd (ED25519)
80/tcp   open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-title: Corp - DevGuru
| http-git: 
|   192.168.100.72:80/.git/
|     Git repository found!
|     Repository description: Unnamed repository; edit this file 'description' to name the...
|     Last commit message: first commit 
|     Remotes:
|       http://devguru.local:8585/frank/devguru-website.git
|_    Project type: PHP application (guessed from .gitignore)
|_http-generator: DevGuru
|_http-server-header: Apache/2.4.29 (Ubuntu)
8585/tcp open  unknown
| fingerprint-strings: 
|   GenericLines: 
|     HTTP/1.1 400 Bad Request
|     Content-Type: text/plain; charset=utf-8
|     Connection: close
|     Request
|   GetRequest: 
|     HTTP/1.0 200 OK
|     Content-Type: text/html; charset=UTF-8
|     Set-Cookie: lang=en-US; Path=/; Max-Age=2147483647
|     Set-Cookie: i_like_gitea=671b9d136662a4f1; Path=/; HttpOnly
|     Set-Cookie: _csrf=R3lbk1b6ebdzQDiAQPgrf6i_L006MTY1ODIxMTk1OTEzMDI2OTkyNw; Path=/; Expires=Wed, 20 Jul 2022 06:25:59 GMT; HttpOnly
|     X-Frame-Options: SAMEORIGIN
|     Date: Tue, 19 Jul 2022 06:25:59 GMT
|     <!DOCTYPE html>
|     <html lang="en-US" class="theme-">
|     <head data-suburl="">
|     <meta charset="utf-8">
|     <meta name="viewport" content="width=device-width, initial-scale=1">
|     <meta http-equiv="x-ua-compatible" content="ie=edge">
|     <title> Gitea: Git with a cup of tea </title>
|     <link rel="manifest" href="/manifest.json" crossorigin="use-credentials">
|     <meta name="theme-color" content="#6cc644">
|     <meta name="author" content="Gitea - Git with a cup of tea" />
|     <meta name="description" content="Gitea (Git with a cup of tea) is a painless
|   HTTPOptions: 
|     HTTP/1.0 404 Not Found
|     Content-Type: text/html; charset=UTF-8
|     Set-Cookie: lang=en-US; Path=/; Max-Age=2147483647
|     Set-Cookie: i_like_gitea=7f1cf787587014b9; Path=/; HttpOnly
|     Set-Cookie: _csrf=emmmgvHc97JUrqeGOPaSJGveVes6MTY1ODIxMTk1OTM3MTg0Njc2OA; Path=/; Expires=Wed, 20 Jul 2022 06:25:59 GMT; HttpOnly
|     X-Frame-Options: SAMEORIGIN
|     Date: Tue, 19 Jul 2022 06:25:59 GMT
|     <!DOCTYPE html>
|     <html lang="en-US" class="theme-">
|     <head data-suburl="">
|     <meta charset="utf-8">
|     <meta name="viewport" content="width=device-width, initial-scale=1">
|     <meta http-equiv="x-ua-compatible" content="ie=edge">
|     <title>Page Not Found - Gitea: Git with a cup of tea </title>
|     <link rel="manifest" href="/manifest.json" crossorigin="use-credentials">
|     <meta name="theme-color" content="#6cc644">
|     <meta name="author" content="Gitea - Git with a cup of tea" />
|_    <meta name="description" content="Gitea (Git with a c
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port8585-TCP:V=7.92%I=7%D=7/19%Time=62D64E76%P=x86_64-pc-linux-gnu%r(Ge
SF:nericLines,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Type:\x20t
SF:ext/plain;\x20charset=utf-8\r\nConnection:\x20close\r\n\r\n400\x20Bad\x
SF:20Request")%r(GetRequest,2A04,"HTTP/1\.0\x20200\x20OK\r\nContent-Type:\
SF:x20text/html;\x20charset=UTF-8\r\nSet-Cookie:\x20lang=en-US;\x20Path=/;
SF:\x20Max-Age=2147483647\r\nSet-Cookie:\x20i_like_gitea=671b9d136662a4f1;
SF:\x20Path=/;\x20HttpOnly\r\nSet-Cookie:\x20_csrf=R3lbk1b6ebdzQDiAQPgrf6i
SF:_L006MTY1ODIxMTk1OTEzMDI2OTkyNw;\x20Path=/;\x20Expires=Wed,\x2020\x20Ju
SF:l\x202022\x2006:25:59\x20GMT;\x20HttpOnly\r\nX-Frame-Options:\x20SAMEOR
SF:IGIN\r\nDate:\x20Tue,\x2019\x20Jul\x202022\x2006:25:59\x20GMT\r\n\r\n<!
SF:DOCTYPE\x20html>\n<html\x20lang=\"en-US\"\x20class=\"theme-\">\n<head\x
SF:20data-suburl=\"\">\n\t<meta\x20charset=\"utf-8\">\n\t<meta\x20name=\"v
SF:iewport\"\x20content=\"width=device-width,\x20initial-scale=1\">\n\t<me
SF:ta\x20http-equiv=\"x-ua-compatible\"\x20content=\"ie=edge\">\n\t<title>
SF:\x20Gitea:\x20Git\x20with\x20a\x20cup\x20of\x20tea\x20</title>\n\t<link
SF:\x20rel=\"manifest\"\x20href=\"/manifest\.json\"\x20crossorigin=\"use-c
SF:redentials\">\n\t<meta\x20name=\"theme-color\"\x20content=\"#6cc644\">\
SF:n\t<meta\x20name=\"author\"\x20content=\"Gitea\x20-\x20Git\x20with\x20a
SF:\x20cup\x20of\x20tea\"\x20/>\n\t<meta\x20name=\"description\"\x20conten
SF:t=\"Gitea\x20\(Git\x20with\x20a\x20cup\x20of\x20tea\)\x20is\x20a\x20pai
SF:nless")%r(HTTPOptions,212E,"HTTP/1\.0\x20404\x20Not\x20Found\r\nContent
SF:-Type:\x20text/html;\x20charset=UTF-8\r\nSet-Cookie:\x20lang=en-US;\x20
SF:Path=/;\x20Max-Age=2147483647\r\nSet-Cookie:\x20i_like_gitea=7f1cf78758
SF:7014b9;\x20Path=/;\x20HttpOnly\r\nSet-Cookie:\x20_csrf=emmmgvHc97JUrqeG
SF:OPaSJGveVes6MTY1ODIxMTk1OTM3MTg0Njc2OA;\x20Path=/;\x20Expires=Wed,\x202
SF:0\x20Jul\x202022\x2006:25:59\x20GMT;\x20HttpOnly\r\nX-Frame-Options:\x2
SF:0SAMEORIGIN\r\nDate:\x20Tue,\x2019\x20Jul\x202022\x2006:25:59\x20GMT\r\
SF:n\r\n<!DOCTYPE\x20html>\n<html\x20lang=\"en-US\"\x20class=\"theme-\">\n
SF:<head\x20data-suburl=\"\">\n\t<meta\x20charset=\"utf-8\">\n\t<meta\x20n
SF:ame=\"viewport\"\x20content=\"width=device-width,\x20initial-scale=1\">
SF:\n\t<meta\x20http-equiv=\"x-ua-compatible\"\x20content=\"ie=edge\">\n\t
SF:<title>Page\x20Not\x20Found\x20-\x20\x20Gitea:\x20Git\x20with\x20a\x20c
SF:up\x20of\x20tea\x20</title>\n\t<link\x20rel=\"manifest\"\x20href=\"/man
SF:ifest\.json\"\x20crossorigin=\"use-credentials\">\n\t<meta\x20name=\"th
SF:eme-color\"\x20content=\"#6cc644\">\n\t<meta\x20name=\"author\"\x20cont
SF:ent=\"Gitea\x20-\x20Git\x20with\x20a\x20cup\x20of\x20tea\"\x20/>\n\t<me
SF:ta\x20name=\"description\"\x20content=\"Gitea\x20\(Git\x20with\x20a\x20
SF:c");
MAC Address: 08:00:27:0B:2B:67 (Oracle VirtualBox virtual NIC)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 98.03 seconds

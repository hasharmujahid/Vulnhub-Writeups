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

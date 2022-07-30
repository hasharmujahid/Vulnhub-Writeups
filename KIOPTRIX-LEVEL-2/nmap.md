# Nmap 7.92 scan initiated Fri May 20 14:18:52 2022 as: nmap -sS -sV -p- --min-rate 2000 -oN nmap.md 192.168.100.54
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
# Nmap done at Fri May 20 14:19:11 2022 -- 1 IP address (1 host up) scanned in 18.30 seconds

Nmap 
 ```
sudo nmap -p- --min-rate 5000 -n -Pn $TARGET -oA tcp-all

Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-09-06 21:00 CST
Warning: 10.129.231.231 giving up on port because retransmission cap hit (10).
Nmap scan report for 10.129.231.231
Host is up (0.088s latency).
Not shown: 65069 closed tcp ports (reset), 443 filtered tcp ports (no-response)
PORT      STATE SERVICE
53/tcp    open  domain
88/tcp    open  kerberos-sec
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
389/tcp   open  ldap
445/tcp   open  microsoft-ds
464/tcp   open  kpasswd5
593/tcp   open  http-rpc-epmap
636/tcp   open  ldapssl
3268/tcp  open  globalcatLDAP
3269/tcp  open  globalcatLDAPssl
5985/tcp  open  wsman
9389/tcp  open  adws
47001/tcp open  winrm
49664/tcp open  unknown
49665/tcp open  unknown
49666/tcp open  unknown
49668/tcp open  unknown
49671/tcp open  unknown
49676/tcp open  unknown
49677/tcp open  unknown
49683/tcp open  unknown
49698/tcp open  unknown
 ```
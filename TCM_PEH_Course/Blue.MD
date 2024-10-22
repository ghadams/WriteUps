IP: 192.168.56.103

Set IP in Kali:

```
echo 'export IP=192.168.56.103' >> ~/.zshrc
source ~/.zshrc
```

## Enumeration

Nmap:

```
$ nmap -A -T4 $IP
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-10-22 11:24 EDT
Stats: 0:01:00 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 75.00% done; ETC: 11:25 (0:00:19 remaining)                                                    
Nmap scan report for 192.168.56.103                                                                                       
Host is up (0.00088s latency).                                                                                            
Not shown: 992 closed tcp ports (reset)                                                                                   
PORT      STATE SERVICE      VERSION                                                                                      
135/tcp   open  msrpc        Microsoft Windows RPC                                                                        
139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn                                                                
445/tcp   open  microsoft-ds Windows 7 Ultimate 7601 Service Pack 1 microsoft-ds (workgroup: WORKGROUP)                   
49152/tcp open  msrpc        Microsoft Windows RPC
49153/tcp open  msrpc        Microsoft Windows RPC
49154/tcp open  msrpc        Microsoft Windows RPC
49155/tcp open  msrpc        Microsoft Windows RPC
49156/tcp open  msrpc        Microsoft Windows RPC
MAC Address: 08:00:27:C4:8F:24 (Oracle VirtualBox virtual NIC)
Device type: general purpose
Running: Microsoft Windows 7|2008|8.1
OS CPE: cpe:/o:microsoft:windows_7::- cpe:/o:microsoft:windows_7::sp1 cpe:/o:microsoft:windows_server_2008::sp1 cpe:/o:microsoft:windows_server_2008:r2 cpe:/o:microsoft:windows_8 cpe:/o:microsoft:windows_8.1
OS details: Microsoft Windows 7 SP0 - SP1, Windows Server 2008 SP1, Windows Server 2008 R2, Windows 8, or Windows 8.1 Update 1
Network Distance: 1 hop
Service Info: Host: WIN-845Q99OO4PP; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2024-10-22T15:25:07
|_  start_date: 2024-10-22T15:15:52
|_clock-skew: mean: 1h20m00s, deviation: 2h18m34s, median: 0s
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_nbstat: NetBIOS name: WIN-845Q99OO4PP, NetBIOS user: <unknown>, NetBIOS MAC: 08:00:27:c4:8f:24 (Oracle VirtualBox virtual NIC)
| smb-os-discovery: 
|   OS: Windows 7 Ultimate 7601 Service Pack 1 (Windows 7 Ultimate 6.1)
|   OS CPE: cpe:/o:microsoft:windows_7::sp1
|   Computer name: WIN-845Q99OO4PP
|   NetBIOS computer name: WIN-845Q99OO4PP\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2024-10-22T11:25:07-04:00
| smb2-security-mode: 
|   2:1:0: 
|_    Message signing enabled but not required

TRACEROUTE
HOP RTT     ADDRESS
1   0.88 ms 192.168.56.103

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 67.58 seconds

```

This version of SMB is vulnerable to EternalBlue.

Use windows/smb/ms17_010_psexec in metasploit.

Set rhosts and lhost. Set smbuser to guest.

Pwned:

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9dbd598d-7e94-428f-b960-b32eeb89a882/68b48422-7f21-4e9e-848a-28a15a2be315/image.png)

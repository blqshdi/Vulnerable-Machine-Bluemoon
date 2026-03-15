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


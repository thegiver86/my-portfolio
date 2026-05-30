<div align="center">

[![Typing SVG](https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=500&size=22&pause=1000&color=00FF88&center=true&vCenter=true&width=600&lines=Initializing+Operator+Environment...;Access+Granted:+Marcos+Cruz;Cybersecurity+Engineer+%7C+TKH+Class+of+2026)](https://git.io/typing-svg)

![Terminal Identity](https://coolreadme.xyz/api/hacker?user=thegiver86&status=OPERATOR+ONLINE&accent=%2300FF88)

[![Security](https://img.shields.io/badge/Security-Blue_Team_%7C_Red_Team-00FF88?style=for-the-badge&logo=tryhackme&logoColor=black)](#) 
[![Linux](https://img.shields.io/badge/Linux-Ubuntu_%7C_Alpine-black?style=for-the-badge&logo=linux&logoColor=white)](#) 
[![Docker](https://img.shields.io/badge/Docker-Containerization-2496ED?style=for-the-badge&logo=docker&logoColor=white)](#) 
[![Python](https://img.shields.io/badge/Python-Automation-3776AB?style=for-the-badge&logo=python&logoColor=white)](#)

> *"The system is yours. Do not fear the dark."*

</div>

---

## 📂 Phase 1 Operations Log

This repository serves as my living artifact cache for Phase 1 of the TKH Innovation Fellowship. It documents my progression through systems architecture, offensive exploitation, and active defense.

| Week | Operation Domain | Key Technologies / Concepts |
| :---: | :--- | :--- |
| **01** | Linux Fundamentals & FHS Navigation | `bash`, `chmod`, `grep`, `awk`, Privilege Escalation |
| **02** | Network Architecture & Subnetting | `ip route`, CIDR, TCP 3-Way Handshake, DNS Poisoning |
| **03** | Python Security Automation | `socket`, `subprocess`, Automated Log Parsing |
| **04** | Virtualization & Container Security | `Docker`, `docker-compose`, Network Air-Gapping |
| **05** | Identity & Access Management (IAM) | Active Directory, Windows Server Core, GPOs |
| **06** | **Midterm Capstone** | Infrastructure Hardening, Disaster Recovery |
| **07** | Reconnaissance & OSINT | `nmap`, `Shodan`, `Sublist3r`, Threat Profiling |
| **08** | Exploitation & Privilege Escalation | `Metasploit`, SUID Binaries, Reverse Shells |
| **09** | Web Application Security | SQL Injection (SQLi), Cross-Site Scripting (XSS), BOLA |
| **10** | DFIR & Threat Hunting | `ELK Stack`, Sleuth Kit (`fls`, `icat`), Disk Carving |
| **11** | Active Defense (Defense in Depth) | `Suricata IDS`, `Sysmon EDR`, `iptables` |
| **12** | **End of Phase Project (TEPP)** | Full Kill-Chain Execution, Incident Response |

---

## 🏆 Featured Capstones

<details>
<summary><b>🛡️ The Hardened Outpost (Midterm Capstone)</b></summary>
<br>

**Objective:** Stand up, secure, and automate a multi-tier containerized infrastructure.
* **Perimeter Security:** Hardened SSH (`PermitRootLogin no`) and deployed a `default-deny` UFW policy.
* **Containerized Air-Gapping:** Architected a Docker Compose stack featuring Nginx and MySQL. Ensured the database had zero external routing by placing it on an `internal: true` network.
* **Real-World Incident Response:** Overcame a physical hypervisor crash during deployment by identifying corrupted image metadata, purging the Docker cache, and executing a clean redeployment.
</details>

<details>
<summary><b>🧠 The Central Nervous System (DFIR & ELK)</b></summary>
<br>

**Objective:** Deploy a local ELK stack to ingest enterprise logs and reconstruct a full breach timeline.
* **Forensic Extraction:** Utilized the Sleuth Kit to interrogate raw disk images, locating orphaned inodes to prove malware was executing purely in volatile memory.
* **Log Correlation:** Queried Kibana (KQL) to track an adversary from an initial web server POST request, through lateral movement via Windows Event ID 4624, to final data exfiltration.
</details>

<details>
<summary><b>⚔️ The Final Reckoning (TEPP)</b></summary>
<br>

**Objective:** Execute a complete cyber kill chain across a multi-subnet range, followed immediately by Blue Team remediation.
* **Offensive Operations:** Mapped the network with Nmap, brute-forced SSH with Hydra, and exploited a custom Python Command Injection vulnerability via URL encoding to gain a root reverse shell.
* **Defensive Operations:** Transitioned to incident response by extracting forensic footprints (PIDs, User-Agents) from application logs and deploying strategic `iptables` rules to permanently isolate the compromised endpoints.
</details>

---

## 💻 Tactical Stack

**CLI & Shell:** `bash`, `awk`, `sed`, `grep`, `find`, `ss`, `chmod`  
**Infrastructure & Networking:** `Docker`, `Docker Compose`, `UFW`, `iptables`  
**Offensive & OSINT:** `nmap`, `Metasploit`, `Hydra`, `Sublist3r`, `Shodan`  
**Defensive:** `Suricata IDS`, `Sysmon EDR`, `ELK Stack / Kibana`  

<div align="center">
<br>
  
![Visitor Count](https://profile-counter.glitch.me/thegiver86/count.svg)

</div>

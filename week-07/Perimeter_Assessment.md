# Perimeter Assessment: Operation Shadow Map
**Target Subnet:** 172.88.0.0/24
**Lead Engineer:** turtle

## Phase 1: Subnet Sweeping (Active Recon)
* **Target Alpha (172.88.0.10):** nginx 1.14.2 (Port 80)
* **Target Beta (172.88.0.15):** Filtered/Unknown Cache Database (No standard ports open)
* **Target Gamma (172.88.0.20):** Apache httpd 2.4.66 ((Unix)) (Port 80)

## Phase 2: Vulnerability Auditing
* **172.88.0.10 (Nginx):** Nikto identified missing `X-Frame-Options` anti-clickjacking headers. Furthermore, Nmap identified the foundational software as Nginx 1.14.2, which is severely outdated (circa 2018).
* **172.88.0.20 (Apache):** Nikto identified that the `HTTP TRACE` method is active (OSVDB-877), rendering the host vulnerable to Cross-Site Tracing (XST) attacks.

## Phase 3: Risk Triage
* **Top Priority Finding:** Outdated Nginx Server (v1.14.2) on Target 172.88.0.10.
* **Justification:** The likelihood of exploitation is near-certain because the server is internet-facing with years of publicly available exploits, and the impact is critical because compromising the web server gives threat actors a direct foothold to pivot into the corporate DMZ.
